#### Created: 2024-08-23
#### Tags:
# Setting up a fake JSON server for testing

Install the JSON server package
```bash
npm i json-server
```

Or, if you want to simulate a delay, use the older version:
```bash
npm i json-server@0.17.3
```

Add a script to the package.json file:
```json
"server": "json-server --watch data/cities.json --port 8000 --delay 1000"
```

NOTE: remove the optional delay if using newer version (as it is no longer supported)




