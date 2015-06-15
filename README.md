# ua-parser

Contains the forked [uap-core](https://github.com/adorsys/uap-core) and [uap-java](https://github.com/adorsys/uap-java).

## Changes

### Common

* Updated DeviceParser to work with new core regexes
* GroupId and Packages changed from ua_parser to de.adorsys.ua_parser (avoids conflicts...)
* Updated Java6 to Java7 and other dependecies to current versions
* Projects can be released to the adorsys nexus

### KTB Agents

The parser now handles KTB specific agents like this:

    APP-BE Test/1.0 (iPad; Apple; CPU iPhone OS 7_0_2 like Mac OS X)
    
Which results to following UserAgent:

    {
      "family": "BE Test", 
      "major": "1", 
      "minor": "0", 
      "patch": "", 
      "engine": "Mobile App"
    }

The engine must be defined in uap-core/regexes.yaml:

    # KTB 
    - regex: 'APP-([\w\s-\d]+)\/(\d+)\.(\d+)'
      family_replacement: '$1'
      engine_replacement: 'Mobile App'    
      
Note: The engine is null unless there is a replacement defined. No pattern matching here.