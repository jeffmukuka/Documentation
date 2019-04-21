---
uid: population_synthesis_1_6
---

# Population Synthesis

## Overview

GTAModelV4 has a population synthesized from the TTS (Transportation for Tomorrow Survey) records.

### Required Software and Dependencies

1. MySql Server 5.5 or greater
2. Python V3 or greater with required package dependencies dependencies

### Installation and Setup

#### Mysql Server Installation

If you do not have a copy of MySQL Server - an installer is available for download at <https://dev.mysql.com/downloads/mysql/.> A minimum version of version 5.5 of the Community Edition is required.

During the installation process, keep note of the server isntallation's root password that you provide. A valid database user and password is required is required to connect to the database server.

##### Server Configuration

It may be necessary to increase the size of the `max_allowed_packet` property before running the server. This property can be set in the server's configuration file. On Windows, the default property file loaded is `my.ini`, located in the root of the server installation directory. 

> [!NOTE]
> For more information about this server variable, please see the MySql documentation at <https://dev.mysql.com/doc/refman/5.5/en/server-system-variables.html#sysvar_max_allowed_packet.>


##### Creating a Database

Apart from the MySQL Server installation, a database must be created with the proper access privileges for the user account used to connect to the server.

(TODO)





#### Python Installation


##### Installing Package Dependencies

#### Input Configuration

GTAModel's population synthesis procedure requires defining its inputs through a JSON formatted configuration file. A blank / schema version of the required input format is provided for guidance in creating the properly structured input.

The default configuration JSON has the following format:

```json
{
	"DatabaseName": "",
	"DatabasePassword": "",
	"DatabaseUser": "",
	"DatabaseServer": "",
	"PersonsSeedFile": "",
    "HouseholdsSeedFile": "",
    "OutputFolder": "",
	"MazLevelControls": "",
	"TazLevelControls": "",
	"MetaLevelControls": "",
	"Java64Path": "C:\\Path\\To\\Jre",
	"PopSyn3SettingsFile": "runtime\\config\\settings.xml",
	"CategoryMapping": {
		"Persons": [
			{
				"FieldName": "",
				"FieldValue": "",
				"MappedValue": 0
			}
		],
		"Households": [
			{
				"FieldName": "",
				"FieldValue": "",
				"MappedValue": 0
			}
		]
	}
}
```

| Configuration Value |                                                                                                          Description                                                                                                          |
| ------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| DatabaseName        | The database name to be used during the population synthesis procedure.                                                                                                                                                       |
| DatabasePassword    | The password to be used to connect to the database.                                                                                                                                                                           |
| DatabaseUser        | The user account to be used to connect to the database.                                                                                                                                                                       |
| DatabaseServer      | The IP address or host name of the database server.                                                                                                                                                                           |
| PersonsSeedFile     | File path to the persons seed data to be used. This file is expected to be in CSV format.                                                                                                                                     |
| HouseholdsSeedFile  | File path to the households seed data to be used. This file is expected to be in CSV format.                                                                                                                                  |
| OutputFolder        | Path to the folder where all output files will be written, including log files.                                                                                                                                               |
| MazLevelControls    | Input file path specifying control totals at MAZ level of geography. This file is autogenerated as part of the preconfiguration setup.                                                                                        |
| TazLevelControls    | Input file path specifying control totals at TAZ level of geography. This file is autogenerated as part of the preconfiguration setup.                                                                                        |
| MetaLevelControls   | Input file path specifying control totals at the META or regional level of geography. This file is autogenerated as part of the preconfiguration setup.                                                                       |
| Java64Path          | Path location of an available JRE installation. There is no need to specify the installation bin folder, only the base path of the installation.                                                                              |
| PopSyn3SettingsFile | File location of the settings configuration file used by PopSyn3. This is an XML document that is transformed to include configuration values specified in config.json alongside other PopSyn3 specific configuration values. |
| Category Mapping    | Contains a list of mapping values for households and persons that transforms input attributes from a character value to an integer mapping                                                                                    |

## Population Synthesis Procedure

### Pre-processing Input Data

### Starting a Run

After the required input configuration has been finalized, the population synthesis procedure can be run. The file `run.py` is the main python script that begins the synthesis procedure. These steps involve reading the input data and configuration settings. This information is then used to create and process the required database tables used by PopSyn3.

> [!NOTE]
> Please ensure that your MySQL server is started before starting the synthesis procedure.

## Post-Processing

### Output Files

After the population synthesis procedure has completed, the synthesized population will be written to the output folder specified in the configuration settings.

#### Population Files

##### Households


##### Persons

##### Zonal Residence

##### Employment and Occupation Vectors


#### Log Files

Logginging information from different stages of execution are appended to several different log files in the output directory:
    1. event.log - Output from PopSyn3
    2. post-process.log - Output from the post process stage of execution.
    3. pre-process.log - Output from the pre-process stage of execution.
    4. run.log - Output during execution, which contains a mix of GTAModel specific information alongside PopSyn3 output information.