# Stored Procedure Generator Feature..

This jar file generates the stored procedure from the given insertupdate.xml or *.sql file.

## Getting Started
Download the jar file and run the following command in command prompt to generate the stored procedure sql.

### Running the jar
````
    > java - jar <<jarfilename.jar>> --fileName="E:\xyz\.sample files\insertupdate.xml" --procedureName=V11.40.25 --versionFrom=V11.40.25
````

### Application Parameters

|Argument   | Description |Type | Use  |
|-----------|--------------|-----|------|
|--fileName | Give the location of file that needs to be parsed for generating the sp.|Required| --fileName="E:\xyz\.sample files\insertupdate.xml" |
|--versionFrom | In case of insertupdate.xml, version starting from this will be added to stored procedure.|Required |--versionFrom=V11.40.25 |
|--procedureName | Generated procedure name will be with format "User_SP_Adhoc_`ParameterValue`_randomnumber. | Required |--procedureName=V11.40.25 |
|--callbackUrl | After completion of the application, it will post the message to the url specified with the status and message parameters. | Optional |--callbackUrl="https://myUrlToPost.com/xyz" |
|--practiceDatabaseName | By default, application will generate the sp to run for db_test database. You can specify the value to change the database. | Optional |--practiceDatabaseName=db_myprac |


### Current Limitation
No limitations currently

~~Current version of the application is not able to parse the Alter table queries with column options.~~
~~For example below query will fail as it has `, COLUMN [cms_quality_id]; `, if we remove it then it should work.~~

~~However, it is because of the vendor jar bug which they have resolved in future release.~~


~~Example: ALTER TABLE mips_measure_detail DROP CONSTRAINT DF_mips_measure_detail_cms_quality_id, COLUMN [cms_quality_id];~~


### Application internal workings
Step 1. Reading the queries from file and give it to the sql parser (gsp.jar)

Step 2. Iterating through individual queries and parsing them.

Step 3. Generating the output files.

* In case of any exception in step1, it will be logged in application.log file and process will be terminated.
* In case of exceptions in step2, failed_xxxx.log file will be generated with the list of queries failing to parse.
* In case of successful parsing the queries, `procedurename.sql` file will be generated.

###

###
> Reference for installing the maven dependency for gudusoft (Not needed for running the code)
>
>
>mvn install:install-file -Dfile=E:\xyz\stored-procedure-generator\external_lib\gudusoft\gsqlparser\1.0.0\gsqlparser-1.0.0.jar -DgroupId=gudusoft -DartifactId=gsqlparser -Dversion=1.0.0 -Dpackaging=jar

### Change Logs
April 2020
* Skipped few tables for duplicate value validation because they required duplication.
    "clinicianallergies" , "interfaceInboundSpecialCharToReplace", "pdmp_hub_config"
