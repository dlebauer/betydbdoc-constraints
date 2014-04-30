# Non Null Constraints

This is a list of fields that should not be allowed to be null. In all cases, the primary key should not be null. For many-to-many relationship tables, the foreign keys should be non-null.

* citations: author, year, title
* covariates: trait\_id, variable\_id
* cultivars: specie\_id, name
* dbfiles: file_name, file\_path, container\_type, container\_id, machine\_id
* sites: lat, lon
* ensembles: workflow\_id
* formats: dataformat
* formats\_variables: ?
* inputs: name, access\_level, format\_id
* likelihoods: run\_id, variable\_id, input\_id
* machines: hostname
* managements: date, management\_type
* methods: name, description, citation\_id
* models: model\_name, model\_path, revision, model\_type
* pfts: definition, name
* posteriors: pft\_id, format\_id
* priors: phylogeny, variable\_id, distn, parama, paramb
* runs: model\_id, site\_id, start\_time, finish\_time, outdir, outprefix, setting, parameter\_list, started\_at, ensemble\_id (note: finished\_at will not be available when record is created)
* sites: lat, lon, sitename, greenhouse
* species: genus, species, scientificname
* traits: specie\_id, citation\_id, treatment\_id, mean, variable\_id, checked, access\_level
* treatments: name, control
* users: login, name, email, crypted\_password, salt, access\_level, page\_access\_level, apikey
* variables: namem, units 
* workflows: folder, started\_at, site\_id, model\_id, hostname, params, advanced\_edit, start\_date, end\_date 
* yields: specie\_id, citation\_id, treatment\_id, mean, variable\_id, checked, access\_level
