# project

## Objectives:

Use public data to explore the significance of “self-reported health” as a health indicator.

## Data Resources:

- **Survey Data**:
  - The 1999-2000 National Health and Nutrition Examination Survey (NHANES):
    ```stata
    import sasxport5 "https://wwwn.cdc.gov/Nchs/Nhanes/1999-2000/DEMO.XPT", clear
    ```

- **Mortality Follow-up Data**:
  - Follow-up mortality data over a 20-year period from the National Center for Health Statistics (NCHS):
     - Health Statistics
        - NCHS
           - Datalinkage
              - Linked Mortality
                 - `NHANES_1999_2000_MORT_2019_PUBLIC.dat`
                 - `Stata_ReadInProgramAllSurveys.do`
                 
                             
```stata
 //data
 global mort_1999_2000 https://ftp.cdc.gov/pub/HEALTH_STATISTICS/NCHS/datalinkage/linked_mortality/NHANES_1999_2000_MORT_2019_PUBLIC.dat

 //code
cat https://ftp.cdc.gov/pub/HEALTH_STATISTICS/NCHS/datalinkage/linked_mortality/Stata_ReadInProgramAllSurveys.do
 ```

### Code Development:

- **Edit and Rename Provided Script**:
  - Download, modify, and upload the provided Stata `.do` file for linking the DEMO.XPT data to mortality follow-up data. Rename this file to `followup.do` and commit it with the description: "Updated DEMO.XPT linkage .do file". In otherwords, download, modify, and upload `Stata_ReadInProgramAllSurveys.do`.

- **Data Merging**:
  - Execute the following Stata code to merge the survey data with the mortality data, ensuring alignment on the unique sequence numbers:
    ```stata
    //use your own username/project repo instead of the class repo below
    global repo "https://github.com/jhustata/intermediate/raw/main/"
    do ${repo}followup.do
    save followup, replace 
    import sasxport5 "https://wwwn.cdc.gov/Nchs/Nhanes/1999-2000/DEMO.XPT", clear
    merge 1:1 seqn using followup
    lookfor follow
    ```
