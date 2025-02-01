# Notion CSV Exporter

This is a simple tool to export data from a Notion database into a CSV file using the Notion API.

## Features
- Exports data from a specified Notion database to a CSV file.
- Supports customization of Notion API tokens and database IDs via command line arguments.
- Supports sorting by a specified key in ascending or descending order.

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
notion-csv-exporter -token={NOTION_API_TOKEN} -databaseID={NOTION_DATABASE_ID} [-sortKey={SORT_KEY}] [-order={ascending|descending}]
```

Replace `{NOTION_API_TOKEN}` with your Notion API token, `{NOTION_DATABASE_ID}` with your database ID, `{SORT_KEY}` with the key to sort by (optional), and `{ascending|descending}` with the sorting order (default is descending).

### Example
Here’s an example command to export data:

```sh
notion-csv-exporter -token=secret_abc12345 -databaseID=1234567890abcdef1234567890abcdef -sortKey=Name -order=ascending
```

This command will export the contents of the specified Notion database to a CSV file named `output.csv` in the current directory, sorted by the `Name` column in ascending order.

## How to Get Notion API Token and Database ID

### API Token
1. Go to Notion Integrations.
2. Create a new integration.
3. Copy the "Internal Integration Token."

### Database ID
1. Open the Notion database in your browser.
2. The database ID is the part of the URL between `/` and `?` or the last part after `/` if there is no query string.

## License
This project is licensed under the MIT License. See the LICENSE file for details.
