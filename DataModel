# 🗃️ Database Schema & Data Objects

This file defines the core data structure for the ToolingDB.

## Base: `Asset`
*A foundational object that `Tool`, `Carrier`, and `Modificator` will share.*
* `SerialNumber` (string, Primary Key): Unique identifier for any asset.
* `AssetType` (enum: 'Tool', 'Carrier', 'Modificator'): Defines the type of asset.
* `CurrentLocationID` (string, links to `Location.LocationID`): The *current* location of the asset.
* `Status` (enum: 'Available', 'InUse', 'InMaintenance', 'Archived'): The operational status of the asset.

---

## `Location`
*Defines all possible physical or logical locations in the system.*
* `LocationID` (string, Primary Key): A unique ID (e.s., 'WAREHOUSE', 'PROD-LINE-1', 'MAINTENANCE').
* `LocationType` (enum): 'ToolingWarehouse', 'ProductionLine', 'MaintenanceArea', 'EngineeringArea', 'CleaningArea', 'ExternalSupplier', 'ArchiveStorage'.
* `Description` (string): A human-readable name (e.g., "Main Tooling Warehouse", "B-Line Production").

---

## `Tool` (inherits from `Asset`)
*The main foam tool.*
* `SerialNumber` (string, PK): e.g., "KIA-001-A01".
* `OEMPartner` (string): e.g., "KIA", "MER", "VOL".
* `Manufacturer` (string).
* `CarModel` (string): e.g., "Sorento", "C-Class".
* `PictureURL` (string).
* `ReleaseDate` (date).
* `Tilt` (decimal): e.g., 15.5 (in degrees).
* `HasAirbag` (boolean): Yes/No.
* `AutoventsCount` (integer).
* `FinishedGoodPartNumber` (string).
* **Relationships:**
    * `CurrentCarrierID` (string, links to `Carrier.SerialNumber`, nullable): The carrier it is *currently* mounted on.
    * `CurrentModificatorID` (string, links to `Modificator.SerialNumber`, nullable): The modificator *currently* installed.
    * Has-many: `Cavities`.

**Key Logic:**
* If `CurrentCarrierID` is set, the `Tool.CurrentLocationID` MUST be the same as the `Carrier.CurrentLocationID`.

---

## `Carrier` (inherits from `Asset`)
*Holds the tools.*
* `SerialNumber` (string, PK).
* **Relationships:**
    * Has-many: `Tools` (a list of `Tool.SerialNumber`, max 6).

**Key Logic:**
* A `Carrier`'s location dictates the location of *all* tools mounted on it.
* If a user moves a `Carrier` to the 'ProductionLine', all associated `Tools` are automatically moved with it.

---

## `Modificator` (inherits from `Asset`)
*Modifies a tool.*
* `SerialNumber` (string, PK).
* **Relationships:**
    * `CurrentToolID` (string, links to `Tool.SerialNumber`, nullable): The tool it is *currently* installed in.

---

## `Cavity`
*The individual part-producing segments.*
* `SerialNumber` (string, PK).
* `ToolSerialNumber` (string, links to `Tool.SerialNumber`): The parent tool it belongs to.
* `Status` (enum: 'Good', 'NeedsRepair', 'Damaged').

---

## `WarehouseSlot`
*The specific physical spots in the warehouse.*
* `SlotID` (string, PK): A system-generated ID (e.g., 'S1-C1-R1').
* `Shelf` (integer).
* `Column` (integer).
* `Row` (integer).
* `OccupiedByAssetID` (string, links to `Asset.SerialNumber`, nullable): The tool currently in this slot.

**Key Logic:**
* When a `Tool`'s `CurrentLocationID` is set to 'WAREHOUSE', it must also be assigned to a `WarehouseSlot`. The `Slot.OccupiedByAssetID` must be updated.
