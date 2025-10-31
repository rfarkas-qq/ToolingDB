# 🗺️ Primary User Flows

This document outlines the intended execution steps for a user.

### Flow 1: Asset Location Overview (Main Screen)
1.  User opens the application and lands on the **Main Dashboard** (`Screens/01-MainDashboard.md`).
2.  User sees a grid of tiles, one for each `LocationType`, with a count of tools in that location.
3.  User clicks the **"Tooling Warehouse"** tile.
4.  Application navigates to the **Warehouse Overview** screen (`Screens/03-WarehouseOverview.md`).
5.  User sees a visual representation of the warehouse shelves, with occupied slots highlighted.

### Flow 2: Finding and Editing a Tool
1.  User is on the **Main Dashboard**.
2.  User clicks the **"🛠️ All Tools"** tile.
3.  Application navigates to a new **Master Tool List** screen (a searchable, filterable table of all `Tools`).
4.  User finds the tool they need (e.g., "KIA-001-A01") and clicks it.
5.  Application navigates to the **Tool Details** screen (`Screens/02-ToolScreen.md`).
6.  User modifies the `Tilt` and `CarModel` parameters and clicks "Save."
7.  The database is updated.

### Flow 3: Configuring the Warehouse
1.  User starts at the **Main Dashboard**.
2.  User clicks the **"Tooling Warehouse"** tile to go to the `WarehouseOverview.md` screen.
3.  On the `WarehouseOverview` screen, the user clicks the **"⚙️ Configure Layout"** button.
4.  Application navigates to the **Warehouse Setup** screen (`Screens/04-WarehouseSetup.md`).
5.  User enters `10` for shelves, `10` for columns, and `5` for rows.
6.  User clicks "Generate." The system deletes all old `WarehouseSlot` records (if empty) and creates 500 new, empty `WarehouseSlot` records (10x10x5).
