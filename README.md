# Medicare Claims, Suicidal Ideation Coding, and River Point Lengths of Stay

This document describes the steps BuzzFeed News took to calculate the rate at which freestanding inpatient psychiatric hospitals included “suicidal ideation” codes in their Medicare claims. It also includes an analysis of lengths of stay for Medicare patients at River Point hospital in Jacksonville, Florida. The analyses provide support for the following passages from the BuzzFeed News article, “[Intake](https://www.buzzfeed.com/rosalindadams/intake),” published December 7, 2016:

> A BuzzFeed News analysis of Medicare claims shows that from at least 2009, UHS hospitals steadily increased the frequency with which they described patients as experiencing suicidal ideation. By 2013, the code for suicidal ideation appeared in more than half of all of the Medicare claims submitted by UHS hospitals. This is four and a half times the rate for all non-UHS psychiatric hospitals. (BuzzFeed News obtained five years of Medicare data from ProPublica, the nonprofit investigative news organization, and a full description of the data analysis is here.)

> In the first full year after UHS bought about 100 hospitals from a competitor, their use of the billing code for suicidal ideation in Medicare claims shot way up — more than sixfold overall.

> [...] Those statistics, UHS said, were simply evidence of more scrupulous attention to proper coding — not of a higher propensity to diagnose suicidal ideation. Internal and external auditors, the company added, “have never identified any improper assignment of the suicidal ideation as a coding designation.”

> More broadly, UHS said, none of its facilities have “received a citation from a regulatory authority alleging that any patient was improperly admitted.”

> [...]

> Eckerd’s effort [at River Point] succeeded. In early 2009, the year she took over as CEO, just 37% of Medicare patients stayed for 10 days or more. By early 2010, the year UHS bought the hospital, that rate had almost doubled to more than 70%. UHS kept Eckerd on to lead the facility, and the rate stayed high for years.  Asked about that increase, Johnson, the UHS vice president of clinical services, said that River Point was “providing care that’s necessary for the patients.”

> In response to questions about River Point’s operations, UHS’s Hudson, who oversaw Eckerd, told BuzzFeed News that all UHS’s hospitals “have a responsibility to the safety of their communities” and “we do that very well at our hospitals and River Point does it very well.”

> “Eckerd knew that medical research shows that short stays are associated with high readmission and suicide rates so she established a 10-day guideline with the goal of providing patients with the medically necessary care they needed,” UHS said in its statement to BuzzFeed News. It added this was not a one-size-fits-all requirement.

## Table of Contents

- [Data Sources](#data-sources)
- [Data Processing](#data-processing)
- [Suicidal Ideation Analysis](#suicidal-ideation-analysis)
- [River Point Analysis](#river-point-analysis)
- [Findings](#findings)

## Data Sources 

These analyses depend on three main sources of data:

- Medicare billing claims. BuzzFeed News obtained, through a data-sharing agreement with [ProPublica](https://www.propublica.org/), Medicare claim data from the Centers for Medicare & Medicaid Services for the years 2009–2013.  Specifically, we used [Medicare’s Limited Data Set files](https://www.cms.gov/Research-Statistics-Data-and-Systems/Files-for-Order/LimitedDataSets/).  Due to the sensitivity of these files, CMS prohibits users from republishing the raw data, any patient-identifying information, or any aggregate statistics that refer to 10 or fewer people.

- Hospital ownership, from the American Hospital Directory. The [AHD](https://www.ahd.com/) classifies hospitals into three broad categories of ownership: government, proprietary/for-profit, and nonprofit.

- Universal Health Services ownership, acquisition, and sale information. BuzzFeed News identified which of the hospitals had, at any point been owned by UHS, and identified the date of establishment/purchase and date of closure/sale, where relevant.  BuzzFeed News also identified which hospitals had been transferred to UHS ownership after the company acquired Psychiatric Solutions (PSI).

## Data Processing 

### Identifying claims from freestanding inpatient psychiatric hospitals 

Freestanding inpatient psychiatric hospitals can be identified by their CMS Certification Number. For such hospitals, the third through sixth characters of that identifier will fall between “4000” and “4499.” For example: The certification number for River Point Behavioral Health, a freestanding inpatient psychiatric hospital, is 104016.  Counterexample: Massachusetts General Hospital’s — which is not a freestanding inpatient psychiatric hospital — has certification number 220071.

BuzzFeed News identified 867,070 claims from 550 such providers between 2009 and 2013.

### Restructuring raw data 

BuzzFeed News used the [Standard Analytic Files](https://www.cms.gov/Research-Statistics-Data-and-Systems/Files-for-Order/LimitedDataSets/StandardAnalyticalFiles.html) from Medicare’s “[Limited Data Set](https://www.cms.gov/Research-Statistics-Data-and-Systems/Files-for-Order/LimitedDataSets/).” (The “limited” refers to the fact that files “have been stripped of data elements that might permit identification of beneficiaries.”) This dataset comes in a “wide” format; each row corresponds to a single billing claim (or a segment of a claim; more on that below), with several groups of repeating columns. For example, each row in the 2013 data contains 25 columns for diagnoses: DGNSCD1, DGNSCD2, DGNSCD3, and so on. To make the data easier to analyze, BuzzFeed News converted these “wide” column groups into separate, “long” tables.

A provider can file multiple claims for a single hospital stay. BuzzFeed News identified claims belonging to the same stay by comparing the provider’s CMS Certification Number, the patient’s numeric identifier, and the admission date. BuzzFeed News identified 822,749 such stays in the data, 812,350 of which corresponded to stays for which the patient had been discharged. (The Medicare dataset also includes claims for patients who, at the time of data submission, had not yet been discharged.)


## Suicidal Ideation Analysis 

### Identifying “Suicidal Ideation” 

In Medicare’s ICD-9 diagnosis codes, [V6284](http://www.hipaaspace.com/Medical_Billing/Coding/ICD-9/Diagnosis/V6284) [stands](http://www.hipaaspace.com/Medical_Billing/Coding/ICD-9/Diagnosis/V6284)[ “suicidal ideation”](http://www.hipaaspace.com/Medical_Billing/Coding/ICD-9/Diagnosis/V6284).  BuzzFeed News identified all claims, and associated hospital stays/discharges, that included a V6284 diagnosis.

### Hospital types 

BuzzFeed News grouped all hospital discharges into four main ownership categories:

- UHS hospitals, excluding those acquired through the purchase of Psychiatric Solutions
- UHS hospitals acquired from Psychiatric Solutions
- Psychiatric Solutions hospitals before UHS acquisition
- All other for-profit hospitals
- Non-profit hospitals
- Government-run hospitals

BuzzFeed News then compared the rates of “suicidal ideation” diagnoses (per inpatient hospital stay) across each hospital type, and over time.

### Checking the analysis within the “psychoses” diagnoses category 

Medicare categorizes all inpatient stays according to its [“Diagnosis Related Group” (DRG) classification system](https://www.hipaaspace.com/Medical.Coding.Library/DRGs). Of all Medicare-billed stays at UHS’s freestanding inpatient psychiatric hospitals, 75% were categorized in the “psychoses” group, DRG 885. (The next most common group was DRG 897 — "alcohol/drug abuse or dependence w/o rehabilitation therapy w/o [major complication or comorbidity].") To double-check the first analysis and test whether the differences were driven by differing proportions of illnesses, BuzzFeed News repeated the analysis with only claims classified as DRG 885.

## River Point Analysis

The analysis of Medicare patients' lengths of stay at River Point is simply based on the discharge date and the length of stay (in days) for each Medicare discharge at the hospital.

## Findings

The findings, and the code used to produce them, can be [found here](notebooks/medicare-claims-analysis.ipynb).

## Questions / Comments?

Please contact Jeremy Singer-Vine at jeremy.singer-vine@buzzfeed.com.

Looking for more from BuzzFeed News? [Click here for a list of our open-sourced projects, data, and code](https://github.com/BuzzFeedNews/everything).
