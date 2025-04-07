# Claude MCP Protocol Practice

This repository is a practice session for MIT Hack Decentralized AI summit. It includes basic steps to create a Claude MCP protocol up and running in under 5 minutes on Windows.

## Weather App Setup

### Prerequisites
- Make sure you pip install uv

### Steps
```bash
cd weather
uv run weather.py
```

This starts the server hosted locally on your machine. The python file includes tools available to LLM for getting alerts and forecast from government API.

### Claude Configuration
Make sure you changed the claude_config.json available on Claude desktop:
1. Navigate to File -> Settings -> Developer -> Edit Config
2. Edit config section and provide absolute path to your python file

Voila! Your 1st MCP server is up and running in 5 mins.

### Sample Config File
```json
{
  "mcpServers": {
    "weather": {
      "command": "npx",
      "args": ["-y", "<abs_path_to_file>/mcp-server-weather"]
    }
  }
}
```

## SQL-lite DB Example for Bakery Data

### Steps to Run the SQL DB as an MCP Server

1. Clone the repository:
   ```bash
   git clone https://github.com/modelcontextprotocol/servers.git
   ```

2. Navigate to the SQLite directory:
   ```bash
   cd servers
   cd src
   cd sqlite
   ```

3. Install Docker if needed:
   - Follow instructions at: https://docs.docker.com/engine/install/
   - Verify it runs as per the documentation

4. Build the Docker image:
   ```bash
   docker build -t mcp/sqlite .
   ```

5. Update your Claude config file:
   ```json
   {
     "mcpServers": {
       "sqlite": {
         "command": "docker",
         "args": [
           "run",
           "--rm",
           "-i",
           "-v",
           "mcp-test:/mcp",
           "mcp/sqlite",
           "--db-path",
           "/mcp/test.db"
         ]
       }
     }
   }
   ```

6. Restart Claude to apply changes

### Bakery Database Setup

1. Create bakery DB tables:
   - ingredients (id, name, unit, quantity, cost, supplier, min_order_quantity)

2. Populate with:
   - 10 ingredients with MOQs

3. Add queries for:
   - Low stock alerts

Hope this is helpful to you in the future!

## References
[MIT Hack Documentation](https://docs.google.com/document/d/1Ej7xWB3qgu5Xrev8bL-OqmpOIMeXGffsAEYW0Wo1g0U/edit?addon_store&tab=t.16jeva4p929l)
