# Fleet Org — MyGeotab Add-in

![Version](https://img.shields.io/badge/version-1.4.0-blue) ![License](https://img.shields.io/badge/license-MIT-green)

A MyGeotab add-in for fleet group management. Visualize your vehicle/group hierarchy, manage group memberships, and analyze device plan distribution — all without leaving MyGeotab.

---

## Features

### Group Hierarchy Panel
- **Treemap view** — ECharts treemap showing all groups sized by vehicle count; click to drill in
- **Tree view** — Collapsible mind-map style hierarchy with vehicle counts per node
- **Breadcrumb navigation** — Click any ancestor to jump up the hierarchy
- **Search** — Find any group by name; highlights and navigates both views
- **Filters** — Hide empty groups, show/hide system groups
- **Full-screen** — Expand the hierarchy panel for large fleet structures
- **Home** — Reset the view to the root group at any time

### KPI Top Bar
- Live counts: **Vehicles**, **Groups**, **Active Devices** — scoped to the selected group
- **Plan pills** — Colored chips showing device plan distribution (e.g. `Pro · 42`, `Suspended · 5`); click a pill to filter the device table

### Device Table
- Lists all vehicles in the selected group (including sub-groups)
- **Columns:** Name, Plate, Odometer (KM), Last Connect, First Connect, Plan, VIN, Serial No., Comment
- **Configurable columns** — Show or hide any column via the ⚙ Columns button; drag to reorder
- **Sorting** — Click any column header to sort ascending or descending
- **Column filters** — Click a cell value to filter by it; clear with ✕
- **Full-text search** — Supports `name=Ford AND plan=Pro OR last<7` syntax
- **Relative dates** toggle — Switch between "3d ago" and exact timestamps
- **Show archived devices** checkbox
- **CSV export** — Download the current filtered view

### Quick Links Bar
Navigate directly to MyGeotab sections scoped to the selected group:

| Button | Destination |
|---|---|
| Map | Live map filtered to group |
| Inventory | Device inventory |
| Dashboard | Performance dashboard |
| Safety | Driver safety scorecard |
| Sustainability | Fuel & CO₂ report |
| Map Devices | Map Devices page |

### Edit Mode
- Lock the current group selection and stage changes before committing
- **Add to Group** — Assign checked devices to any target group
- **Create Group** — Stage a new sub-group under any parent
- **Remove from Group** — Click group badges on device rows to stage removals
- **Delete Group** — Remove an empty leaf group (shown only when applicable)
- **Staged changes panel** — Review all pending adds, removes, creates, and deletes
- **Apply Changes** — Confirm and commit everything in one step

### Bulk Load
Import a CSV or paste a list to assign multiple devices to groups at once.

**Format** (one device per line):
```
serial_or_name,group1,group2,group3
G92721214263,Fleet North,Maintenance
00_Astra,Islandia,PRUEBA_OPS
```

- Matches devices by serial number first, then by name
- Preview shows match status for each device and group before staging
- BOM and extra whitespace are stripped automatically (safe to paste from Excel)
- Staged changes merge into any existing Edit Mode queue

### Other
- **Language selector** — EN / ES / DE dropdown; selection is persisted
- **Preference persistence** — Language, column config, sort order, filters, and display options are saved via the MyGeotab AddInData API
- **Progressive loading** — Step-by-step loading indicator with stage labels
- **Version** — Current add-in version shown in the Help panel (? button)

---

## Installation

### Production

In MyGeotab go to **Administration → Add-ins → Add (`+`)**, paste the contents of [`addin-manifest.json`](https://github.com/gulfuroth/myGeotab-groupsAddin/blob/main/addin-manifest.json) and click **OK**.

```json
{
  "name": "Groups Mgm",
  "supportEmail": "daniel.garciafernandez@telefonica.com",
  "version": "1.0",
  "items": [
    {
      "url": "https://gulfuroth.github.io/myGeotab-groupsAddin/addin/index.html",
      "path": "AdministrationLink/",
      "menuName": {
        "en": "Groups Management",
        "es": "Gestión de Grupos"
      }
    }
  ],
  "isSigned": false
}
```

### Staging / Dev

Use `dev-manifest.json` to install the development build alongside production:

```json
{
  "name": "Groups Mgm [DEV]",
  "supportEmail": "daniel.garciafernandez@telefonica.com",
  "version": "1.0",
  "items": [
    {
      "url": "https://gulfuroth.github.io/myGeotab-groupsAddin/dev/index.html",
      "path": "AdministrationLink/",
      "menuName": {
        "en": "Groups Management [DEV]",
        "es": "Gestión de Grupos [DEV]"
      }
    }
  ],
  "isSigned": false
}
```

---

## Development

```bash
git clone https://github.com/gulfuroth/groups-addin.git
cd groups-addin
npm install
```

### Build

```bash
npm run build
```

Minifies `addin/app.js` (Terser) and `addin/styles.css` (CleanCSS) into `dist/`. The version from `package.json` is injected automatically.

### Deploy

Deployments go to a separate dist repo ([`myGeotab-groupsAddin`](https://github.com/gulfuroth/myGeotab-groupsAddin)) served via GitHub Pages. Configure the path in `.deploy.json` (git-ignored):

```json
{ "distRepo": "../myGeotab-groupsAddin" }
```

| Command | Target | Requirement |
|---|---|---|
| `npm run deploy:dev` | `dev/` directory | Any commit |
| `npm run deploy:prod` | `addin/` directory | Git tag on HEAD |

**Release workflow:**
```bash
# Bump version in package.json, then:
git tag v1.4.0
npm run deploy:prod
```

---

## License

MIT © Daniel García
