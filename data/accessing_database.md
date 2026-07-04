# Comprehensive Guide to Accessing the SEER (Surveillance, Epidemiology, and End Results) Database

The Surveillance, Epidemiology, and End Results (SEER) Program of the National Cancer Institute (NCI) is an authoritative source of information on cancer incidence and survival in the United States. Accessing this database requires following specific procedures to ensure compliance with data use agreements and patient confidentiality.

This guide provides a step-by-step walkthrough on how to request access, obtain credentials, and download the SEER data.

---

## Prerequisites and Requirements

Before beginning the application process, ensure you have the following:
1. **Institutional Affiliation:** A valid email address associated with a research institution, university, government agency, or healthcare organization.
2. **ERA Commons Account or HHS Identity (Optional but recommended):** Can speed up verification, though alternative verification methods are available.
3. **Research Purpose:** A clear intent for using the data (e.g., academic research, epidemiological studies, public health analysis).

---

## Step 1: Determine the Data Type Needed

SEER provides different tiers of data depending on the level of detail required for your research:

* **SEER*Stat Data (Standard):** Includes county-level data, details on primary site, histology, stage, and survival. Requires a standard SEER Data Use Agreement.
* **Specialized Databases:** Includes specialized datasets like SEER-Medicare linked data, SEER-MHOS (Medicare Health Outcomes Survey), or CAHPS. These have separate, more rigorous application processes and often incur fees.
* **Custom Data / Variables:** Certain restricted variables (like specific geographic identifiers below county level) require a specialized custom data request.

*Most researchers start with the standard **SEER\*Stat Data**.*

---

## Step 2: Request a SEER*Stat Account

To access the primary SEER datasets, you must request a SEER*Stat account through the official SEER website.

1. Go to the **[SEER Data Access Request Page](https://seer.cancer.gov/data/access.html)**.
2. Click on **Request Access to SEER Data**.
3. Fill out the registration form with your personal and institutional details.
4. **Data Use Agreement (DUA):** Read and electronically sign the SEER Data Use Agreement. 
   * *Crucial Rule:* You must agree never to attempt to identify any individual patient or disclose proprietary institutional data.

---

## Step 3: Application Review and Approval

* **Timeline:** The SEER administration typically reviews applications within **2 to 5 business days**.
* **Confirmation:** Once approved, you will receive an email containing your **SEER*Stat username** and instructions to set up your password.
* **Validity:** Access must be renewed annually. You will receive an automated email notification when your account is nearing expiration.

---

## Step 4: Software Installation (SEER*Stat)

While some data can be accessed via online query tools, comprehensive analysis requires the SEER*Stat desktop application.

1. Download the SEER*Stat software from the **[SEER*Stat Download Page](https://seer.cancer.gov/seerstat/)**.
2. Install the application on a Windows-based PC (or use a Windows emulator/virtual machine if you are on macOS/Linux).
3. Launch SEER*Stat and enter your approved credentials when prompted.

---

## Step 5: Accessing and Analysing the Data

Once logged into SEER*Stat, you can create various session types depending on your research goals:

1. **Frequency Session:** Count cases matching specific criteria (e.g., number of lung cancer cases in 2020).
2. **Rate Session:** Calculate age-adjusted cancer incidence or mortality rates.
3. **Survival Session:** Compute relative or cause-specific survival rates over time.
4. **Limited-Use Data Download:** If you wish to analyze the raw data using external statistical software (such as R, SAS, or Stata), you can export the data matrix or download binary files directly through the SEER website using your account credentials.

---

## Important Compliance and Citation Notes

When publishing or presenting research that utilizes SEER data, you are strictly required to:
* Acknowledge the SEER Program by including the specific citation provided in your data release documentation.
* Update your data files annually to ensure you are using the most current, corrected versions of the registry data.
* Never share your login credentials or export raw underlying microdata to unauthorized individuals.

***

*Disclaimer: This guide is for informational purposes. Always refer to the official [NCI SEER Website](https://seer.cancer.gov/) for the most up-to-date procedures, legal agreements, and technical documentation.*
