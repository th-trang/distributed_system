# Chapter 7
## What is JSON?
- JSON (JavaScript Object Notation) is a language-independent data format that express JSON objects as human-readable lists of properties (name-value pairs).
## JSON Syntax Tour
- JSON data format presents a JSON object as a brace-delimited and comma-seperated list of properties:
          {
            property 1,
            property 2,
            ...
            property N
          }
- Comma is not placed after the final property.
- For each property, the name is expressed as a string that’s typically quoted (and by a pair of double quotes). The name string is followed by a colon character, which is followed by a value of a specific type ( "name": "JSON", for example).
- JSON supports 6 types: - Number
                         - String
                         - Boolean
                         - Array
                         - Object
                         - Null
- Whitespace is allowed and ignored around or between syntactic elements.
## Validating JSON Objects
- It’s often necessary for applications to validate JSON objects, to ensure that required properties are present and that additional constraints are met. Validation is typically performed in the context of JSON Schema.
- JSON Schema is a grammar language for defining the structure, content, and (to some extent) semantics of JSON objects. It lets you specify metadata (data about data) about what an object’s properties mean and what values are valid for those properties. The result of applying the grammar language is a schema (a blueprint) describing the set of JSON objects that are valid according to the schema. 
