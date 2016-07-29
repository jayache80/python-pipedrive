python-pipedrive
================

Python library for interacting with the pipedrive.com API


This is being developed for my specific use so there's no guarantee I'll cover all of the aspects of the Pipedrive API. Feel free to add features though, I welcome pull requests.

All features should be supported though as this is just a lightweight wrapper around the API.


Usage:

Create a Pipedrive object, passing either the api key or your username and password as the parameters

```python
from pipedrive import Pipedrive
pipedrive = Pipedrive(USERNAME, PASSSWORD)
```

or

```python
from pipedrive import Pipedrive
pipedrive = Pipedrive(API_KEY)
```

The rest of the functions relate to the URL as specified in the [API Docs](https://developers.pipedrive.com/v1).

The two things to note are the HTTP Method, and the path:

Examples:

1.  List the organizations
    ```python
        pipedrive.organizations(method='GET')
    ```

2.  Add a New Deal
    ```python
        pipedrive.deals({
        	'title': 'Big Sucker',
        	'value': 1000000,
        	'org_id': 2045,
        	'status': 'open'
       	}, method='POST')
    ```

3.  Delete an Activity
    ```python
        pipedrive.activities({'id': 6789}, method='DELETE')
    ```

4.  Find a person, and use the search results. The variable ```term``` is the search term that has been passed in.
    ```python
        import json
        ...
        response = pipedrive.persons_find({'term':term}, method='GET')
        results = response['data']
        suggestions = []
        if results != None:
                for result in results:
                    suggestions.append({'value': result['name'], 'data': result})
        json_response = {'query': term, 'suggestions': suggestions}
        data = json.dumps(json_response)

    ```
    And return ```data``` to some kind of javascript search result autocomplete thing (this example is formatted for devbridge's simple and easy-to-use [jquery.autocomplete.js](https://github.com/devbridge/jQuery-Autocomplete))
