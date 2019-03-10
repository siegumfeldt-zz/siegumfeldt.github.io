# Dacpac #


Zipfiler med databaseschemaer i.

Deployes med SQLPackage, som typisk ligger sådan noget som her:

 - "C:\Program Files (x86)\Microsoft SQL Server\140\DAC\bin\SqlPackage.exe"

Deployment af en dacpac med deployment-info i en profil:

    SqlPackage.exe /Action:Publish /SourceFile:current/SQLFlow.Dacpac /Profile:Test.publish.xml