<center> <h1> Data Model </h1>
*****************************
<center>
![](http://write.flossmanuals.net/openmrs-developers-guide/data-model/static/openmrs_data_model_1.9.0.png)
*OpenMRS data model version 1.9. Details at http://go.openmrs.org/newdev-data*

OpenMRS invests continuous effort into shaping the OpenMRS data model using knowledge and experience gathered from practical experiences from the Regenstrief Institute, Partners in Health, and all of our development partners spread across the world. The core of this data model addresses the who, what, when, where, and how of medical encounters. The core data model is divided into ten basic domains.

* **Concept:** Concepts are defined and used to support strongly coded data throughout the system
* **Encounter:** Captures the interaction between a healthcare provider and patient at a specific location.
* **Form:** A computerized version of a paper form. More specifically, a formatted document with blank fields (i.e. Observations, etc) that users can populate with data.
* **Observation:** Single piece of information recorded about a person at a moment in time.
* **Order:** An action that a healthcare provider requests be taken regarding a patient.
* **Patient:** Specific information about receiving healthcare services as related to a Person in the system.
* **User:** Basic information about the people that use this system.
* **Person:** Basic information about person in the system.
* **Business:** Non-medical data used to administrate OpenMRS
* **Groups/Workflow:** Workflows and Cohort data
However, other domains may also be added to the data model via the use of modules.

## Metadata

[Metadata](https://en.wikipedia.org/wiki/Metadata) is 'data about data'. In OpenMRS, metadata represents system and descriptive data such as data types. Metadata are generally referenced by clinical data, but do not represent any patient-specific data.

##### Significant OpenMRS Metadata Types Include:

1. Drugs
2. EncounterRole
3. EncounterType
4. Concept
5. Form
6. Location
7. Program
8. Role
9. User 

The OpenMRS source code comes with certain metadata included by default. It is recommended that you do not edit/remove these. 

Any request to modify/add metadata should be communicated to the Meta-Data/Terminology lead, who is responsible for the oversight of content required for key functionality of the OpenMRS platform. 