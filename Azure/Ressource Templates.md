# Fields of a ressource template :

## Fields:
```
{
    "$schema": "http://schema.management.​azure.com/schemas/2019-04-01/deploymentTemplate.json#",​
    "contentVersion": "",​
    "parameters": {},​ // Not Obligatory
    "variables": {},​ // Not Obligatory
    "functions": [],​ // Not Obligatory
    "resources": [],​
    "outputs": {}​ // Not Obligatory
}
```

### Field parameters:
The parameters field accepts objects these various subfields such as :
```
"<parameter-name>" : {
        "type" : "<type-of-parameter-value>",
        "defaultValue": "<default-value-of-parameter>",
        "allowedValues": [ "<array-of-allowed-values>" ],
        "minValue": <minimum-value-for-int>,
        "maxValue": <maximum-value-for-int>,
        "minLength": <minimum-length-for-string-or-array>,
        "maxLength": <maximum-length-for-string-or-array-parameters>,
        "metadata": {
        "description": "<description-of-the parameter>"
        }
```
