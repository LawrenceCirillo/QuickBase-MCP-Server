# QuickBase MCP Server

A Model Context Protocol (MCP) server that provides maximum flexibility for QuickBase operations. This server allows you to create tables, add fields, modify relationships, and perform all QuickBase operations through MCP tools.

<a href="https://glama.ai/mcp/servers/@LawrenceCirillo/QuickBase-MCP-Server">
  <img width="380" height="200" src="https://glama.ai/mcp/servers/@LawrenceCirillo/QuickBase-MCP-Server/badge" alt="QuickBase Server MCP server" />
</a>

## Features

### Application Management
- Get application information
- List all tables
- Test connection

### Table Operations
- Create new tables
- Get table information
- Update table properties
- Delete tables

### Field Management
- Get all fields for a table
- Create new fields (all types supported)
- Update existing fields
- Delete fields
- Support for lookups, formulas, relationships

### Record Operations
- Query records with filtering and sorting
- Get specific records
- Create single or multiple records
- Update existing records
- Delete records
- Search records by text
- Bulk operations

### Relationship Management
- Create parent-child relationships
- Get existing relationships
- Foreign key management

### Utility Functions
- Get and run reports
- Advanced querying capabilities
- Error handling and retry logic

## Installation

1. **Clone and setup the server:**
```bash
cd quickbase-mcp-server
npm install
```

2. **Copy environment configuration:**
```bash
cp env.example .env
```

3. **Configure your QuickBase credentials in `.env`:**
```bash
# QuickBase Configuration
QB_REALM=seanngates.quickbase.com
QB_USER_TOKEN=your_quickbase_user_token_here
QB_APP_ID=btr3r3fk5

# Optional: Default settings
QB_DEFAULT_TIMEOUT=30000
QB_MAX_RETRIES=3

# MCP Server Configuration
MCP_SERVER_NAME=quickbase-mcp
MCP_SERVER_VERSION=1.0.0
```

4. **Build the project:**
```bash
npm run build
```

## Getting Your QuickBase User Token

1. Go to QuickBase → My Apps → User Account
2. Click "Manage user tokens"
3. Click "New user token"
4. Give it a name like "MCP Server"
5. Set appropriate permissions
6. Copy the token to your `.env` file

## Usage

### Run the server standalone:
```bash
npm start
```

### Add to your MCP client configuration:

Add to your MCP client configuration (e.g., Claude Desktop):

```json
{
  "mcpServers": {
    "quickbase": {
      "command": "node",
      "args": ["/path/to/quickbase-mcp-server/dist/index.js"],
      "env": {
        "QB_REALM": "seanngates.quickbase.com",
        "QB_USER_TOKEN": "your_token_here",
        "QB_APP_ID": "btr3r3fk5"
      }
    }
  }
}
```

## Available Tools

### Application Tools
- `quickbase_get_app_info` - Get application information
- `quickbase_get_tables` - List all tables
- `quickbase_test_connection` - Test connection

### Table Tools
- `quickbase_create_table` - Create new table
- `quickbase_get_table_info` - Get table details
- `quickbase_delete_table` - Delete table

### Field Tools
- `quickbase_get_table_fields` - Get all fields
- `quickbase_create_field` - Create new field
- `quickbase_update_field` - Update existing field
- `quickbase_delete_field` - Delete field

### Record Tools
- `quickbase_query_records` - Query with filters/sorting
- `quickbase_get_record` - Get specific record
- `quickbase_create_record` - Create new record
- `quickbase_update_record` - Update existing record
- `quickbase_delete_record` - Delete record
- `quickbase_bulk_create_records` - Create multiple records
- `quickbase_search_records` - Search by text

### Relationship Tools
- `quickbase_create_relationship` - Create table relationship
- `quickbase_get_relationships` - Get existing relationships

### Utility Tools
- `quickbase_get_reports` - Get all reports
- `quickbase_run_report` - Run specific report

## Example Usage

### Create a new table:
```json
{
  "name": "quickbase_create_table",
  "arguments": {
    "name": "New Projects",
    "description": "Project tracking table"
  }
}
```

### Add a field to a table:
```json
{
  "name": "quickbase_create_field",
  "arguments": {
    "tableId": "bu65pc8px",
    "label": "Project Status",
    "fieldType": "text_choice",
    "choices": ["Planning", "Active", "Complete", "On Hold"],
    "required": true
  }
}
```

### Query records with filtering:
```json
{
  "name": "quickbase_query_records",
  "arguments": {
    "tableId": "bu65pc8px",
    "where": "{6.EX.'John'}",
    "top": 10,
    "sortBy": [{"fieldId": 3, "order": "DESC"}]
  }
}
```

### Create a new record:
```json
{
  "name": "quickbase_create_record",
  "arguments": {
    "tableId": "bu65pc8px",
    "fields": {
      "6": {"value": "John Doe"},
      "7": {"value": "123 Main St"},
      "8": {"value": "john@example.com"}
    }
  }
}
```

## Field Types Supported

- `text` - Single line text
- `text_choice` - Single choice dropdown
- `text_multiline` - Multi-line text
- `richtext` - Rich text editor
- `numeric` - Number field
- `currency` - Currency field
- `percent` - Percentage field
- `date` - Date field
- `datetime` - Date/time field
- `checkbox` - Checkbox field
- `email` - Email field
- `phone` - Phone number field
- `url` - URL field
- `address` - Address field
- `file` - File attachment
- `lookup` - Lookup from another table
- `formula` - Calculated field
- `reference` - Table reference

## Development

### Run in development mode:
```bash
npm run dev
```

### Run tests:
```bash
npm test
```

## Troubleshooting

### Common Issues

1. **Authentication Error**
   - Check your user token is correct
   - Verify token permissions include your app
   - Ensure realm hostname is correct

2. **Table/Field Not Found**
   - Verify table/field IDs are correct
   - Check if you have permissions to access

3. **Field Creation Fails**
   - Check field type is supported
   - Verify choices are provided for choice fields
   - Ensure formula syntax is correct for formula fields

### Enable Debug Logging
Set environment variable:
```bash
DEBUG=quickbase-mcp:*
```

## Implementation Notes

This server provides the maximum flexibility for QuickBase operations by:

1. **Direct API Access** - Uses QuickBase REST API v1 directly
2. **Complete Field Support** - Supports all QuickBase field types
3. **Relationship Management** - Can create and manage table relationships
4. **Bulk Operations** - Efficient bulk record operations
5. **Advanced Querying** - Full QuickBase query syntax support
6. **Error Handling** - Comprehensive error handling and retry logic

## Your QuickBase Application

Based on your mapping file, you have:
- **App ID**: `btr3r3fk5`
- **Realm**: `seanngates.quickbase.com`
- **Tables**: Leads, Clients, Orders, Sales Representatives, Employees, etc.

This server can help you implement the relationships and new fields defined in your mapping file.

## License

MIT License