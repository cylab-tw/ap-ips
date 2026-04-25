# Condition (APS, IPS Derived) - Asia-Pacific Patient Summary v0.1.0

* [**Table of Contents**](toc.md)
* [**Artifacts Summary**](artifacts.md)
* **Condition (APS, IPS Derived)**

## Resource Profile: Condition (APS, IPS Derived) 

| | |
| :--- | :--- |
| *Official URL*:https://cylab-tw.github.io/aps-ig/StructureDefinition/condition-aps | *Version*:0.1.0 |
| Draft as of 2026-04-25 | *Computable Name*:ConditionAps |
| **Copyright/Legal**: Used by permission of Asia-Pacific Patient Summary Alliance, all rights reserved Creative Commons License | |

 
APS baseline profile directly derived from IPS Condition profile. 

**Usages:**

* This Profile is not used by any profiles in this Implementation Guide

You can also check for [usages in the FHIR IG Statistics](https://packages2.fhir.org/xig/hl7.fhir.asia.aps|current/StructureDefinition/condition-aps)

### Formal Views of Profile Content

 [Description of Profiles, Differentials, Snapshots and how the different presentations work](http://build.fhir.org/ig/FHIR/ig-guidance/readingIgs.html#structure-definitions). 

 

Other representations of profile: [CSV](StructureDefinition-condition-aps.csv), [Excel](StructureDefinition-condition-aps.xlsx), [Schematron](StructureDefinition-condition-aps.sch) 



## Resource Content

```json
{
  "resourceType" : "StructureDefinition",
  "id" : "condition-aps",
  "url" : "https://cylab-tw.github.io/aps-ig/StructureDefinition/condition-aps",
  "version" : "0.1.0",
  "name" : "ConditionAps",
  "title" : "Condition (APS, IPS Derived)",
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
  "description" : "APS baseline profile directly derived from IPS Condition profile.",
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
    "identity" : "workflow",
    "uri" : "http://hl7.org/fhir/workflow",
    "name" : "Workflow Pattern"
  },
  {
    "identity" : "sct-concept",
    "uri" : "http://snomed.info/conceptdomain",
    "name" : "SNOMED CT Concept Domain Binding"
  },
  {
    "identity" : "v2",
    "uri" : "http://hl7.org/v2",
    "name" : "HL7 v2 Mapping"
  },
  {
    "identity" : "rim",
    "uri" : "http://hl7.org/v3",
    "name" : "RIM Mapping"
  },
  {
    "identity" : "w5",
    "uri" : "http://hl7.org/fhir/fivews",
    "name" : "FiveWs Pattern Mapping"
  },
  {
    "identity" : "sct-attr",
    "uri" : "http://snomed.org/attributebinding",
    "name" : "SNOMED CT Attribute Binding"
  }],
  "kind" : "resource",
  "abstract" : false,
  "type" : "Condition",
  "baseDefinition" : "http://hl7.org/fhir/uv/ips/StructureDefinition/Condition-uv-ips",
  "derivation" : "constraint",
  "differential" : {
    "element" : [{
      "id" : "Condition",
      "path" : "Condition"
    }]
  }
}

```
