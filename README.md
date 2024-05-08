# project


## Objectives:

1. **Create a Public GitHub Repository**:
   - Set up a repository named `project` on GitHub. You will be working individually, but you are encouraged to use [GitHub Discussions](https://github.com/jhufena/discussions/discussions) to seek help from your peers when needed.

2. **Utilize Publicly Available Data**:
   - The focus will be on using public data to explore the significance of "self-reported health" as a health indicator.

3. **Documentation and Transparency**:
   - Document your project comprehensively using a `README.md` file and other necessary documentation to make your analysis accessible and understandable. Embrace the principles of [Open Science](https://publichealth.jhu.edu/the-r3-center-for-innovation-in-science-education) which are Rigor, Reproducibility, and Responsibility.

## Detailed Steps and Resources:

### 6.1 Data Acquisition and Preparation:

- **Survey Data**:
  - Import the survey data from the 1999-2000 National Health and Nutrition Examination Survey (NHANES):
    ```stata
    import sasxport5 "https://wwwn.cdc.gov/Nchs/Nhanes/1999-2000/DEMO.XPT", clear
    ```

- **Mortality Follow-up Data**:
  - Obtain follow-up mortality data to analyze over a 20-year period from the National Center for Health Statistics (NCHS). Detailed linkage instructions are available on the [Linked Mortality](https://ftp.cdc.gov/pub/) page:
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

### 6.2 Code Development:

- **Edit and Rename Provided Script**:
  - Download, modify, and upload the provided Stata `.do` file for linking the DEMO.XPT data to mortality follow-up data. Rename this file to `followup.do` and commit it with the description: "Updated DEMO.XPT linkage .do file". In otherwords, download, modify, and upload `Stata_ReadInProgramAllSurveys.do`. You may watch the week 6 video for the key items to edit. For instance, you may edit it so that it reads in the data directly from the website.

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
