# migration-support-services-code

import requests
import json

# set up the URL for the ONOS REST API
url = 'http://172.17.0.5:8181/onos/v1/'

# create a new Host-to-Host intent
intent = {
    'type': 'HostToHostIntent',
    'appId': 'org.onosproject.cli',
    'priority': 100,
    'one': '00:00:00:00:00:01/1',
    'two': '00:00:00:00:00:02/1'
}

# convert the intent to JSON format
data = json.dumps(intent)

# set up the headers for the REST API request
headers = {
    'Content-Type': 'application/json',
    'Accept': 'application/json'
}

# send the REST API request to ONOS
response = requests.post(url + 'intents', headers=headers, data=data, auth=('onos', 'rocks'))

# check if the request was successful
if response.status_code == 200:
    print('Host-to-Host intent created successfully')
else:
    print('Error creating Host-to-Host intent:', response.content)
