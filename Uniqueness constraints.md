

# Uniqueness constraints

These are "natural keys", i.e. combinations of fields that should be unique within a table. Ideally, each table would have a natural key, but a table may have 0, 1, or many uniqueness constraints.

For many-to-many relationship tables, the foreign key pairs should be unique; these should be implemented but are not listed here for brevity.

* citations: author, year, title
* covariates: trait\_id, variable\_id
* cultivars: specie\_id, name
* dbfiles: file\_name, file\_path, machine\_id
* dbfiles: container\_type, container\_id
* formats\_variables: ?
* formats: site\_id, start\_date, end\_date, format\_id
* likelihoods: run\_id, variable\_id, input\_id
* machines: hostname
* managements: date, management\_type
* methods: name, citation\_id
* models: model\_path
* pfts: name
* posteriors: pft\_id
* priors: phylogeny, variable\_id, distn, parama, paramb
* priors: phylogeny, variable\_id, notes
* runs: (?) model\_id, site\_id, start\_time, finish\_time, parameter\_list, ensemble\_id
* sites: lat, lon, sitename
* species: scientificname (not genus, species because there may be multiple varieties)
* traits: site\_id, specie\_id, citation\_id, cultivar\_id, treatment\_id, date, time, variable\_id, entity\_id, method\_id, date\_year, date\_month, date\_day, time\_hour, time\_minute
* treatments: 
 * for a given citation, name should be unique; 
 * for a given citation and site, there should be only one control
* users: (each of the following fields should be independently unique from other records) 
 * login
 * email
 * crypted\_password
 * salt 
 * apikey
* variables: name
* workflows: site\_id, model\_id, params, advanced\_edit, start\_date, end\_date
* yields: site\_id, specie\_id, citation\_id, cultivar\_id, treatment\_id, date, entity\_id, method\_id, date\_year, date\_month, date\_day