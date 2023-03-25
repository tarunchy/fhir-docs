# How to load FHIR Bundle JSON file in HAPI FHIR JPA server

This guide will show you how to load a FHIR Bundle JSON file into a HAPI FHIR JPA server using Java code.

## Prerequisites

- Java installed on your machine
- HAPI FHIR JPA server installed and running
- Basic understanding of Java programming

## Step-by-Step Guide

1. Create a new instance of the `FhirContext` class. This class is the entry point for interacting with FHIR resources using HAPI FHIR.

```
FhirContext ctx = FhirContext.forR4();
```

2. Create an instance of the JsonParser class, which is used to parse JSON-encoded FHIR resources.

```
JsonParser parser = ctx.newJsonParser();

```

3. Load the JSON file into a String variable. You can do this using a variety of methods, depending on your application. For example, you could read the file using a FileReader:

```
String json = new FileReader("bundle.json").readText();
```

4. Parse the JSON string using the parseResource method of the JsonParser class. This method takes a Class object representing the type of resource to parse and the JSON string to parse.

```
Bundle bundle = parser.parseResource(Bundle.class, json);

```

5. Finally, use the FhirContext to create a new instance of the FhirResourceDao for the resource type contained in the bundle, and call the create method to persist the resources to the database.


```
FhirResourceDao<Bundle> dao = ctx.getResourceDao(bundle.getType().toString());
dao.create(bundle);
```

This should load the resources from the FHIR Bundle JSON file into the HAPI FHIR JPA server.

## Conclusion
Loading a FHIR Bundle JSON file into a HAPI FHIR JPA server is a straightforward process using Java code. By following the steps in this guide, you should be able to load your FHIR resources into the server with ease.

