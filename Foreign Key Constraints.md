# Foreign Key Constraints

```ALTER TABLE "traits" ADD CONSTRAINT "fk_traits_species_1" FOREIGN KEY ("specie_id") REFERENCES "species" ("id");

ALTER TABLE "yields" ADD CONSTRAINT "fk_yields_species_1" FOREIGN KEY ("specie_id") REFERENCES "species" ("id");

ALTER TABLE "traits" ADD CONSTRAINT "fk_traits_sites_1" FOREIGN KEY ("site_id") REFERENCES "sites" ("id");

ALTER TABLE "yields" ADD CONSTRAINT "fk_yields_sites_1" FOREIGN KEY ("site_id") REFERENCES "sites" ("id");

ALTER TABLE "traits" ADD CONSTRAINT "fk_traits_citations_1" FOREIGN KEY ("citation_id") REFERENCES "citations" ("id");

ALTER TABLE "yields" ADD CONSTRAINT "fk_yields_citations_1" FOREIGN KEY ("citation_id") REFERENCES "citations" ("id");

ALTER TABLE "traits" ADD CONSTRAINT "fk_traits_cultivars_1" FOREIGN KEY ("cultivar_id") REFERENCES "cultivars" ("id");

ALTER TABLE "yields" ADD CONSTRAINT "fk_yields_cultivars_1" FOREIGN KEY ("cultivar_id") REFERENCES "cultivars" ("id");

ALTER TABLE "traits" ADD CONSTRAINT "fk_traits_treatments_1" FOREIGN KEY ("treatment_id") REFERENCES "treatments" ("id");

ALTER TABLE "yields" ADD CONSTRAINT "fk_yields_treatments_1" FOREIGN KEY ("treatment_id") REFERENCES "treatments" ("id");

ALTER TABLE "treatments" ADD CONSTRAINT "fk_treatments_users_1" FOREIGN KEY ("user_id") REFERENCES "users" ("id");

ALTER TABLE "citations" ADD CONSTRAINT "fk_citations_users_1" FOREIGN KEY ("user_id") REFERENCES "users" ("id");

ALTER TABLE "yields" ADD CONSTRAINT "fk_yields_users_1" FOREIGN KEY ("user_id") REFERENCES "users" ("id");

ALTER TABLE "traits" ADD CONSTRAINT "fk_traits_users_1" FOREIGN KEY ("user_id") REFERENCES "users" ("id");

ALTER TABLE "yields" ADD CONSTRAINT "fk_yields_entities_1" FOREIGN KEY ("entity_id") REFERENCES "entities" ("id");

ALTER TABLE "traits" ADD CONSTRAINT "fk_traits_entities_1" FOREIGN KEY ("entity_id") REFERENCES "entities" ("id");

ALTER TABLE "yields" ADD CONSTRAINT "fk_yields_methods_1" FOREIGN KEY ("method_id") REFERENCES "methods" ("id");

ALTER TABLE "traits" ADD CONSTRAINT "fk_traits_methods_1" FOREIGN KEY ("method_id") REFERENCES "methods" ("id");

ALTER TABLE "cultivars" ADD CONSTRAINT "fk_cultivars_cultivars_1" FOREIGN KEY ("previous_id") REFERENCES "cultivars" ("id");

ALTER TABLE "cultivars" ADD CONSTRAINT "fk_cultivars_species_1" FOREIGN KEY ("specie_id") REFERENCES "species" ("id");

ALTER TABLE "sites" ADD CONSTRAINT "fk_sites_users_1" FOREIGN KEY ("user_id") REFERENCES "users" ("id");

ALTER TABLE "pfts_priors" ADD CONSTRAINT "fk_pfts_priors_pfts_1" FOREIGN KEY ("pft_id") REFERENCES "pfts" ("id");

ALTER TABLE "pfts_priors" ADD CONSTRAINT "fk_pfts_priors_priors_1" FOREIGN KEY ("prior_id") REFERENCES "priors" ("id");

ALTER TABLE "pfts_species" ADD CONSTRAINT "fk_pfts_species_pfts_1" FOREIGN KEY ("pft_id") REFERENCES "pfts" ("id");

ALTER TABLE "pfts_species" ADD CONSTRAINT "fk_pfts_species_species_1" FOREIGN KEY ("specie_id") REFERENCES "species" ("id");

ALTER TABLE "covariates" ADD CONSTRAINT "fk_covariates_traits_1" FOREIGN KEY ("trait_id") REFERENCES "traits" ("id");

ALTER TABLE "covariates" ADD CONSTRAINT "fk_covariates_variables_1" FOREIGN KEY ("variable_id") REFERENCES "variables" ("id");

ALTER TABLE "traits" ADD CONSTRAINT "fk_traits_variables_1" FOREIGN KEY ("variable_id") REFERENCES "variables" ("id");

ALTER TABLE "managements_treatments" ADD CONSTRAINT "fk_managements_treatments_managements_1" FOREIGN KEY ("management_id") REFERENCES "managements" ("id");

ALTER TABLE "managements_treatments" ADD CONSTRAINT "fk_managements_treatments_treatments_1" FOREIGN KEY ("treatment_id") REFERENCES "treatments" ("id");

ALTER TABLE "citations_sites" ADD CONSTRAINT "fk_citations_sites_citations_1" FOREIGN KEY ("citation_id") REFERENCES "citations" ("id");

ALTER TABLE "citations_sites" ADD CONSTRAINT "fk_citations_sites_sites_1" FOREIGN KEY ("site_id") REFERENCES "sites" ("id");

ALTER TABLE "inputs" ADD CONSTRAINT "fk_inputs_sites_1" FOREIGN KEY ("site_id") REFERENCES "sites" ("id");

ALTER TABLE "inputs" ADD CONSTRAINT "fk_inputs_users_1" FOREIGN KEY ("user_id") REFERENCES "users" ("id");

ALTER TABLE "inputs" ADD CONSTRAINT "fk_inputs_inputs_1" FOREIGN KEY ("parent_id") REFERENCES "inputs" ("id");

ALTER TABLE "inputs" ADD CONSTRAINT "fk_inputs_formats_1" FOREIGN KEY ("format_id") REFERENCES "formats" ("id");

ALTER TABLE "dbfiles" ADD CONSTRAINT "fk_dbfiles_users_1" FOREIGN KEY ("created_user_id") REFERENCES "users" ("id");

ALTER TABLE "dbfiles" ADD CONSTRAINT "fk_dbfiles_users_2" FOREIGN KEY ("updated_user_id") REFERENCES "users" ("id");

ALTER TABLE "dbfiles" ADD CONSTRAINT "fk_dbfiles_machines_1" FOREIGN KEY ("machine_id") REFERENCES "machines" ("id");

ALTER TABLE "inputs_variables" ADD CONSTRAINT "fk_inputs_variables_variables_1" FOREIGN KEY ("variable_id") REFERENCES "variables" ("id");

ALTER TABLE "inputs_variables" ADD CONSTRAINT "fk_inputs_variables_inputs_1" FOREIGN KEY ("input_id") REFERENCES "inputs" ("id");

ALTER TABLE "inputs_runs" ADD CONSTRAINT "fk_inputs_runs_inputs_1" FOREIGN KEY ("input_id") REFERENCES "inputs" ("id");

ALTER TABLE "inputs_runs" ADD CONSTRAINT "fk_inputs_runs_runs_1" FOREIGN KEY ("run_id") REFERENCES "runs" ("id");

ALTER TABLE "runs" ADD CONSTRAINT "fk_runs_models_1" FOREIGN KEY ("model_id") REFERENCES "models" ("id");

ALTER TABLE "models" ADD CONSTRAINT "fk_models_models_1" FOREIGN KEY ("parent_id") REFERENCES "models" ("id");

ALTER TABLE "posteriors_runs" ADD CONSTRAINT "fk_posteriors_runs_posteriors_1" FOREIGN KEY ("posterior_id") REFERENCES "posteriors" ("id");

ALTER TABLE "posteriors_runs" ADD CONSTRAINT "fk_posteriors_runs_runs_1" FOREIGN KEY ("run_id") REFERENCES "runs" ("id");

ALTER TABLE "formats_variables" ADD CONSTRAINT "fk_formats_variables_variables_1" FOREIGN KEY ("variable_id") REFERENCES "variables" ("id");

ALTER TABLE "likelihoods" ADD CONSTRAINT "fk_likelihoods_variables_1" FOREIGN KEY ("variable_id") REFERENCES "variables" ("id");

ALTER TABLE "likelihoods" ADD CONSTRAINT "fk_likelihoods_runs_1" FOREIGN KEY ("run_id") REFERENCES "runs" ("id");

ALTER TABLE "likelihoods" ADD CONSTRAINT "fk_likelihoods_inputs_1" FOREIGN KEY ("input_id") REFERENCES "inputs" ("id");

ALTER TABLE "posteriors" ADD CONSTRAINT "fk_posteriors_pfts_1" FOREIGN KEY ("pft_id") REFERENCES "pfts" ("id");

ALTER TABLE "posteriors" ADD CONSTRAINT "fk_posteriors_formats_1" FOREIGN KEY ("format_id") REFERENCES "formats" ("id");

ALTER TABLE "formats_variables" ADD CONSTRAINT "fk_formats_variables_formats_1" FOREIGN KEY ("format_id") REFERENCES "formats" ("id");

ALTER TABLE "ensembles" ADD CONSTRAINT "fk_ensembles_workflows_1" FOREIGN KEY ("workflow_id") REFERENCES "workflows" ("id");

ALTER TABLE "workflows" ADD CONSTRAINT "fk_workflows_models_1" FOREIGN KEY ("model_id") REFERENCES "models" ("id");

ALTER TABLE "workflows" ADD CONSTRAINT "fk_workflows_sites_1" FOREIGN KEY ("site_id") REFERENCES "sites" ("id");

ALTER TABLE "runs" ADD CONSTRAINT "fk_runs_sites_1" FOREIGN KEY ("site_id") REFERENCES "sites" ("id");

ALTER TABLE "runs" ADD CONSTRAINT "fk_runs_ensembles_1" FOREIGN KEY ("ensemble_id") REFERENCES "ensembles" ("id");

ALTER TABLE "priors" ADD CONSTRAINT "fk_priors_variables_1" FOREIGN KEY ("variable_id") REFERENCES "variables" ("id");

ALTER TABLE "priors" ADD CONSTRAINT "fk_priors_citations_1" FOREIGN KEY ("citation_id") REFERENCES "citations" ("id");

ALTER TABLE "formats" ADD CONSTRAINT "fk_formats_mimetypes_1" FOREIGN KEY ("mimetype_id") REFERENCES "mimetypes" ("id");

ALTER TABLE "entities" ADD CONSTRAINT "fk_entities_entities_1" FOREIGN KEY ("parent_id") REFERENCES "entities" ("id");

ALTER TABLE "citations_treatments" ADD CONSTRAINT "fk_citations_treatments_treatments_1" FOREIGN KEY ("treatment_id") REFERENCES "treatments" ("id");

ALTER TABLE "citations_treatments" ADD CONSTRAINT "fk_citations_treatments_citations_1" FOREIGN KEY ("citation_id") REFERENCES "citations" ("id");

ALTER TABLE "managements" ADD CONSTRAINT "fk_managements_citations_1" FOREIGN KEY ("citation_id") REFERENCES "citations" ("id");


```