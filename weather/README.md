This repository is a practice session for MIT Hack Decentralized AI summit. It includes basic steps to create a Claude MCP protocol up and running in under 5 minutes on Windows

# To get started with weather app. 
### Note: Make sure you pip install uv
```
cd weather
uv run weather.py
```
This starts the server hosted locally on your machine. The python file includes tools available to LLM for get alerts and forecast from gov api. 
Make sure you changed the claude_config.json available on claude desktop File-> Settings-> Developer-> Edit Config and edit config section. Provide absolute path to your python file. Voila your 1st mcp server is up and running in 5 mins.


## Sample config file
```
{"mcpServers":{"weather":{"command":"npx","args":["-y","<abs_path_to_file>/mcp-server-weather"]}}}
```

# SQL-lite db example for bakery data
Steps to run the SQL DB as an MCP server : 

Step 1. “git clone https://github.com/modelcontextprotocol/servers.git “ 
Step 2. “cd servers” 
Step 3. “cd src “ 
Step 4. “cd sqlite”

Install docker if you need it  : https://docs.docker.com/engine/install/
Install it, verify it runs as per the documentation upon the link

 Then we run the docker build command 
Step 5. “docker build -t mcp/sqlite .” 
This makes the docker image and then 

Step 6. Paste this into your config file : 
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

And restart claude to run ! 


Step 7.

Quick version:
1.. Create bakery DB tables:
   - ingredients (id, name, unit, quantity, cost, supplier, min_order_quantity)

2. Populate with:
   - 10 ingredients with MOQs

3. Add queries for:
   - Low stock alerts


Hope this is helpful to you in the future!