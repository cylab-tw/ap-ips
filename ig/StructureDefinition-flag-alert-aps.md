# Flag Alert (APS, IPS Derived) - Asia-Pacific Patient Summary v0.1.0

* [**Table of Contents**](toc.md)
* [**Artifacts Summary**](artifacts.md)
* **Flag Alert (APS, IPS Derived)**

## Resource Profile: Flag Alert (APS, IPS Derived) 

| | |
| :--- | :--- |
| *Official URL*:https://cylab-tw.github.io/aps-ig/StructureDefinition/flag-alert-aps | *Version*:0.1.0 |
| Draft as of 2026-04-25 | *Computable Name*:FlagAlertAps |
| **Copyright/Legal**: Used by permission of Asia-Pacific Patient Summary Alliance, all rights reserved Creative Commons License | |

 
APS baseline profile directly derived from IPS Flag Alert profile. 

**Usages:**

* This Profile is not used by any profiles in this Implementation Guide

You can also check for [usages in the FHIR IG Statistics](https://packages2.fhir.org/xig/hl7.fhir.asia.aps|current/StructureDefinition/flag-alert-aps)

### Formal Views of Profile Content

 [Description of Profiles, Differentials, Snapshots and how the different presentations work](http://build.fhir.org/ig/FHIR/ig-guidance/readingIgs.html#structure-definitions). 

 

Other representations of profile: [CSV](StructureDefinition-flag-alert-aps.csv), [Excel](StructureDefinition-flag-alert-aps.xlsx), [Schematron](StructureDefinition-flag-alert-aps.sch) 



## Resource Content

```json
{
  "resourceType" : "StructureDefinition",
  "id" : "flag-alert-aps",
  "url" : "https://cylab-tw.github.io/aps-ig/StructureDefinition/flag-alert-aps",
  "version" : "0.1.0",
  "name" : "FlagAlertAps",
  "title" : "Flag Alert (APS, IPS Derived)",
  "status" : "draft",
  "date" : "2026-04-25T19:59:58+08:00",
  "publisher" : "Asia-Pacific Patient Summary Alliance",
  "contact" : [{
    "name" : "Asia-Pacific Patient Summary Alliance",
    "telecom" : [{
      "system" : "url",
      "value" : "https://cylab-tw.github.io/aps-ig"
    }]
  },
  {
    "name" : "Asia-Pacific Patient Summary Alliance",
    "telecom" : [{
      "system" : "email",
      "value" : "aps-ig@example.org",
      "use" : "work"
    }]
  }],
  "description" : "APS baseline profile directly derived from IPS Flag Alert profile.",
  "jurisdiction" : [{
    "coding" : [{
      "system" : "http://unstats.un.org/unsd/methods/m49/m49.htm",
      "code" : "035",
      "display" : "South-Eastern Asia"
    }]
  }],
  "copyright" : "Used by permission of Asia-Pacific Patient Summary Alliance, all rights reserved Creative Commons License",
  "fhirVersion" : "4.0.1",
  "mapping" : [{
    "identity" : "rim",
    "uri" : "http://hl7.org/v3",
    "name" : "RIM Mapping"
  },
  {
    "identity" : "w5",
    "uri" : "http://hl7.org/fhir/fivews",
    "name" : "FiveWs Pattern Mapping"
  }],
  "kind" : "resource",
  "abstract" : false,
  "type" : "Flag",
  "baseDefinition" : "http://hl7.org/fhir/uv/ips/StructureDefinition/Flag-alert-uv-ips",
  "derivation" : "constraint",
  "differential" : {
    "element" : [{
      "id" : "Flag",
      "path" : "Flag"
    }]
  }
}

```
