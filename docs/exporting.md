# Exporting notes

Scene Notes can export your notes to CSV for use in project management tools, spreadsheets, or task trackers.

## CSV export

### Exporting from the editor

1. Open the Scene Notes Manager window
2. Click the Export CSV button
3. The CSV file is saved to the path configured in settings (default: `SceneNotes_Export.csv` in the project root)
4. A confirmation message appears with the file path

### CSV format

The exported CSV contains these columns:

| Column | Description |
|--------|-------------|
| Type | The note type name (Critical, Bug, Todo, etc.) |
| Description | The full note description text |
| Author | The name of the person who created the note |
| Date | Creation date and time |
| Scene | The Unity scene the note belongs to |
| Position X | World X coordinate |
| Position Y | World Y coordinate |
| Position Z | World Z coordinate |
| Resolved | True or False |

### Example CSV output

```
Type,Description,Author,Date,Scene,Position X,Position Y,Position Z,Resolved
Critical,Player falls through floor,-12.4,Chris,2026-03-29 14:14,Level_01,0.0,33.7,False
Bug,Enemy AI stuck on doorframe,Chris,2026-03-29 14:18,Level_01,5.1,1.2,-8.3,False
Todo,Add particle FX to waterfall,Chris,2026-03-29 14:30,Level_01,72.6,8.0,-1.4,False
```

### Using with project management tools

The CSV format is compatible with most project management tools:

Trello — Use Trello's CSV import feature or a third-party tool like Coda to create cards from the exported file. Each note becomes a card with the description as the title and the position, scene, and author in the card description.

Jira — Use Jira's CSV import to create issues. Map the Type column to Jira priority or issue type, and the Description column to the issue summary.

GitHub Issues — Use a CSV-to-GitHub-Issues tool or script to batch-create issues from the export.

Notion — Import the CSV as a Notion database. Each note becomes a row with sortable and filterable properties.

Google Sheets / Excel — Open the CSV directly for manual review and tracking.

## Filtering before export

The CSV export respects the current filters in the Scene Notes Manager. If you have filtered to show only Critical notes, only those notes will be exported.

To export all notes, make sure all type filters are active and the resolved filter is set to show all.

## Export scope

The CSV export includes notes from the currently active scene only. To export notes across all scenes, switch to each scene and export separately, or combine the CSV files manually.

## JSON export (builds)

Notes from standalone builds are automatically saved as JSON files. See [Standalone builds](build-workflow.md) for details on the JSON format and import workflow.
