# Notion CSV Exporter

This is a simple tool to export data from a Notion database into a CSV file using the Notion API.

## Features
- Exports data from a specified Notion database to a CSV file.
- Supports customization of Notion API tokens and database IDs via command line arguments.
- Supports sorting by a specified key in ascending or descending order.
- **Allows selecting specific columns to export** using a comma-separated list.
- **Validates column names**, ensuring that only existing columns are included in the export.
- **Supports fetching relation page names** instead of just page IDs for relation properties.

## Requirements
Before you start, make sure you have:
- A valid Notion Integration Token
- The Notion Database ID that you want to export
- Go installed on your machine

## Installation
You can install `notion-csv-exporter` using `go install`:

```sh
go install github.com/yudppp/notion-csv-exporter/cmd/notion-csv-exporter@latest
```

This will download and build the tool, placing the binary in your `$GOBIN` directory (by default `$HOME/go/bin`).

If you want to install a specific version, you can use a tagged version like this:

```sh
go install github.com/yudppp/notion-csv-exporter/cmd/notion-csv-exporter@v1.0.0
```

Make sure your `$GOBIN` is added to your system's `$PATH`, so you can run the tool from anywhere in your terminal.

## Usage
Once installed, you can use the tool from anywhere in your terminal:

```sh
notion-csv-exporter -token={NOTION_API_TOKEN} -databaseID={NOTION_DATABASE_ID} [-sortKey={SORT_KEY}] [-order={ascending|descending}] [-columns={COLUMN1,COLUMN2,...}] [-fetchRelationNames={true|false}]
```

Replace:
- `{NOTION_API_TOKEN}` with your Notion API token.
- `{NOTION_DATABASE_ID}` with your database ID.
- `{SORT_KEY}` with the key to sort by (optional).
- `{ascending|descending}` with the sorting order (default is descending).
- `{COLUMN1,COLUMN2,...}` with a comma-separated list of column names to export (optional).
- `{true|false}` to enable or disable fetching relation names instead of page IDs (default is false).

### Example
#### Export all columns
```sh
notion-csv-exporter -token=secret_abc12345 -databaseID=1234567890abcdef1234567890abcdef
```
This command exports all columns from the specified Notion database.

#### Export specific columns
```sh
notion-csv-exporter -token=secret_abc12345 -databaseID=1234567890abcdef1234567890abcdef -columns=Name,Email,Status
```
This command exports only the `Name`, `Email`, and `Status` columns from the specified Notion database.

#### Export with sorting
```sh
notion-csv-exporter -token=secret_abc12345 -databaseID=1234567890abcdef1234567890abcdef -sortKey=Name -order=ascending
```
This command sorts the exported data by the `Name` column in ascending order.

#### Export with relation names
```sh
notion-csv-exporter -token=secret_abc12345 -databaseID=1234567890abcdef1234567890abcdef -fetchRelationNames=true
```
This command exports data with relation properties showing the related page names instead of just page IDs.

## Column Selection and Validation
- If `-columns` is specified, **only those columns will be included in the output**.
- If a column name does not exist in the Notion database, **the export will fail with an error**.

## Relation Properties
- By default, relation properties are exported as page IDs.
- When `-fetchRelationNames=true` is specified, the exporter will fetch the title of each related page.

## How to Get Notion API Token and Database ID

### API Token
1. Go to [Notion Integrations](https://www.notion.so/my-integrations).
2. Create a new integration.
3. Copy the "Internal Integration Token."

### Database ID
1. Open the Notion database in your browser.
2. The database ID is the part of the URL between `/` and `?` or the last part after `/` if there is no query string.

## Development
Before starting development, run the following command:

```sh
make setup
```

This command will:
- Install lefthook for pre-commit hooks to prevent accidental commits of sensitive files

### Pre-commit Hooks
This project uses [lefthook](https://github.com/evilmartians/lefthook) to manage Git hooks. The pre-commit hooks help prevent accidental commits of sensitive files.

## License
This project is licensed under the MIT License. See the LICENSE file for details.
