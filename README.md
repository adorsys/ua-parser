# ua-parser

Contains the forked [uap-core](https://github.com/adorsys/uap-core) and [uap-java](https://github.com/adorsys/uap-java).

## Build and Releases

**This project includes two independent git-submodules which must be built and released seperatly (uap-core before uap-java).**

Could be fixed by adding a parent pom if anybody knows if it's possible to release a multi-modul project which includes maven-modules as git-modules.

## Changes

### Common

* Updated DeviceParser to work with new core regexes
* GroupId and Packages changed from ua_parser to de.adorsys.uap.java (avoids conflicts...)
* Updated Java6 to Java7 and other dependecies to current versions
* uap-core is now also a maven project which builds a jar and a test-jar containing the regexes. 
  Both can be released and uap-java relies on a released version of uap-core
  (a mvn release relying on relative paths doesn't work)
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