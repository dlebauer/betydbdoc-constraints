# Non Null Constraints

This is a list of fields that should not be allowed to be null. In all cases, the primary key should not be null. For many-to-many relationship tables, the foreign keys should be non-null.

* citations: author, year, title
* covariates: trait_id, variable_id
* cultivars: specie_id, name
* dbfiles: file_name, file_path, container_type, container_id, machine_id
* sites: lat, lon
* ensembles: workflow_id
* formats: dataformat
* formats_variables: ?
* inputs: name, access_level, format_id
* likelihoods: run_id, variable_id, input_id
* machines: hostname
* managements: date, management_type
* methods: name, description, citation_id
* sites: lat, lon, sitename
* treatments: control
