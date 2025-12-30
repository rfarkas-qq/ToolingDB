
[//]: # (Hand written initial app description)

# ToolingDB

Application is professional tool like Maximo to maintain company production assets. Specifically this is about foam tools which are used to produce foam parts. 

**Project Goal:** To create a professional asset management application, similar to Maximo, for tracking and maintaining foam tools used in production.

This application will provide a clean, intuitive, and reliable interface for managing the location, status, and parameters of all core production assets.

**Core Assets to Track:**
* **Tools:** The primary foam tools used to create parts.
* **Carriers:** Mounts that hold 1-6 tools for use on the production line.
* **Modificators:** Inserts that alter a tool to produce a different part.
* **Cavities:** The individual part-forming sections within a tool.

## Description of subjects
Foam tools are heavy big devices, 2m x 1,5m x 1m, made from aluminium. Foam tools are mounted onto carrier to be used on production line. 
There can be from 1 up to 6 tools mounted on one carrier.
Each tool can have multiple cavities, where each cavity will produce one foam part during production.
Some tools can be used with modificator. Modificators are mounted into tool and with that they are able to produce different part.
Each carrier, tool, modificator, cavity has its own serial number.

## Tools location
Tools can be located at:
- tooling warehouse
- production line - mounted on carrier
- maintenance area - mounted on carrier or alone
- engineering area - mounted on carrier or alone
- cleaning area - mounted on carrier
- external supplier for special treatment - alone, without carrier
- archive storage for not active parts - alone, without carrier

## Carriers location
Carriers are stored in carriers warehouse. Carrier can be empty or with mounted tools. Carriers locations:
- carriers warehouse
- production line - with tools mounted 
- maintenance area - with tools mounted or alone
- engineering area - with tools mounted or alone
- cleaning area - mounted on carrier


Lets start with main screen in Maximo style.
There will be tiles showing amount of tools on every location.
By clicking on tile, subpage will be opened with specific actions available for each location. Now generate only main screen and tiles.

## Tool
Foam tool has its own screen to modify parameters.
Parameters are:
- serial number of the tool
- OEM partner
- manufacturer
- car model
- picture of tool 
- release date
- tilt [in degrees]
- airbag [yes/no]
- autovents [number of autovents]
- part number of finished goods

create dedicate tile to modify all tools attributes
attached is example of the tool

## Tooling warehouse
Tool serial number is made of 10 alphanumerical characters. First 3 are abbreviation of OEM car maker like KIA for Kia, MER for Mercedes, VOL for Volvo and so on.  
Warehouse of tools is organised in shelves. 
Prepare warehouse setup page. There will be definition of warehouse.
Warehouse setup is subpage of warehouse tile.
There are typically 10 shelves in tooling warehouse.
Each shelve has typically 10 columns and 5 rows.
Main page of Tooling warehouse will show shelves and tool within shelves,
