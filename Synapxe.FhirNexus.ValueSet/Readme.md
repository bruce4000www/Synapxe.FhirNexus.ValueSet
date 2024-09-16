This repo is for monthly sharing purposes. Following are the steps to create and run the demo:
1. Create a new project from FhirNexus template.
2. Create a seed data file `seed-valueset.json` in the project root directory.
3. Configure `fhirengine.json` file to use terminology service and include the `seed-valueset.json` file as its seed data.
```
  "Handlers": {
    "Repository": {
      "FhirTerminologyDataStore": {
        "CorrelationIdTagSystem": "http://ihis.sg/coding/correlationid",
        "UseSqlRelationalModels": {
          "AutoCreateTables": true
        },
        "ConnectionString": "TerminologyDb",
        "BaseUrl": "http://health.sg/",
        "SeedDataPaths": [
          "seed-valuesets.json"
        ]
      }
    }
  }
```
4. Update `appsetting.Development.json` to include the connection string for the terminology database.
```
{
  "ConnectionStrings": {
	"TerminologyDb": "Server=(localdb)\\MSSQLLocalDB;Integrated Security=True;Encrypt=false;Database=Synapxe.FhirNexus.ValueSet;Encrypt=false"
  }
}
```
5. Add following nuget packages `Ihis.FhirEngine.Data.TerminologyDataStore.R5` and `Ihis.FhirEngine.Data.Relational.SqlServer` to the project file.
6. Update `Conformance/Appointment-custom.StructureDefinition.json` to bind the `Appointment.serviceCategory` to ValueSet `http://synapxe.sg/ValueSet/fhirnexus-appointment-category`
7. Run the project and test it with `Sample Request\appointment.http` file.
