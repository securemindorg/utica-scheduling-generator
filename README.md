# WARNING - This tool is not finished

---

# Academic Course Scheduler & Banner Exporter

A lightweight, single-page web application designed for academic departments to manage course offerings, faculty rosters, classroom assignments, and enrollment capacities (**Max Seats**). It features customizable time blocks and exports directly to the **Banner Schedule Roll Template (`output.csv`)** format.

---

## Key Features

###  Updated Default Timeslots & Customization

Pre-configured with standard institutional meeting patterns, with full flexibility to add, edit, or delete timeslots dynamically:

* **Monday Wednesday Friday (MWF) [50-minute blocks]:**
* `8:30 - 9:20`
* `9:30 - 10:20`
* `10:30 - 11:20`
* `11:30 - 12:20`


* **Monday Friday (MF) [75-minute blocks]:**
* `12:30 - 1:45`
* `2:00 - 3:15`
* `3:30 - 4:45`


* **Tuesday Thursday (TR) [75-minute blocks]:**
* `8:30 - 9:45`
* `10:00 - 11:15`
* `11:30 - 12:45`
* `1:00 - 2:15`
* `2:30 - 3:45`
* `4:00 - 5:15`



### Faculty Roster & Excel/CSV Import

* **Bulk File Import:** Upload spreadsheets containing faculty records (e.g., `Faculty Banner IDs - Spring 2027.xlsx` or custom `.csv` files with `BANNER ID`, `LAST NAME`, and `FIRST NAME`).
* **Manual Course Load Management:** Easily set and update individual maximum course loads per professor.

### Max Seats & Modality Management

* **Enrollment Capacity Control:** Set section capacities (`Max Seats`) per course.
* **Multi-Modality Support:** Seamlessly handles On-Ground (`GRND`) and Distance/Online (`DIST`) offerings.

### Automated Conflict-Free Scheduler

* Auto-assigns available classrooms and default timeslots based on room seating capacities and instructor course caps.

### Standard Banner Export (`output.csv`)

* Generates an exact **43-column Banner Schedule Roll Template** export matching official registrar templates (`SYRCRLT Schedule Roll Template, 202710`).
* Converts time ranges into standard 12-hour Banner format (e.g., `11:30AM`, `12:45PM`).
* Leaves the **`Fees`** column blank (for downstream processing) along with unassigned/optional fields.

---

## File Structure

```text
.
├── index.html                           # Main Web Application (UI, State Engine, CSV Exporter)
├── Faculty Banner IDs - Spring 2027.xlsx# (Optional) Faculty Banner ID source file
├── output.csv                           # Reference/Target Banner Roll Template file
└── README.md                            # System documentation

```

---

## Quick Start Guide

### Prerequisites

No local build steps, Node.js, or backend servers are required. The tool runs directly in any modern browser using client-side libraries via CDN:

* **Tailwind CSS** (Styling & Responsive UI)
* **FontAwesome** (Icons)
* **SheetJS / XLSX** (Excel `.xlsx`/`.xls` and `.csv` parsing)

### Running the App

1. Save `index.html` on your machine.
2. Double-click or open `index.html` in Chrome, Firefox, Edge, or Safari.

### Recommended Workflow

1. **Faculty Import:** Go to the **Faculty Roster** tab $\rightarrow$ Click **Import Excel / CSV** $\rightarrow$ Upload your faculty list spreadsheet $\rightarrow$ Adjust each professor's **Max Course Load**.
2. **Course Setup:** Go to the **Course Catalog** tab $\rightarrow$ Define course numbers, titles, sections, modalities, and **Max Seats**.
3. **Classrooms & Timeslots:** Adjust available rooms or customize timeslot blocks under their respective tabs.
4. **Schedule Generation:** Click **Generate Schedule** (top right) to automatically allocate non-conflicting timeslots and classrooms.
5. **Banner Export:** Click **Export Banner output.csv** to download your fully formatted schedule roll template.

---

## Banner Output Format Mapping

| Column Index | Banner Field Name | Sample Value | Notes |
| --- | --- | --- | --- |
| **0** | `School` | `Business and Justice Studies` | Default department school |
| **2** | `CRN` | `5236` | Course Reference Number |
| **5–7** | `Subj` / `Crse#` / `Section` | `CYB` / `101` / `A` | Subject code & section ID |
| **8** | `Instructor (Primary marked...)` | `Aaronson, Lawrence*` | Formatted primary instructor |
| **10–11** | `Campus` / `Sched Type` | `U` / `A` *(On-Ground)* or `D` / `Z` *(Online)* | Banner modality parameters |
| **22** | `Fees` | *(Blank)* | Kept empty per specifications |
| **23** | `Max Seats` | `25` | Section enrollment cap |
| **34–36** | `Meet Days` / `Begin` / `End` | `TR` / `11:30AM` / `12:45PM` | Formatted meeting times |
| **37** | `Meet Building and Room` | `ECJS214` or `ONLINE` | Classroom location |
| **41–42** | `Modality(Attribute)` / `(Title)` | `GRND` / `(OG)` or `DIST` / `(OL)` | Modality codes |

---

## Customization & Maintenance

* **Adding Timeslots:** Navigate to the **Timeslots** tab, select a day pattern (`MWF`, `MF`, `TR`, or single days), enter start/end times in 24-hour format, and save.
* **Editing Data:** All course, classroom, and faculty entries can be edited inline or via pop-up modals at any point.
