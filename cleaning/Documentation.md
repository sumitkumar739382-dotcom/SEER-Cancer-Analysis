1.  Overview

This document describes the complete data cleaning and preparation
pipeline applied to SEER (Surveillance, Epidemiology, and End Results)
cancer registry data. Five cancer types were extracted, cleaned
individually, and combined into a master analytical dataset. The
cleaning process was implemented in Python using the pandas and numpy
libraries.

Each cancer type follows an identical cleaning pipeline ensuring
consistency and comparability across cancer types. The only
cancer-specific differences are in primary site codes, histological
classification bins, and the Cancer_type identifier column.

1.1 Data Source

1.2 Variables Selected (16 Variables)

2.  Data Cleaning Pipeline

Each of the five cancer datasets was cleaned using an identical
step-by-step pipeline. The steps below describe each transformation with
the corresponding Python code, exactly as implemented in the cleaning
notebooks.

The following Python libraries were imported at the start of each
cleaning notebook:

pandas is used for all data loading, filtering, transformation and
export operations. numpy is used for vectorized computations, especially
for creating the Age and Income midpoint variables and applying
conditional logic using np.select().

The raw SEER CSV file is loaded for each cancer type:

Before proceeding with cleaning, exploratory steps were run to
understand each variable's content, data types, value counts, and unique
values:

The raw age variable is stored as a string range (e.g. '70-74 years',
'90+ years'). It cannot be used directly for calculations. The following
steps transform it into a numeric midpoint variable.

The midpoint approach (e.g., '70-74' becomes 72) provides a
representative numeric value for each age group while preserving the
original age recode column for reference.

The Primary Site column contains numeric ICD-O-3 site codes. These are
mapped to descriptive anatomical labels using a cancer-specific
dictionary. The mapping differs for each cancer type.

    500: 'Nipple and areola',  501: 'Central portion of breast',
    502: 'Upper-inner quadrant of breast',  503: 'Lower-inner quadrant of breast',
    504: 'Upper-outer quadrant of breast',  505: 'Lower-outer quadrant of breast',
    506: 'Axillary tail of breast',  508: 'Overlapping lesion of breast',

    340: 'Main bronchus',  341: 'Upper lobe, lung',  342: 'Middle lobe, lung',
    343: 'Lower lobe, lung',  348: 'Overlapping lesion of lung',  349: 'Lung, NOS'



    160: 'Cardia, NOS',  161: 'Fundus of stomach',  162: 'Body of stomach',
    163: 'Gastric antrum',  164: 'Pylorus',  165: 'Lesser curvature, NOS',
    166: 'Greater curvature, NOS',  168: 'Overlapping lesion',  169: 'Stomach, NOS'

The Histologic Type ICD-O-3 column contains numeric ICD-O-3 codes
representing specific cancer cell types. These are classified into
clinically meaningful groups using pd.cut() with cancer-specific bin
boundaries.

    bins=bins,
    labels=labels,
    ordered=False

)

The Combined Summary Stage variable contains descriptive text
categories. These are mapped to simplified clinical stages (I, II, III,
IV, Unknown) using a dictionary mapping.

    'Regional by direct extension only': 'II',
    'Regional lymph nodes involved only': 'III',
    'Regional by both direct extension and lymph node involvement': 'III',
    'Distant site(s)/node(s) involved': 'IV',
    'Unknown/unstaged/unspecified/DCO': 'Unknown',

The Radiation recode column contains detailed radiation type categories.
These are simplified to Yes/No/Unknown to indicate whether radiation was
received.

    'None/Unknown': 'No',
    'Radiation, NOS  method or source not specified': 'Yes',
    'Recommended, unknown if administered': 'Unknown',
    'Radioactive implants (includes brachytherapy) (1988+)': 'Yes',
    'Combination of beam with implants or isotopes': 'Yes',

The RX Summ--Surg Prim Site column contains numeric surgery procedure
codes. Code '0' indicates no surgery; code '99' and blanks indicate
unknown. All other codes represent various surgical interventions and
are mapped to 'Yes'.

    '0': 'No',                    # No surgical intervention
    '12': 'Yes', '13': 'Yes', '15': 'Yes', '19': 'Yes',   # Surgical interventions
    '20': 'Yes', '21': 'Yes', '22': 'Yes', '23': 'Yes',
    '24': 'Yes', '25': 'Yes', '30': 'Yes', '33': 'Yes',
    '45': 'Yes', '46': 'Yes', '47': 'Yes', '48': 'Yes',
    '55': 'Yes', '56': 'Yes', '65': 'Yes', '66': 'Yes',
    '70': 'Yes', '80': 'Yes', '90': 'Yes',  # Surgery performed, scope unknown
    '99': 'Unknown', 'Blank(s)': 'Unknown'  # Missing/unknown data

Treatment combinations are derived from the three individual treatment
variables (Surgery, Radiation, Chemotherapy). All possible combinations
are captured using np.select() with conditions ordered from most
specific (all three) to least specific (single treatment).

    s & r & c,   # All three treatments
    s & r,       # Surgery + Radiation
    s & c,       # Surgery + Chemotherapy
    r & c,       # Radiation + Chemotherapy
    s,           # Surgery only
    r,           # Radiation only
    c            # Chemotherapy only

    'Surgery+Radiation+Chemotherapy',
    'Surgery+Radiation',
    'Surgery+Chemotherapy',
    'Radiation+Chemotherapy',
    'Surgery',
    'Radiation',
    'Chemotherapy'

The Survival months column is initially stored as an object (text) type.
It is converted to numeric, with invalid or unknown entries coerced to
NaN. Rows with missing survival time are dropped as they cannot be used
in survival analysis.

The vital status variable is encoded as binary numeric values: 0 =
Alive, 1 = Dead. This binary encoding is required for survival analysis
where the event indicator must be numeric.

The median household income variable is stored as a formatted string
range (e.g., '\$70,000 - \$74,999'). Similar to the age transformation,
string parsing is used to extract the lower and upper bounds, and a
numeric midpoint is calculated.

             .str.replace(',', '', regex=False).str.replace('+', '', regex=False)
             .str.replace('<', '', regex=False).str.strip()

After all transformations are complete, the cleaned dataframe is saved
as a CSV file. The Unnamed: 0 index column (if present from previous
saves) is dropped before saving.

3.  Master Script Documentation

After all five cancer datasets are individually cleaned and saved, the
Master.ipynb notebook combines them into a single analytical dataset and
generates cancer-wise Excel files with stage-wise sheets for the
professor's use.

3.1 Combining All Cancer Datasets

The five cleaned CSV files are loaded and combined into a single master
dataframe. Only the 15 analytical columns are loaded (excluding raw SEER
columns that were used during cleaning but are not needed for analysis).

        'Race and origin recode (NHW, NHB, NHAIAN, NHAPI, Hispanic)',
        'Primary Site', 'Histologic Type ICD-O-3', 'Stage', 'Treatment',
        'Survival months', 'Vital status recode (study cutoff used)',
        'COD to site recode', 'Rural-Urban Continuum Code',

        'Prostate_Clean.csv', 'Stomach_Clean.csv']

3.2 Final Dataset Summary

3.3 Cancer-wise Excel Files with Stage Sheets

For each cancer type, a separate Excel file is generated with four
sheets corresponding to cancer stages I, II, III, and IV. Each sheet
contains all patient records for that cancer type and stage.

    'Breast':            'BreastClean.xlsx',
    'Liver':             'LiverClean.xlsx',
    'Lung and Bronchus': 'LungClean.xlsx',
    'Prostate':          'ProstateClean.xlsx',
    'Stomach':           'StomachClean.xlsx',

3.4 Output Files Structure

4.  Known Limitations

5.  Suggested Citation
