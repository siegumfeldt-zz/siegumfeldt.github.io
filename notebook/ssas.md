# SSAS #

Initialiseres med en Model.bim.

Sæt Default Processing Option til Full, ellers bliver 

## Import af SQL Server-data ##

Data Sources > Import from Data Source... > SQL Server

Impersonation er de credentials, som SSAS-serveren bruger til at genopfriske data med.


## Deployment ##

https://docs.microsoft.com/en-us/sql/analysis-services/tabular-models/tabular-model-solution-deployment-ssas-tabular?view=sql-server-2017

### Direkte fra VS ###

Højreklik på projektet og vælg Deploy.


### Med Deployment.exe ###

Når SSAS-projektet bygges dannes der en .asdatabasefil i bin. Det ser ud til at være bim-filen, bare med et andet navn i "name" end SemanticDatabase.

    $deployment = "C:\Program Files (x86)\Microsoft SQL Server\140\Tools\Binn\ManagementStudio\Microsoft.AnalysisServices.Deployment.exe"
    & $deployment Model.asdatabase /s:current\DeploymentLog.txt


Tool'et kan køres på flere måder:

 - /a (answer): Kør wizarden og dan XML-filer med konfig-info.
 - /s (silent): Deployer og logger til fil. Deployment options mv. findes i de XML-filer, der ligger sammen med .asdatabase-filen
 - /o (output): Som silent, men der dannes et json-script (ligesom Generate Script når man deployer SQL-projekter)


Det ser ud til at være svært at deploye impersonation-info med toolet. Hvis .delpoymentoptions-filen har

    <ProcessingOption>DoNotProcess</ProcessingOption>

så prøver toolet ikke at processe data ved deployment, hvilket også giver en vis mening.

De to filer Model.deploymenttargets og Model.configsettings kan (formodentlig?) tilrettes per miljø, så kun Model.asdatabase skal deployes.




    ....
          "connectionString": "Provider=SQLNCLI11.1;Data Source=localhost;Persist Security Info=True;Trusted_Connection=yes;Initial Catalog=ETU_BI",
          "impersonationMode": "impersonateAccount",
          "account": "GRITLAPTOP02\\SSASServiceUser",
          "annotations": [
            {
              "name": "ConnectionEditUISource",
              "value": "SqlServer"
            }
    ....

