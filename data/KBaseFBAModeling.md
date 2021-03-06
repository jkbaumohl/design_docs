#FBA Modeling
##Description 
Flux Balance Analysis Modeling

##Owner/Author
Chris Henry

##Repo
https://github.com/kbase/KBaseFBAModeling

##Data Sources
* Uses mongo db
* Workspace
* idserver - which uses mongo


##Dependencies
typecomp
kb_seed
auth
idserver
kb_model_seed
probabilistic_annotation
workspace_deluxe
genome_annotation

##SPECS: 
Note there are 12 spec files.
11 appear to be WS specs and one is a spec file for 95 functions.
Note that many of these specs are duplicated from other repos.
Since the spec is being stored in two locations there is a probability for the WS specs in this repo to be out of date.
Note mutiple specs have the same name structure but they are already out of sync with one another.
Example Biochemistry in fbaModelServices.spec is not consistent with the Biochemistry in Biochem.spec

The Specs are : 

1. Biochem.spec 
2. Expression.spec
3. FBAModel.spec
4. Genome.spec
5. GenomeComparison.spec
6. Metabolome.spec
7. Ontology.spec
8. Phenotypes.spec
9. ProbabilisticAnnotation.spec
10. Regulation.spec
11. RegulatoryFBA.spec
12. fbaModelServices.spec  - This is where the function specs reside.

##Methods from https://github.com/kbase/KBaseFBAModeling/blob/master/fbaModelServices.spec
95 Methods.

###Function definitions relating to data retrieval for Model Objects

1. funcdef get_models(get_models_params input) returns (list<FBAModel> out_models);

			/* Input parameters for the "get_models" function.
				list<fbamodel_id> models - a list of the model IDs for the models to be returned (a required argument)
				list<workspace_id> workspaces - a list of the workspaces contianing the models to be returned (a required argument)
				string id_type - the type of ID that should be used in the output data (a optional argument; default is 'ModelSEED')
				string auth - the authentication token of the KBase account changing workspace permissions; must have 'admin' privelages to workspace (an optional argument; user is "public" if auth is not provided)
					
			*/
			typedef structure {
				list<fbamodel_id> models;
				list<workspace_id> workspaces;
				string auth;
				string id_type;
			} get_models_params;
			/*
			    Returns model data for input ids
			*/

2. funcdef get_fbas(get_fbas_params input) returns (list<FBA> out_fbas);	

		/* Input parameters for the "get_fbas" function.
		
			list<fba_id> fbas - a list of the FBA study IDs for the FBA studies to be returned (a required argument)
			list<workspace_id> workspaces - a list of the workspaces contianing the FBA studies to be returned (a required argument)
	        string id_type - the type of ID that should be used in the output data (a optional argument; default is 'ModelSEED')
			string auth - the authentication token of the KBase account changing workspace permissions; must have 'admin' privelages to workspace (an optional argument; user is "public" if auth is not provided)
				
		*/
	    typedef structure {
			list<fba_id> fbas;
			list<workspace_id> workspaces; 
			string auth;
	        string id_type;
	    } get_fbas_params;
	    /*
	    	Returns data for the requested flux balance analysis formulations
	    */

3. funcdef get_gapfills(get_gapfills_params input) returns (list<GapFill> out_gapfills);

		/* Input parameters for the "get_gapfills" function.
			list<gapfill_id> gapfills - a list of the gapfill study IDs for the gapfill studies to be returned (a required argument)
			list<workspace_id> workspaces - a list of the workspaces contianing the gapfill studies to be returned (a required argument)
	        string id_type - the type of ID that should be used in the output data (a optional argument; default is 'ModelSEED')
			string auth - the authentication token of the KBase account changing workspace permissions; must have 'admin' privelages to workspace (an optional argument; user is "public" if auth is not provided)
				
		*/
	    typedef structure {
			list<gapfill_id> gapfills;
			list<workspace_id> workspaces; 
			string auth;
	        string id_type;
	    } get_gapfills_params;
	    /*
	    	Returns data for the requested gap filling simulations
	    */

4. funcdef get_gapgens(get_gapgens_params input) returns (list<GapGen> out_gapgens);	

		/* Input parameters for the "get_gapgens" function.
			list<gapgen_id> gapgens - a list of the gapgen study IDs for the gapgen studies to be returned (a required argument)
			list<workspace_id> workspaces - a list of the workspaces contianing the gapgen studies to be returned (a required argument)
	        string id_type - the type of ID that should be used in the output data (a optional argument; default is 'ModelSEED')
			string auth - the authentication token of the KBase account changing workspace permissions; must have 'admin' privelages to workspace (an optional argument; user is "public" if auth is not provided)
				
		*/
	    typedef structure {
			list<gapgen_id> gapgens;
			list<workspace_id> workspaces;
			string auth;
	        string id_type;
	    } get_gapgens_params;
	    /*
	    	Returns data for the requested gap generation simulations
	    */


5. funcdef get_reactions(get_reactions_params input) returns (list<Reaction> out_reactions);	

		/* Input parameters for the "get_reactions" function.
		
			list<reaction_id> reactions - a list of the reaction IDs for the reactions to be returned (a required argument)
			string id_type - the type of ID that should be used in the output data (a optional argument; default is 'ModelSEED')
			string auth - the authentication token of the KBase account changing workspace permissions; must have 'admin' privelages to workspace (an optional argument; user is "public" if auth is not provided)
				
		*/
	    typedef structure {
			list<reaction_id> reactions;
			string auth;
	        string id_type;
	    } get_reactions_params;
	    /*
	    	Returns data for the requested reactions
	    */

    
6. funcdef get_compounds(get_compounds_params input) returns (list<Compound> out_compounds);	
	
		/* 
		        Input parameters for the "get_compounds" function.	
			list<compound_id> compounds - a list of the compound IDs for the compounds to be returned (a required argument)
			string id_type - the type of ID that should be used in the output data (a optional argument; default is 'ModelSEED')
			string auth - the authentication token of the KBase account changing workspace permissions; must have 'admin' privelages to workspace (an optional argument; user is "public" if auth is not provided)
				
		*/
	    typedef structure {
			list<compound_id> compounds;
			string auth;
	        string id_type;
	    } get_compounds_params;
	    /*
	    	Returns data for the requested compounds
	    */

7. funcdef get_alias(get_alias_params input) returns (list<get_alias_outputs> output);
	
	    /* Input parameters for the get_alias function
	                string object_type    - The type of object (e.g. Compound or Reaction)
	                string input_id_type - The type (e.g. ModelSEED) of alias to be inputted
			string output_id_type - The type (e.g. KEGG) of alias to be outputted
			list<string> input_ids - A list of input IDs
			string auth; - The authentication token of the KBase account (optional)
	    */
	
	    typedef structure {
			string object_type;
			string input_id_type;
			string output_id_type;
			list<string> input_ids;
			string auth;
	    } get_alias_params;
	
	    /* Output for get_alias function
	
	              string original_id - The original ID
		      list<string> aliases - Aliases for the original ID in the new format
	
	    */
	    typedef structure {
			string original_id;
			list<string> aliases;
	    } get_alias_outputs;
	
	    /* Turns one compound I into another of a different type */

8. funcdef get_aliassets(get_aliassets_params input) returns ( list<string> aliassets );	

	    /* Input parameters for the get_aliassets function
	
	              string auth; - The authentication token of the KBase account (optional)
		      string object_type; - The type of object (e.g. Compound or Reaction)
	    */
	    typedef structure {
		string object_type;
		string auth;
	    } get_aliassets_params;
	
	    /* 
	         Get possible types of aliases (alias sets) 
	    */

9. funcdef get_media(get_media_params input) returns (list<Media> out_media);
    
	    /* Input parameters for the "get_media" function.
			list<media_id> medias - a list of the media IDs for the media to be returned (a required argument)
			string id_type - the type of ID that should be used in the output data (a optional argument; default is 'ModelSEED')
			string auth - the authentication token of the KBase account changing workspace permissions; must have 'admin' privelages to workspace (an optional argument; user is "public" if auth is not provided)
				
		*/
	    typedef structure {
			list<media_id> medias;
			list<workspace_id> workspaces;
			string auth;
	    } get_media_params;
	    /*
	    	Returns data for the requested media formulations
	    */

10. funcdef get_biochemistry(get_biochemistry_params input) returns (Biochemistry out_biochemistry);    

		/* Input parameters for the "get_biochemistry" function.
		
			biochemistry_id biochemistry - ID of the biochemistry database to be returned (a required argument)
			workspace_id biochemistry_workspace - workspace containing the biochemistry database to be returned (a required argument)
			string id_type - the type of ID that should be used in the output data (a optional argument; default is 'ModelSEED')
			string auth - the authentication token of the KBase account changing workspace permissions; must have 'admin' privelages to workspace (an optional argument; user is "public" if auth is not provided)
				
		*/
	    typedef structure {
	        biochemistry_id biochemistry;
	        workspace_id biochemistry_workspace;
	        string id_type;
	        string auth;
	    } get_biochemistry_params;
	    /*
	    	Returns biochemistry object
	    */

###Code relating to reconstruction of metabolic models

11. funcdef import_probanno(import_probanno_params input) returns (object_metadata probannoMeta);    
	
	    /* Input parameters for the "import_probanno" function.
		
			probanno_id probanno - id of the probabilistic annotation to be created (an optional parameter; default is 'undef')
			workspace_id workspace - id of the workspace where the probabilistic annotation will be stored (an essential parameter)
			genome_id genome - id of the genome that the probabilistic annotation will be associated with (an essential parameter)
			workspace_id genome_workspace - workspace containing the genome for the probabilistic annotation (an optional parameter; default is 'workspace' parameter)
			list<annotationProbability> annotationProbabilities - a list of the probabilistic annotations for all genes to be part of the prababilistic annotations (an essential parameter)
			bool ignore_errors - a flag indicating that even if errors are encountered, the probabilistic annotation should still be imported (an optional parameter; default is '0')
			string auth - the authentication token of the KBase account changing workspace permissions; must have 'admin' privelages to workspace (an optional argument; user is "public" if auth is not provided)
			
		*/
	    typedef structure {
			probanno_id probanno;
			workspace_id workspace;		
			genome_id genome;
			workspace_id genome_workspace;
			list<annotationProbability> annotationProbabilities;
			bool ignore_errors;
			string auth;
			bool overwrite;
	    } import_probanno_params;
	    /*
	        Loads an input genome object into the workspace.
	    */

12. funcdef genome_object_to_workspace(genome_object_to_workspace_params input) returns (object_metadata genomeMeta);    
    
	    /* Input parameters for the "genome_object_to_workspace" function.
		
			Genome_uid uid - ID to use when saving genome to workspace
			GenomeObject genomeobj - full genome typed object to be loaded into the workspace (a required argument)
			workspace_id workspace - ID of the workspace into which the genome typed object is to be loaded (a required argument)
			string auth - the authentication token of the KBase account changing workspace permissions; must have 'admin' privelages to workspace (an optional argument; user is "public" if auth is not provided)
	
		*/
	    typedef string Genome_uid;
	    typedef structure {
			Genome_uid uid;
			GenomeObject genomeobj;
			workspace_id workspace;
			string auth;
			bool overwrite;
	    } genome_object_to_workspace_params;
	    /*
	        Loads an input genome object into the workspace.
	    */

13. funcdef genome_to_workspace(genome_to_workspace_params input) returns (object_metadata genomeMeta);   
    
	    /* Input parameters for the "genome_to_workspace" function.
		
			genome_id genome - ID of the CDM genome that is to be loaded into the workspace (a required argument)
			string sourceLogin - login to pull private genome from source database
			string sourcePassword - password to pull private genome from source database
			string source - Source database for genome (i.e. seed, rast, kbase)
			workspace_id workspace - ID of the workspace into which the genome typed object is to be loaded (a required argument)
			string auth - the authentication token of the KBase account changing workspace permissions; must have 'admin' privelages to workspace (an optional argument; user is "public" if auth is not provided)
			Genome_uid uid - ID to use when saving genome to workspace
	
		*/
	    typedef structure {
			genome_id genome;
			workspace_id workspace;
			string sourceLogin;
			string sourcePassword;
			string source;
			string auth;
			bool overwrite;
			Genome_uid uid;
	    } genome_to_workspace_params;
	    /*
	        Retrieves a genome from the CDM and saves it as a genome object in the workspace.
	    */

14. funcdef domains_to_workspace(domains_to_workspace_params input) returns (object_metadata GenomeDomainMeta);    
    
	    /* Input parameters for the "domains_to_workspace" function.
		
			genome_id genome - ID of the workspace genome to fetch domains for (a required argument)
			string output_id - ID in which the domains are to be saved (default is genome ID plus ".dom.0")
			workspace_id workspace - ID of the workspace into which the domains are to be loaded (a required argument)
			string auth - the authentication token of the KBase account changing workspace permissions; must have 'admin' privelages to workspace (an optional argument; user is "public" if auth is not provided)
	
		*/
	    typedef structure {
			genome_id genome;
			string output_id;
			workspace_id workspace;
			string auth;
	    } domains_to_workspace_params;
	    /*
	        Computes or fetches domains for a genome
	    */

15. funcdef compute_domains(compute_domains_params params) returns (object_metadata output);    
    
	    /* Input parameters for the "compute_domains_params" function.
			string genome;
			string genome_workspace;
			list<tuple<string,string>> proteins;
			workspace_id workspace;
		*/
		typedef structure {
			string genome;
			string genome_workspace;
			list<tuple<string,string>> proteins;
			workspace_id workspace;
	    } compute_domains_params;
	    
	    /*
			Computes domains for either a genome or a list of proteins
	    */

16. funcdef add_feature_translation(add_feature_translation_params input) returns (object_metadata genomeMeta);
    
	    /* A link between a KBase gene ID and the ID for the same gene in another database
		
			string foreign_id - ID of the gene in another database
			feature_id feature - ID of the gene in KBase
			
		*/
	    typedef tuple<string foreign_id,feature_id feature> translation; 
	    
	    /* Input parameters for the "add_feature_translation" function.
		
			genome_id genome - ID of the genome into which the new aliases are to be loaded (a required argument)
			workspace_id workspace - ID of the workspace containing the target genome (a required argument)
			list<translation> translations - list of translations between KBase gene IDs and gene IDs in another database (a required argument)
			string id_type - type of the IDs being loaded (e.g. KEGG, NCBI) (a required argument)
			string auth - the authentication token of the KBase account changing workspace permissions; must have 'admin' privelages to workspace (an optional argument; user is "public" if auth is not provided)
			
		*/
	    typedef structure {
			genome_id genome;
			workspace_id workspace;
			list<translation> translations;
			string id_type;
			string auth;
			bool overwrite;
	    } add_feature_translation_params;
	    /*
	        Adds a new set of alternative feature IDs to the specified genome typed object
	    */

17. funcdef genome_to_fbamodel(genome_to_fbamodel_params input) returns (object_metadata modelMeta);
    
	    /* Input parameters for the "genome_to_fbamodel" function.
			genome_id genome - ID of the genome for which a model is to be built (a required argument)
			workspace_id genome_workspace - ID of the workspace containing the target genome (an optional argument; default is the workspace argument)
			template_id templatemodel - 
			workspace_id templatemodel_workspace - 
			bool probannoOnly - a boolean indicating if only the probabilistic annotation should be used in building the model (an optional argument; default is '0')
			fbamodel_id model - ID that should be used for the newly constructed model (an optional argument; default is 'undef')
			bool coremodel - indicates that a core model should be constructed instead of a genome scale model (an optional argument; default is '0')
			workspace_id workspace - ID of the workspace where the newly developed model will be stored; also the default assumed workspace for input objects (a required argument)
			string auth - the authentication token of the KBase account changing workspace permissions; must have 'admin' privelages to workspace (an optional argument; user is "public" if auth is not provided)
			
		*/
	    typedef structure {
			genome_id genome;
			workspace_id genome_workspace;
			template_id templatemodel;
			workspace_id templatemodel_workspace;
			fbamodel_id model;
			bool coremodel;
			workspace_id workspace;
			string auth;
			bool fulldb;
	    } genome_to_fbamodel_params;
	    /*
	        Build a genome-scale metabolic model based on annotations in an input genome typed object
	    */

18. funcdef translate_fbamodel(translate_fbamodel_params input) returns (object_metadata modelMeta);
	
		/* Input parameters for the "translate_fbamodel" function.
			gencomp
			gencomp_workspace
			fbamodel_id model;
			fbamodel_id model_workspace;
		*/
	    typedef structure {
			string protcomp;
			string protcomp_workspace;
			string model;
			string model_workspace;
			workspace_id workspace;
	    } translate_fbamodel_params;
	    /*
	        Translate an existing model to a new genome based on the genome comparison object
	    */

19. funcdef build_pangenome(build_pangenome_params input) returns (object_metadata output);    

		/* Input parameters for the "translate_fbamodel" function.
			gencomp
			gencomp_workspace
			fbamodel_id model;
			fbamodel_id model_workspace;
		*/
	    typedef structure {
			list<string> genomes;
			list<string> genome_workspace;
			workspace_id workspace;
	    } build_pangenome_params;
	    /*
	        Translate an existing model to a new genome based on the genome comparison object
	    */
    
20. funcdef genome_heatmap_from_pangenome(genome_heatmap_from_pangenome_params input) returns (heat_map_matrix output);
    
	    typedef structure {
	    	bool is_refs;
			list<string> labels;
			list<list<float>> matrix;
	    } heat_map_matrix;
	    
	    typedef structure {
			string pangenome;
			string pangenome_workspace;
			string workspace;
	    } genome_heatmap_from_pangenome_params;
	    /*
	        Builds a comparason matrix for genomes included in a pangenome object
	    */
	    authentication required;

21. funcdef ortholog_family_from_pangenome(ortholog_family_from_pangenome_params input) returns (ortholog_data output);

		/*gene ID,gene ref,protein sequence,function,score*/
		typedef structure {
			list<tuple<string,string,string,string,float>> gene_data;
			heat_map_matrix protein_heatmap;
		} ortholog_data;
		
		typedef structure {
			string pangenome;
			string pangenome_workspace;
			string orthologid;
			string workspace;
		} ortholog_family_from_pangenome_params;
		/*
		Returns more detailed data from a single ortholog family from a pangenome object
		*/

22. funcdef pangenome_to_proteome_comparison(pangenome_to_proteome_comparison_params input) returns (object_metadata output);    
	
		typedef structure {
			string pangenome;
			string pangenome_workspace;
			string outputid;
			string workspace;
	    } pangenome_to_proteome_comparison_params;
	    /*
	        Builds a proteome comparison object from a pangenome object
	    */

23. funcdef import_fbamodel(import_fbamodel_params input) returns (object_metadata modelMeta);
	
		/* Input parameters for the "import_fbamodel" function.
			genome_id genome - ID of the genome for which a model is to be built (a required argument)
			workspace_id genome_workspace - ID of the workspace containing the target genome (an optional argument; default is the workspace argument)
			string biomass - biomass equation for model (an essential argument)
			list<tuple<string id,string direction,string compartment,string gpr> reactions - list of reactions to appear in imported model (an essential argument)
			fbamodel_id model - ID that should be used for the newly imported model (an optional argument; default is 'undef')
			workspace_id workspace - ID of the workspace where the newly developed model will be stored; also the default assumed workspace for input objects (a required argument)
			bool ignore_errors - ignores missing genes or reactions and imports model anyway
			string auth - the authentication token of the KBase account changing workspace permissions; must have 'admin' privelages to workspace (an optional argument; user is "public" if auth is not provided)
			
		*/
	    typedef structure {
			genome_id genome;
			workspace_id genome_workspace;
			string biomass;
			list<tuple<string id,string direction,string compartment,string gpr>> reactions;
			fbamodel_id model;
			workspace_id workspace;
			bool ignore_errors;
			string auth;
			bool overwrite;
	    } import_fbamodel_params;
	    /*
	        Import a model from an input table of model and gene IDs
	    */

24. funcdef export_fbamodel(export_fbamodel_params input) returns (string output);    
	
	    /* Input parameters for the "export_fbamodel" function.
		
			fbamodel_id model - ID of the model to be exported (a required argument)
			workspace_id workspace - workspace containing the model to be exported (a required argument)
			fba_id fba - A FBA object related to the model. (an optional argument)
			string format - format to which the model should be exported (sbml, html, json, readable, cytoseed) (a required argument)
			string auth - the authentication token of the KBase account changing workspace permissions; must have 'admin' privelages to workspace (an optional argument; user is "public" if auth is not provided)
			
		*/
	    typedef structure {
			fbamodel_id model;
			workspace_id workspace;
			list<fba_id> fbas;
			string format;
			string auth;
	    } export_fbamodel_params;
	    /*
	        This function exports the specified FBAModel to a specified format (sbml,html)
	    */

25. funcdef export_object(export_object_params input) returns (string output);    
    
	    /* Input parameters for the "export_object" function.
			workspace_ref reference - reference of object to print in html (a required argument)
			string type - type of the object to be exported (a required argument)
			string format - format to which data should be exported (an optional argument; default is html)
			string auth - the authentication token of the KBase account changing workspace permissions; must have 'admin' privelages to workspace (an optional argument; user is "public" if auth is not provided)
			
		*/
	    typedef structure {
			workspace_ref reference;
			string type;
			string format;
	    	string auth;
	    } export_object_params;
	    /*
	        This function prints the object pointed to by the input reference in the specified format
	    */

26. funcdef export_genome(export_genome_params input) returns (string output);    
	
		/* Input parameters for the "export_genome" function.
			genome_id genome - ID of the genome to be exported (a required argument)
			workspace_id workspace - workspace containing the model to be exported (a required argument)
			string format - format to which the model should be exported (sbml, html, json, readable, cytoseed) (a required argument)
			string auth - the authentication token of the KBase account changing workspace permissions; must have 'admin' privelages to workspace (an optional argument; user is "public" if auth is not provided)
			
		*/
		typedef structure {
			genome_id genome;
			workspace_id workspace;
			string format;
			string auth;
		} export_genome_params;
		/*
		This function exports the specified FBAModel to a specified format (sbml,html)
		*/
 
27. funcdef adjust_model_reaction(adjust_model_reaction_params input) returns (object_metadata modelMeta);  
	
	    /* Input parameters for the "adjust_model_reaction" function.
			fbamodel_id model - ID of model to be adjusted
			workspace_id workspace - workspace containing model to be adjusted
			list<reaction_id> reaction - List of IDs of reactions to be added, removed, or adjusted
			list<string> direction - directions to set for reactions being added or adjusted
			list<compartment_id> compartment - IDs of compartment containing reaction being added or adjusted
			list<int> compartmentIndex - indexes of compartment containing reaction being altered or adjusted
			list<string> gpr - array specifying gene-protein-reaction association(s)
			bool removeReaction - boolean indicating listed reaction(s) should be removed
			bool addReaction - boolean indicating reaction(s) should be added
			bool overwrite - boolean indicating whether or not to overwrite model object in the workspace
			string auth - the authentication token of the KBase account changing workspace permissions; must have 'admin' privelages to workspace (an optional argument; user is "public" if auth is not provided)
	
			For all of the lists above, if only one element is specified it is assumed the user wants to apply the same
			to all the listed reactions.
			
		*/
	    typedef structure {
			fbamodel_id model;
			workspace_id workspace;
			list<reaction_id> reaction;
			list<string> direction;
			list<compartment_id> compartment;
			list<int> compartmentIndex;
			list<string> gpr;
			bool removeReaction;
			bool addReaction;
			bool overwrite;
			string auth;
	    } adjust_model_reaction_params;
	    /*
	        Enables the manual addition of a reaction to model
	    */
28. funcdef adjust_biomass_reaction(adjust_biomass_reaction_params input) returns (object_metadata modelMeta);   
    
	    /* Input parameters for the "adjust_biomass_reaction" function.
			fbamodel_id model - ID of model to be adjusted
			workspace_id workspace - workspace containing model to be adjusted
			biomass_id biomass - ID of biomass reaction to adjust
			list<float> coefficients - coefficient of biomass compound
			list<compound_id> compounds - ID of biomass compound to adjust in biomass
			list<compartment_id> compartments - ID of compartment containing compound to adjust in biomass
			list<int> compartmentIndecies - index of compartment containing compound to adjust in biomass
			string auth - the authentication token of the KBase account changing workspace permissions; must have 'admin' privelages to workspace (an optional argument; user is "public" if auth is not provided)
		*/
	    typedef structure {
			fbamodel_id model;
			workspace_id workspace;
			biomass_id biomass;
			list<float> coefficients;
			list<compound_id> compounds;
			list<compartment_id> compartments;
			list<int> compartmentIndecies;
			string auth;
	    } adjust_biomass_reaction_params;
	    /*
	        Enables the manual adjustment of model biomass reaction
	    */
    
    
###Code relating to flux balance analysis


29. funcdef addmedia(addmedia_params input) returns (object_metadata mediaMeta);

	    /* Input parameters for the "addmedia" function.
			media_id media - ID of the new media to be added (a required argument)
			workspace_id workspace - workspace where the new media should be created (a required argument)
			string name - name of the new media to be added  (an optional argument: default is the value of the media argument)
			bool isDefined - boolean indicating if new media is defined (an optional argument: default is '0')
			bool isMinimal - boolean indicating if new media is mininal (an optional argument: default is '0')
			string type - the type of the new media (e.g. Biolog) (an optional argument: default is 'unknown')
			list<string> compounds - a list of the compounds to be included in the new media (a required argument)
			list<float> concentrations - a list of the concentrations for compounds in the new media (an optional argument: default is 0.001 M for all compounds)
			list<float> maxflux - a list of the maximum uptakes for compounds in the new media (an optional argument: default is 100 mmol/hr gm CDW for all compounds)
			list<float> minflux - a list of the minimum uptakes for compounds in the new media (an optional argument: default is 100 mmol/hr gm CDW for all compounds)
			string auth - the authentication token of the KBase account changing workspace permissions; must have 'admin' privelages to workspace (an optional argument; user is "public" if auth is not provided)
			
		*/
	    typedef structure {
			media_id media;
			workspace_id workspace;
			string name;
			bool isDefined;
			bool isMinimal;
			string type;
			list<string> compounds;
			list<float> concentrations;
			list<float> maxflux;
			list<float> minflux;
			bool overwrite;
			string auth;
	    } addmedia_params;
	    /*
	        Add media condition to workspace
	    */
 
30. funcdef export_media(export_media_params input) returns (string output);    
    
	    /* Input parameters for the "export_media" function.
			media_id media - ID of the media to be exported (a required argument)
			workspace_id workspace - workspace containing the media to be exported (a required argument)
			string format - format to which the media should be exported (html, json, readable) (a required argument)
			string auth - the authentication token of the KBase account changing workspace permissions; must have 'admin' privelages to workspace (an optional argument; user is "public" if auth is not provided)
			
		*/
	    typedef structure {
			media_id media;
			workspace_id workspace;
			string format;
			string auth;
	    } export_media_params;
	    /*
	        Exports media in specified format (html,readable)
	    */

31. funcdef runfba(runfba_params input) returns (object_metadata fbaMeta);    
    
	    /* Input parameters for the "addmedia" function.
			fbamodel_id model - ID of the model that FBA should be run on (a required argument)
			workspace_id model_workspace - workspace where model for FBA should be run (an optional argument; default is the value of the workspace argument)
			FBAFormulation formulation - a hash specifying the parameters for the FBA study (an optional argument)
			bool fva - a flag indicating if flux variability should be run (an optional argument: default is '0')
			bool simulateko - a flag indicating if flux variability should be run (an optional argument: default is '0')
			bool minimizeflux - a flag indicating if flux variability should be run (an optional argument: default is '0')
			bool findminmedia - a flag indicating if flux variability should be run (an optional argument: default is '0')
			string notes - a string of notes to attach to the FBA study (an optional argument; defaul is '')
			fba_id fba - ID under which the FBA results should be saved (an optional argument; defaul is 'undef')
			workspace_id workspace - workspace where FBA results will be saved (a required argument)
			bool add_to_model - a flag indicating if the FBA study should be attached to the model to support viewing results (an optional argument: default is '0')
			string auth - the authentication token of the KBase account changing workspace permissions; must have 'admin' privelages to workspace (an optional argument; user is "public" if auth is not provided)
			
		*/
	    typedef structure {
	    	fbamodel_id model;
			workspace_id model_workspace;
			FBAFormulation formulation;
			bool fva;
			bool simulateko;
			bool minimizeflux;
			bool findminmedia;
			string notes;
			fba_id fba;
			workspace_id workspace;
			string auth;
			bool overwrite;
			bool add_to_model;
	    } runfba_params;
	    /*
	        Run flux balance analysis and return ID of FBA object with results 
	    */

32. funcdef quantitative_optimization(quantitative_optimization_params input) returns (object_metadata output);
    
	    /* Input parameters for the "addmedia" function.
			fbamodel_id model - ID of the model that FBA should be run on (a required argument)
			workspace_id model_workspace - workspace where model for FBA should be run (an optional argument; default is the value of the workspace argument)
			FBAFormulation formulation - a hash specifying the parameters for the FBA study (an optional argument)
			fbamodel_id outputid - ID of model to be saved with quantitative optimization solution (an optional argument)
			workspace_id workspace - workspace where all output objects will be saved (a required argument)
			string biomass - ID of biomass reaction as target for quantitative optimization (an optional argument)
			
		*/
	    typedef structure {
	    	fbamodel_id model;
			workspace_id model_workspace;
			FBAFormulation formulation;
			fbamodel_id outputid;
			workspace_id workspace;
			string biomass;		
	    } quantitative_optimization_params;
	    /*
	        Identify ways to adjust model to quantitatively match specified uptake, growth, and excretion constraints
	    */
    
33.  funcdef generate_model_stats(generate_model_stats_params input) returns (model_statistics output);
   
	    /* Input parameters for the "generate_model_stats" function.
			fbamodel_id model - ID of the models that FBA should be run on (a required argument)
			workspace_id model_workspace - workspaces where model for FBA should be run (an optional argument; default is the value of the workspace argument)
			
		*/
	    typedef structure {
	    	fbamodel_id model;
			workspace_id model_workspace;
	    } generate_model_stats_params;
	    
	    typedef structure {
	    	string name;
	    	string class;
	    	string subclass;
	    	int genes;
	    	int reactions;
	    	int model_genes;
	    	int minimal_essential_genes;
	    	int complete_essential_genes;
			int minimal_essential_reactions;
	    	int complete_essential_reactions;
	    	int minimal_blocked_reactions;
	    	int complete_blocked_reactions;
	    	int minimal_variable_reactions;
	    	int complete_variable_reactions;
	    } subsystem_statistics;
	    
	    typedef structure {
	    	int total_reactions;
	    	int total_genes;
	    	int total_compounds;
	    	int extracellular_compounds;
	    	int intracellular_compounds;
	    	int transport_reactions;
	    	int subsystem_reactions;
	    	int subsystem_genes;
	    	int spontaneous_reactions;
	    	int reactions_with_genes;
	    	int gapfilled_reactions;
	    	int model_genes;
	    	int minimal_essential_genes;
	    	int complete_essential_genes;
			int minimal_essential_reactions;
	    	int complete_essential_reactions;
	    	int minimal_blocked_reactions;
	    	int complete_blocked_reactions;
	    	int minimal_variable_reactions;
	    	int complete_variable_reactions;
	    	
	    	bool growth_complete_media;
	    	bool growth_minimal_media;
	    	
	    	list<subsystem_statistics> subsystems;
	    } model_statistics;
	    
	    /*
	        Generate statistics with model and associated genome properties
	    */

34. funcdef minimize_reactions(minimize_reactions_params input) returns (object_metadata fbaMeta);   
    
	    /* Input parameters for the "minimize_reactions" function.
			fbamodel_id model - ID of the model that FBA should be run on (a required argument)
			workspace_id model_workspace - workspace where model for FBA should be run (an optional argument; default is the value of the workspace argument)
			workspace_id workspace - workspace where FBA results will be saved (a required argument)
			FBAFormulation formulation - a hash specifying the parameters for the FBA study (an optional argument)
			list<string> reactions - list of model reactions to be minimized (an optional argument)
			bool all_model_reactions - minimize all reactions in the model (default is 'false' unless 'reactions' list is empty)
			mapping<string,float> reaction_costs - hash of costs for each reaction to be minimized (default is '1' for every reaction)
			fba_id output_id - id to which FBA result should be saved
					
		*/
	    typedef structure {
	    	fbamodel_id model;
			workspace_id model_workspace;
			workspace_id workspace;
			FBAFormulation formulation;
			list<string> reactions;
			bool all_model_reactions;
			mapping<string,float> reaction_costs;
			fba_id output_id;
	    } minimize_reactions_params;
	    /*
	        Minimize the specified set of reactions while maintaining the FBA objective above a specified threshold
	    */
35. funcdef export_fba(export_fba_params input) returns (string output);    
    
	    /* Input parameters for the "addmedia" function.
		
			fba_id fba - ID of the FBA study to be exported (a required argument)
			workspace_id workspace - workspace where FBA study is stored (a required argument)
			string format - format to which the FBA study should be exported (i.e. html, json, readable) (a required argument)
			string auth - the authentication token of the KBase account changing workspace permissions; must have 'admin' privelages to workspace (an optional argument; user is "public" if auth is not provided)
			
		*/
	    typedef structure {
			fba_id fba;
			workspace_id workspace;
			string format;
			string auth;
	    } export_fba_params;
	    /*
	        Export an FBA solution for viewing
	    */

    
    

###Code relating to phenotype simulation and reconciliation


36. funcdef import_phenotypes(import_phenotypes_params input) returns (object_metadata output);

	    /* Input parameters for the "import_phenotypes" function.
		
			phenotype_set_id phenotypeSet - ID to be used for the imported phenotype set (an optional argument: default is 'undef')
			workspace_id workspace - workspace where the imported phenotype set should be stored (a required argument)
			genome_id genome - genome the imported phenotypes should be associated with (a required argument)
			workspace_id genome_workspace - workspace containing the genome object (an optional argument: default is value of the workspace argument)
			list<Phenotype> phenotypes - list of observed phenotypes to be imported (a required argument)
			bool ignore_errors - a flag indicating that any errors encountered during the import should be ignored (an optional argument: default is '0')
			string auth - the authentication token of the KBase account changing workspace permissions; must have 'admin' privelages to workspace (an optional argument; user is "public" if auth is not provided)
			
		*/
	    typedef structure {
			phenotype_set_id phenotypeSet;
			workspace_id workspace;
			genome_id genome;
			workspace_id genome_workspace;
			list<Phenotype> phenotypes;
			string name;
			string source;
			bool ignore_errors;
			string auth;
	    } import_phenotypes_params;
	    /*
	        Loads the specified phenotypes into the workspace
	    */

37. funcdef simulate_phenotypes (simulate_phenotypes_params input) returns (object_metadata output);    
    
		/* Input parameters for the "simulate_phenotypes" function.
		
			fbamodel_id model - ID of the model to be used for the simulation (a required argument)
			workspace_id model_workspace - workspace containing the model for the simulation (an optional argument: default is value of workspace argument)
			phenotype_set_id phenotypeSet - ID of the phenotypes set to be simulated (a required argument)
			workspace_id phenotypeSet_workspace - workspace containing the phenotype set to be simulated (an optional argument: default is value of workspace argument)
			FBAFormulation formulation - parameters for the simulation flux balance analysis (an optional argument: default is 'undef')
			string notes - string of notes to associate with the phenotype simulation (an optional argument: default is '')
			phenotypeSimulationSet_id phenotypeSimulationSet - ID of the phenotype simulation set to be generated (an optional argument: default is 'undef')
			workspace_id workspace - workspace where the phenotype simulation set should be saved (a required argument)
			string auth - the authentication token of the KBase account changing workspace permissions; must have 'admin' privelages to workspace (an optional argument; user is "public" if auth is not provided)
			bool all_transporters - Set to TRUE if you want to add transporters for ALL media in the phenotypeset before simulating
			bool positive_transporters - Set to TRUE if you want to add transporters for POSITIVE (non-zero growth) media only before simulating
		*/
		typedef structure {
			fbamodel_id model;
			workspace_id model_workspace;
			phenotype_set_id phenotypeSet;
			workspace_id phenotypeSet_workspace;
			FBAFormulation formulation;
			string notes;
			phenotypeSimulationSet_id phenotypeSimulationSet;
			workspace_id workspace;
			bool overwrite;
			string auth;
			bool all_transporters;
			bool positive_transporters;
		} simulate_phenotypes_params;
		/*
		Simulates the specified phenotype set
		*/
    
38. funcdef add_media_transporters (add_media_transporters_params input) returns (object_metadata output);
    
	    /* Input parameters for the add_media_transporters function.
	    	phenotype_set_id phenotypeSet - ID for a phenotype set (required)
		    workspace_id phenotypeSet_workspace - ID for the workspace in which the phenotype set is found
			fbamodel_id model - Model to which to add the transport reactions (required)
			workspace_id model_workspace - workspace containing the input model
			fbamodel_id outmodel - Name of output model (with transporters added)
			workspace_id workspace - workspace where the modified model should be saved
			bool overwrite - Overwrite or not
			string auth - Auth string
			bool all_transporters - Add transporters for ALL media in the phenotypeset
			bool positive_transporters - Add transporters for only POSITIVE (non-zero growth) media in the phenotype set
	
	    */
	    typedef structure {
			phenotype_set_id phenotypeSet;
			workspace_id phenotypeSet_workspace;
			fbamodel_id model;
			workspace_id model_workspace;
			fbamodel_id outmodel;
			workspace_id workspace;
			bool overwrite;
			string auth;
			bool all_transporters;
			bool positive_transporters;
	    } add_media_transporters_params;
	
	    /*
	         Adds transporters for media in a PhenotypeSet to a model
		 
	    */

39. funcdef export_phenotypeSimulationSet (export_phenotypeSimulationSet_params input) returns (string output);    
	
	    /* Input parameters for the "export_phenotypeSimulationSet" function.
			phenotypeSimulationSet_id phenotypeSimulationSet - ID of the phenotype simulation set to be exported (a required argument)
			workspace_id workspace - workspace where the phenotype simulation set is stored (a required argument)
			string format - format to which phenotype simulation set should be exported (html, json)
			string auth - the authentication token of the KBase account changing workspace permissions; must have 'admin' privelages to workspace (an optional argument; user is "public" if auth is not provided)
			
		*/
	    typedef structure {
			phenotypeSimulationSet_id phenotypeSimulationSet;
			workspace_id workspace;
			string format;
			string auth;
	    } export_phenotypeSimulationSet_params;
	    /*
	        Export a PhenotypeSimulationSet for viewing
	    */

40. funcdef integrate_reconciliation_solutions(integrate_reconciliation_solutions_params input) returns (object_metadata modelMeta);    
    
	    /* Input parameters for the "integrate_reconciliation_solutions" function.
		
			fbamodel_id model - ID of model for which reconciliation solutions should be integrated (a required argument)
			workspace_id model_workspace - workspace containing model for which solutions should be integrated (an optional argument: default is value of workspace argument)
			list<gapfillsolution_id> gapfillSolutions - list of gapfill solutions to be integrated (a required argument)
			list<gapgensolution_id> gapgenSolutions - list of gapgen solutions to be integrated (a required argument)
			fbamodel_id out_model - ID to which modified model should be saved (an optional argument: default is value of workspace argument)
			workspace_id workspace - workspace where modified model should be saved (a required argument)
			string auth - the authentication token of the KBase account changing workspace permissions; must have 'admin' privelages to workspace (an optional argument; user is "public" if auth is not provided)
			
		*/
	    typedef structure {
			fbamodel_id model;
			workspace_id model_workspace;
			list<gapfillsolution_id> gapfillSolutions;
			list<gapgensolution_id> gapgenSolutions;
			fbamodel_id out_model;
			workspace_id workspace;
			string auth;
			bool overwrite;
	    } integrate_reconciliation_solutions_params;
	    /*
	        Integrates the specified gapfill and gapgen solutions into the specified model
	    */

    
### Code relating to queuing long running jobs

41. funcdef queue_runfba(queue_runfba_params input) returns (JobObject job);

	    /* Input parameters for the "queue_runfba" function.
			fbamodel_id model - ID of the model that FBA should be run on (a required argument)
			workspace_id model_workspace - workspace where model for FBA should be run (an optional argument; default is the value of the workspace argument)
			FBAFormulation formulation - a hash specifying the parameters for the FBA study (an optional argument)
			bool fva - a flag indicating if flux variability should be run (an optional argument: default is '0')
			bool simulateko - a flag indicating if flux variability should be run (an optional argument: default is '0')
			bool minimizeflux - a flag indicating if flux variability should be run (an optional argument: default is '0')
			bool findminmedia - a flag indicating if flux variability should be run (an optional argument: default is '0')
			string notes - a string of notes to attach to the FBA study (an optional argument; defaul is '')
			fba_id fba - ID under which the FBA results should be saved (an optional argument; defaul is 'undef')
			workspace_id workspace - workspace where FBA results will be saved (a required argument)
			bool add_to_model - a flag indicating if the FBA study should be attached to the model to support viewing results (an optional argument: default is '0')
			string auth - the authentication token of the KBase account changing workspace permissions; must have 'admin' privelages to workspace (an optional argument; user is "public" if auth is not provided)
			
		*/
	    typedef structure {
	    	fbamodel_id model;
			workspace_id model_workspace;
			FBAFormulation formulation;
			bool fva;
			bool simulateko;
			bool minimizeflux;
			bool findminmedia;
			string notes;
			fba_id fba;
			workspace_id workspace;
			string auth;
			bool overwrite;
			bool add_to_model;
	    } queue_runfba_params;
		/*
	        Queues an FBA job in a single media condition
	    */

42. funcdef queue_gapfill_model(gapfill_model_params input) returns (JobObject job);

	Uses the same as gapfill_model
	
43. funcdef gapfill_model(gapfill_model_params input) returns (object_metadata modelMeta);
   
		/* Input parameters for the "queue_gapfill_model" function.
			fbamodel_id model - ID of the model that gapfill should be run on (a required argument)
			workspace_id model_workspace - workspace where model for gapfill should be run (an optional argument; default is the value of the workspace argument)
			GapfillingFormulation formulation - a hash specifying the parameters for the gapfill study (an optional argument)
			phenotype_set_id phenotypeSet - ID of a phenotype set against which gapfilled model should be simulated (an optional argument: default is 'undef')
			workspace_id phenotypeSet_workspace - workspace containing phenotype set to be simulated (an optional argument; default is the value of the workspace argument)
			bool integrate_solution - a flag indicating if the first solution should be integrated in the model (an optional argument: default is '0')
			list<string> target_reactions - a list of reactions to activate with gapfilling
			fbamodel_id out_model - ID where the gapfilled model will be saved (an optional argument: default is 'undef')
			gapfill_id gapFill - ID to which gapfill solution will be saved (an optional argument: default is 'undef')
			workspace_id workspace - workspace where gapfill results will be saved (a required argument)
			int timePerSolution - maximum time to spend to obtain each solution
			int totalTimeLimit - maximum time to spend to obtain all solutions
			string auth - the authentication token of the KBase account changing workspace permissions; must have 'admin' privelages to workspace (an optional argument; user is "public" if auth is not provided)
			bool completeGapfill - boolean indicating that all inactive reactions should be gapfilled
		*/
	    typedef structure {
			fbamodel_id model;
			workspace_id model_workspace;
			GapfillingFormulation formulation;
			phenotype_set_id phenotypeSet;
			workspace_id phenotypeSet_workspace;
			bool integrate_solution;
			list<string> target_reactions;
			fbamodel_id out_model;
			workspace_id workspace;
			gapfill_id gapFill;
			int timePerSolution;
			int totalTimeLimit;
			string auth;
			bool overwrite;
			bool completeGapfill;
	    } gapfill_model_params;
	    /*
	        Queues an FBAModel gapfilling job in single media condition
	    */

44. funcdef queue_gapgen_model(gapgen_model_params input) returns (JobObject job);    

	same as gapgen_model

45. funcdef gapgen_model(gapgen_model_params input) returns (object_metadata modelMeta);

	    /* Input parameters for the "queue_gapgen_model" function.
			fbamodel_id model - ID of the model that gapgen should be run on (a required argument)
			workspace_id model_workspace - workspace where model for gapgen should be run (an optional argument; default is the value of the workspace argument)
			GapgenFormulation formulation - a hash specifying the parameters for the gapgen study (an optional argument)
			phenotype_set_id phenotypeSet - ID of a phenotype set against which gapgened model should be simulated (an optional argument: default is 'undef')
			workspace_id phenotypeSet_workspace - workspace containing phenotype set to be simulated (an optional argument; default is the value of the workspace argument)
			bool integrate_solution - a flag indicating if the first solution should be integrated in the model (an optional argument: default is '0')
			fbamodel_id out_model - ID where the gapgened model will be saved (an optional argument: default is 'undef')
			gapgen_id gapGen - ID to which gapgen solution will be saved (an optional argument: default is 'undef')
			workspace_id workspace - workspace where gapgen results will be saved (a required argument)
			int timePerSolution - maximum time to spend to obtain each solution
			int totalTimeLimit - maximum time to spend to obtain all solutions
			string auth - the authentication token of the KBase account changing workspace permissions; must have 'admin' privelages to workspace (an optional argument; user is "public" if auth is not provided)
			
		*/
	    typedef structure {
			fbamodel_id model;
			workspace_id model_workspace;
			GapgenFormulation formulation;
			phenotype_set_id phenotypeSet;
			workspace_id phenotypeSet_workspace;
			bool integrate_solution;
			fbamodel_id out_model;
			workspace_id workspace;
			gapgen_id gapGen;
			string auth;
			int timePerSolution;
			int totalTimeLimit;
			bool overwrite;
	    } gapgen_model_params;
	    /*
	        Queues an FBAModel gapfilling job in single media condition
	    */

46. funcdef queue_wildtype_phenotype_reconciliation(wildtype_phenotype_reconciliation_params input) returns (JobObject job);    

	    /* Input parameters for the "queue_wildtype_phenotype_reconciliation" function.
			fbamodel_id model - ID of the model that reconciliation should be run on (a required argument)
			workspace_id model_workspace - workspace where model for reconciliation should be run (an optional argument; default is the value of the workspace argument)
			FBAFormulation formulation - a hash specifying the parameters for the reconciliation study (an optional argument)
			GapfillingFormulation gapfill_formulation - a hash specifying the parameters for the gapfill study (an optional argument)
			GapgenFormulation gapgen_formulation - a hash specifying the parameters for the gapgen study (an optional argument)
			phenotype_set_id phenotypeSet - ID of a phenotype set against which reconciled model should be simulated (an optional argument: default is 'undef')
			workspace_id phenotypeSet_workspace - workspace containing phenotype set to be simulated (an optional argument; default is the value of the workspace argument)
			fbamodel_id out_model - ID where the reconciled model will be saved (an optional argument: default is 'undef')
			list<gapgen_id> gapGens - IDs of gapgen solutions (an optional argument: default is 'undef')
			list<gapfill_id> gapFills - IDs of gapfill solutions (an optional argument: default is 'undef')
			bool queueSensitivityAnalysis - flag indicating if sensitivity analysis should be queued to run on solutions (an optional argument: default is '0')
			bool queueReconciliationCombination - flag indicating if reconcilication combination should be queued to run on solutions (an optional argument: default is '0')
			workspace_id workspace - workspace where reconciliation results will be saved (a required argument)
			string auth - the authentication token of the KBase account changing workspace permissions; must have 'admin' privelages to workspace (an optional argument; user is "public" if auth is not provided)
			
		*/
	    typedef structure {
			fbamodel_id model;
			workspace_id model_workspace;
			FBAFormulation fba_formulation;
			GapfillingFormulation gapfill_formulation;
			GapgenFormulation gapgen_formulation;
			phenotype_set_id phenotypeSet;
			workspace_id phenotypeSet_workspace;
			fbamodel_id out_model;
			workspace_id workspace;
			list<gapfill_id> gapFills;
			list<gapgen_id> gapGens;
			bool queueSensitivityAnalysis;
			bool queueReconciliationCombination;
			string auth;
			bool overwrite;
	    } wildtype_phenotype_reconciliation_params;
	    /*
	        Queues an FBAModel reconciliation job
	    */

47. funcdef queue_reconciliation_sensitivity_analysis(wildtype_phenotype_reconciliation_params input) returns (JobObject job);
    
	    /* Input parameters for the "queue_reconciliation_sensitivity_analysis" function.
			fbamodel_id model - ID of the model that sensitivity analysis should be run on (a required argument)
			workspace_id model_workspace - workspace where model for sensitivity analysis should be run (an optional argument; default is the value of the workspace argument)
			FBAFormulation formulation - a hash specifying the parameters for the sensitivity analysis study (an optional argument)
			GapfillingFormulation gapfill_formulation - a hash specifying the parameters for the gapfill study (an optional argument)
			GapgenFormulation gapgen_formulation - a hash specifying the parameters for the gapgen study (an optional argument)
			phenotype_set_id phenotypeSet - ID of a phenotype set against which sensitivity analysis model should be simulated (an optional argument: default is 'undef')
			workspace_id phenotypeSet_workspace - workspace containing phenotype set to be simulated (an optional argument; default is the value of the workspace argument)
			fbamodel_id out_model - ID where the sensitivity analysis model will be saved (an optional argument: default is 'undef')
			list<gapgen_id> gapGens - IDs of gapgen solutions (an optional argument: default is 'undef')
			list<gapfill_id> gapFills - IDs of gapfill solutions (an optional argument: default is 'undef')
			bool queueReconciliationCombination - flag indicating if sensitivity analysis combination should be queued to run on solutions (an optional argument: default is '0')
			workspace_id workspace - workspace where sensitivity analysis results will be saved (a required argument)
			string auth - the authentication token of the KBase account changing workspace permissions; must have 'admin' privelages to workspace (an optional argument; user is "public" if auth is not provided)
			
		*/
	    typedef structure {
			fbamodel_id model;
			workspace_id workspace;
			phenotype_set_id phenotypeSet;
			
			FBAFormulation fba_formulation;
			workspace_id model_workspace;
			workspace_id phenotypeSet_workspace;
			
			list<gapfill_id> gapFills;
			list<gapgen_id> gapGens;
			bool queueReconciliationCombination;
			string auth;
			bool overwrite;
	    } queue_reconciliation_sensitivity_analysis_params;
	    /*
	        Queues an FBAModel reconciliation job
	    */

48. funcdef queue_combine_wildtype_phenotype_reconciliation(combine_wildtype_phenotype_reconciliation_params input) returns (JobObject job);
    
	    /* Input parameters for the "queue_combine_wildtype_phenotype_reconciliation" function.
			fbamodel_id model - ID of the model that solution combination should be run on (a required argument)
			workspace_id model_workspace - workspace where model for solution combination should be run (an optional argument; default is the value of the workspace argument)
			FBAFormulation formulation - a hash specifying the parameters for the solution combination study (an optional argument)
			GapfillingFormulation gapfill_formulation - a hash specifying the parameters for the gapfill study (an optional argument)
			GapgenFormulation gapgen_formulation - a hash specifying the parameters for the gapgen study (an optional argument)
			phenotype_set_id phenotypeSet - ID of a phenotype set against which solution combination model should be simulated (an optional argument: default is 'undef')
			workspace_id phenotypeSet_workspace - workspace containing phenotype set to be simulated (an optional argument; default is the value of the workspace argument)
			fbamodel_id out_model - ID where the solution combination model will be saved (an optional argument: default is 'undef')
			list<gapgen_id> gapGens - IDs of gapgen solutions (an optional argument: default is 'undef')
			list<gapfill_id> gapFills - IDs of gapfill solutions (an optional argument: default is 'undef')
			workspace_id workspace - workspace where solution combination results will be saved (a required argument)
			int timePerSolution - maximum time spent per solution
			int totalTimeLimit - maximum time allowed to work on problem
			string auth - the authentication token of the KBase account changing workspace permissions; must have 'admin' privelages to workspace (an optional argument; user is "public" if auth is not provided)
			
		*/
	    typedef structure {
			fbamodel_id model;
			workspace_id model_workspace;
			FBAFormulation fba_formulation;
			GapfillingFormulation gapfill_formulation;
			GapgenFormulation gapgen_formulation;
			phenotype_set_id phenotypeSet;
			workspace_id phenotypeSet_workspace;
			fbamodel_id out_model;
			workspace_id workspace;
			list<gapfill_id> gapFills;
			list<gapgen_id> gapGens;
			string auth;
			bool overwrite;
	    } combine_wildtype_phenotype_reconciliation_params;
	    /*
	        Queues an FBAModel reconciliation job
	    */

49. funcdef run_job(run_job_params input) returns (JobObject job);

		/* Input parameters for the "run_job" function.
			job_id job - ID of the job object (a required argument)
			string auth - the authentication token of the KBase account changing workspace permissions; must have 'admin' privelages to workspace (an optional argument; user is "public" if auth is not provided)
			
		*/
		typedef structure {
			job_id job;
			string auth;
	    } run_job_params;
		/*
	        Runs specified job
	    */
		authentication required;

50. funcdef queue_job(queue_job_params input) returns (JobObject job);
		
		/* Input parameters for the "queue_job" function.
		
			string method;
			mapping<string,string> parameters;
					
		*/
		typedef structure {
			string method;
			mapping<string,string> parameters;
	    } queue_job_params;
		/*
	        Queues the specified command to run as a job
	    */
		authentication required;

51. funcdef set_cofactors(set_cofactors_params input) returns (object_metadata output);

		/* Input parameters for the "set_cofactors" function.
		
			list<compound_id> cofactors - list of compounds that are universal cofactors (required)
			biochemistry_id biochemistry - ID of biochemistry database (optional, default is "default") 
			workspace_id biochemistry_workspace - ID of workspace containing biochemistry database (optional, default is current workspace)
			bool reset - true to reset (turn off) compounds as universal cofactors (optional, default is false)
			bool overwrite - true to overwrite existing object (optional, default is false)
			string auth - the authentication token of the KBase account (optional, default user is "public")
		
		*/
		typedef structure {
			list<compound_id> cofactors;
			biochemistry_id biochemistry;
			workspace_id biochemistry_workspace;
			bool reset;
			bool overwrite;
			string auth;
		} set_cofactors_params;
		authentication required;	
	
52. funcdef find_reaction_synonyms(find_reaction_synonyms_params input) returns (object_metadata output);	
	
		/* Input parameters for the "find_reaction_synonyms" function.
			reaction_synonyms - ID of reaction synonyms object (required argument)
			workspace_id workspace - ID of workspace for storing objects (optional argument, default is current workspace)
			biochemistry_id biochemistry - ID of the biochemistry database (optional argument, default is default)
			workspace_id biochemistry_workspace - ID of workspace containing biochemistry database (optional argument, default is kbase)
			overwrite - True to overwrite existing object (optional argument, default is false)
			string auth - the authentication token of the KBase account (optional argument, default user is "public")
			
		 */
		typedef structure {
			reaction_synonyms_id reaction_synonyms;
			workspace_id workspace;
			biochemistry_id biochemistry;
			workspace_id biochemistry_workspace;
			bool overwrite;
			string auth;
		} find_reaction_synonyms_params;
			
53. funcdef role_to_reactions(role_to_reactions_params params) returns (list<RoleComplexReactions> output);

		/* Input parameters for the "role_to_reactions" function.
			template_id templateModel - ID of the template model to be used to determine mapping (default is '')
			string auth - the authentication token of the KBase account changing workspace permissions; must have 'admin' privelages to workspace (an optional argument; user is "public" if auth is not provided)
			
		*/
		typedef structure {
			template_id templateModel;
			workspace_id workspace;
			string auth;
		} role_to_reactions_params;
		/*
		Retrieves a list of roles mapped to reactions based on input template model
		*/
    
###Code relating to assessing model sensitivity to reaction knockouts

54. funcdef reaction_sensitivity_analysis(reaction_sensitivity_analysis_params input) returns (object_metadata output);

		/* Input parameters for the "reaction_sensitivity_analysis" function.
			fbamodel_id model - ID of model to be analyzed (a required argument)
			workspace_id model_ws - ID of workspace with model to be analyzed (an optional argument - default is value of workspace argument)
			string rxnsens_uid - Name of RxnSensitivity object in workspace (an optional argument - default is KBase ID)
			workspace_id workspace - ID of workspace where output and default inputs will be selected from (a required argument)
			list<reaction_id> reactions_to_delete - list of reactions to delete in sensitiviity analysis; note, order of the reactions matters (a required argument unless gapfill solution ID is provided)		
			gapfillsolution_id gapfill_solution_id - A Gapfill solution ID. If provided, all reactions in the provided solution will be tested for deletion.
			bool delete_noncontributing_reactions - a boolean indicating if unuseful reactions should be deleted when running the analysis (an optional argument - default is "0")
			rxnprob_id rxnprobs_id - ID for a RxnProbs object in a workspace. If provided less likely reactions will be tested for deletion first in the sensitivity analysis (optional).
			workspace_id rxnprobs_ws - Workspace in which the RxnProbs object is located (optional - default is the value of the workspace argument).
			string type - type of Reaction sensitivity analysis (an optional argument - default is "unknown")
			string auth  - the authentication token of the KBase account changing workspace permissions; must have 'admin' privelages to workspace (an optional argument)
		*/
	    typedef structure {
			fbamodel_id model;
			workspace_id model_ws;
			string rxnsens_uid;
			workspace_id workspace;
			list<reaction_id> reactions_to_delete;
			gapfillsolution_id gapfill_solution_id;
			bool delete_noncontributing_reactions;
			rxnprob_id rxnprobs_id;
			workspace_id rxnprobs_ws;
			string type;
			string auth;
	    } reaction_sensitivity_analysis_params;
	    /*
	        Queues a sensitivity analysis on the knockout of model reactions
	    */

55. funcdef filter_iterative_solutions(filter_iterative_solutions_params input) returns (object_metadata output);

	        /* Input parameters for the "filter_iterative_solutions" function.
		        fbamodel_id model - Model ID for which to filter iterative gapfill solutions (a required argument)
			fbamodel_id outmodel - ModelID to which to save the filtered results (by default the filtered model is given the same ID as the input model)
			float cutoff - Cutoff for cost per reaction above which to remove iterative gapfill solution reactions (a required argument)
			gapfillsolution_id gapfillsln - Gapfill_solution ID (UUID.solution.#) containing the iterative gapfill solutions to filter (a required argument)
	                string auth - The authorization token of the KBase account with workspace permissions.
	                workspace_id workspace - ID of workspace where output and default inputs will be selected from (a required argument)
			workspace_id input_model_ws - ID of workspace containing the input model 
			*/
	    typedef structure {
		fbamodel_id model;
		fbamodel_id outmodel;
		float cutoff;
		gapfillsolution_id gapfillsln;
		workspace_id workspace;
		workspace_id input_model_ws;
		string auth;
	    } filter_iterative_solutions_params;
	
	    /* 
	        Apply a cutoff to remove high-cost iterations from an iterative gapfill run.
		*/
		authentication required;

56. funcdef delete_noncontributing_reactions(delete_noncontributing_reactions_params input) returns (object_metadata output);
		
		/* Input parameters for the "delete_noncontributing_reactions" function.
		      workspace_id workspae - Workspace for outputs and default inputs (a required argument)
		      workspace_id rxn_sensitivity_ws - Workspace for reaction sensitivity object used as input
		      string rxn_sensitivity - Reaction sensitivity ID
		      fbamodel_id new_model_uid - ID for output model with noncontributing reactions deleted
		      string new_rxn_sensitivity_uid - ID for rxnsensitivity object with bits set to indicate reactions were deleted
		      string auth - Authorization token for user (must have appropriate permissions to read and write objects)
		*/
	    typedef structure {
			workspace_id rxn_sensitivity_ws;
			string rxn_sensitivity;
			workspace_id workspace;
			fbamodel_id new_model_uid;
			string new_rxn_sensitivity_uid;
			string auth;
	    } delete_noncontributing_reactions_params;
	    /*
	        Deleted flagged reactions from a RxnSensitivity object
	    */

    

###Code relating to workspace versions of genome analysis algorithms

57. funcdef annotate_workspace_Genome(annotate_workspace_Genome_params params) returns (object_metadata output);

		/* AnnotationParameters: parameters for all annotation functions
		
			bool call_selenoproteins - identify all selenoproteins
			bool call_pyrrolysoproteins - identify all pyrrolysoproteins
			bool call_RNAs - identify all RNAs
			bool call_CDSs - identify all CDSs
			bool find_close_neighbors - identify nearby genomes in CDM
			bool gene_calling - call genes based on DNA sequences in transcripts or contigs
			string gene_calling_algorithm - algorithm to use for gene calling
			mapping<string,string> gene_calling_params - parameters for gene calling algorithm
			bool assign_functions_to_CDSs - assign functions to proteins
			string assign_functions_to_CDS_algorithm - algorithm to use for functional annotation
			mapping<string,string> assign_functions_to_CDS_params - parameters to use for functional annotation
			
		*/
		typedef structure {
			bool call_genes;
			bool annotate_genes;
	    } AnnotationParameters;
		
		/* Input parameters for the "annotate_workspace_Genome" function.
			
			string Genome_uid - user ID to be assigned to the Genome (required argument)
			string Genome_ws - workspace with genome for annotation (optional; workspace argument will be used if no genome workspace is provided)
			string new_uid - new ID to assign to annotated genome (optional; original genome will be overwritten if no new uid is provided)
			workspace_id workspace - ID of workspace with Genome (required argument)
			AnnotationParameters parameters - parameters for running annotation job
			string auth - the authentication token of the KBase account changing workspace permissions
			
		*/
		typedef structure {
			string Genome_uid;
			string Genome_ws;
			string new_uid;
			workspace_id workspace;
			AnnotationParameters annotation_parameters;
			string auth;
	    } annotate_workspace_Genome_params;
	    /*
			Create a job that runs the genome annotation pipeline on a genome object in a workspace
	    */

###Code relating to import and analysis of ProteinSets

58. funcdef gtf_to_genome(gtf_to_genome_params params) returns (object_metadata output);

		/* Input parameters for the "gtf_to_genome" function.
			string contigset;
			workspace_id contigset_ws;
			workspace_id workspace;	
			string genome_uid;
			string source_id - source ID of the genome (optional)
			string source - source of the genome(optional)
			string scientific_name;
			string domain;
			int genetic_code;
			string taxonomy;
			string gtf_file;
		*/
		typedef structure {
			string contigset;
			workspace_id contigset_ws;
			workspace_id workspace;	
			string genome_uid;
			string source_id;
			string source;
			string scientific_name;
			string domain;
			int genetic_code;
			string taxonomy;
			string gtf_file;
	    } gtf_to_genome_params;
	    /*
			Loads a gtf file to a genome typed object in the workspace      
	    */
    
59. funcdef fasta_to_ProteinSet(fasta_to_ProteinSet_params params) returns (object_metadata output);
	
		/* Input parameters for the "fasta_to_ProteinSet" function.
			string uid - user assigned ID for the protein set (optional)
			string fasta - string with sequence data from fasta file (required argument)
			workspace_id workspace - ID of workspace for storing objects (required argument)
			string auth - the authentication token of the KBase account changing workspace permissions; must have 'admin' privelages to workspace (an optional argument; user is "public" if auth is not provided)
			string name - name of the protein data (optional)
			string sourceid - source ID of the protein data (optional)
			string source - source of the protein data (optional)
			string type - type of the protein set (optional)
			
		*/
		typedef structure {
			string uid;
			string fasta;
			workspace_id workspace;
			string auth;
			string name;
			string sourceid;
			string source;
			string type;
	    } fasta_to_ProteinSet_params;
	    /*
			Loads a fasta file as a ProteinSet object in the workspace       
	    */
60. funcdef ProteinSet_to_Genome(ProteinSet_to_Genome_params params) returns (object_metadata output);    
    
	    /* Input parameters for the "ProteinSet_to_Genome" function.
			string ProteinSet_uid - ID to be assigned to the ProteinSet (required argument)
			workspace_id ProteinSet_ws - ID of workspace with the ProteinSet (optional argument; default is value of workspace argument)
			string uid - user assigned ID for the Genome (optional)
			workspace_id workspace - ID of workspace for storing objects (required argument)
			string auth - the authentication token of the KBase account changing workspace permissions; must have 'admin' privelages to workspace (an optional argument; user is "public" if auth is not provided)
			string scientific_name - scientific name to assign to genome
			string domain - domain of life for genome
			int genetic_code - genetic code to assign to genome
			
		*/
		typedef structure {
			string ProteinSet_uid;
			workspace_id ProteinSet_ws;
			workspace_id workspace;
			string uid;
			string auth;
			string scientific_name;
			string domain;
			AnnotationParameters annotation_parameters;
	    } ProteinSet_to_Genome_params;
	    /*
			Creates a Genome associated with the ProteinSet object. You cannot recall genes on this genome.  
	    */
	    authentication required;
    
###Code relating to import and analysis of Contigs

61. funcdef fasta_to_ContigSet(fasta_to_ContigSet_params params) returns (object_metadata output);

		/* Input parameters for the "fasta_to_ContigSet" function.
			string uid - user assigned ID for the ContigSet (optional)
			string fasta - string with sequence data from fasta file (required argument)
			workspace_id workspace - ID of workspace for storing objects (required argument)
			string auth - the authentication token of the KBase account changing workspace permissions; must have 'admin' privelages to workspace (an optional argument; user is "public" if auth is not provided)
			string name - name of the ContigSet data (optional)
			string sourceid - source ID of the ContigSet data (optional)
			string source - source of the ContigSet data (optional)
			string type - type of the ContigSet (optional)
			
		*/
		typedef structure {
			string uid;
			string fasta;
			workspace_id workspace;
			string auth;
			string name;
			string sourceid;
			string source;
			string type;
	    } fasta_to_ContigSet_params;
	    /*
			Loads a fasta file as a ContigSet object in the workspace       
	    */
	    authentication required;
    
62. funcdef ContigSet_to_Genome(ContigSet_to_Genome_params params) returns (object_metadata output);   

		/* Input parameters for the "ContigSet_to_Genome" function.
			string ContigSet_uid - ID to be assigned to the ContigSet (required argument)
			workspace_id ContigSet_ws - ID of workspace with the ContigSet (optional argument; default is value of workspace argument)
			string uid - user assigned ID for the Genome (optional)
			workspace_id workspace - ID of workspace for storing objects (required argument)
			string auth - the authentication token of the KBase account changing workspace permissions; must have 'admin' privelages to workspace (an optional argument; user is "public" if auth is not provided)
			string scientific_name - scientific name to assign to genome
			string domain - domain of life for genome
			int genetic_code - genetic code to assign to genome
			AnnotationParameters annotation_parameters - parameters for annotation of the genome
			
		*/
		typedef structure {
			string ContigSet_uid;
			workspace_id ContigSet_ws;
			workspace_id workspace;
			string uid;
			string auth;
			string scientific_name;
			string domain;
			int genetic_code;
			AnnotationParameters annotation_parameters;
	    } ContigSet_to_Genome_params;
	    /*
			Creates a genome associated with the ContigSet object   
	    */
	    authentication required;
    
    

###Code relating to analysis of probabilistic annotations

63. funcdef probanno_to_genome(probanno_to_genome_params params) returns (object_metadata output);
	
		/* Input parameters for the "probanno_to_genome" function.
			probanno_id pa_id - ID of the probanno object (required)
			workspace_id pa_ws - ID of workspace with probanno object (optional argument, default is value of workspace argument)
			genome_id g_id - ID to use for genome object (required argument)
			workspace_id workspace - ID of workspace for storing output objects (optional argument, default is current workspace)
			float threshold - probability threshold for including function in genome (optional argument, default is to include all functions)
			string auth - the authentication token of the KBase account changing workspace permissions; must have 'admin' privelages to workspace (an optional argument; user is "public" if auth is not provided)
			
		*/
		typedef structure {
			probanno_id pa_id;
			workspace_id pa_ws;
			workspace_id workspace;
			genome_id g_id;
			float threshold;
			string auth;
	    } probanno_to_genome_params;
	    /*
			Converts a probabilistic annotation into a genome with the same annotations        
	    */
	    authentication required;
    
	
###Code relating to loading, retrieval, and curation of mappings

64. funcdef get_mapping(get_mapping_params params) returns (Mapping output);

		typedef structure {
			role_id id;
			string name;
			string feature;
			list<string> aliases;
			list<complex_id> complexes;
	    } FunctionalRole;
	    
	    typedef tuple<role_id id,string roleType,bool optional_role,bool triggering> ComplexRole;
	    
	    typedef structure {
			complex_id id;
			string name;
			list<string> aliases;
			list<ComplexRole> roles;
	    } Complex;
	    
	    typedef string subsystem_id;
	    typedef structure {
			subsystem_id id;
			string name;
			string phenoclass;
			string subclass;
			string type;
			list<string> aliases;
			list<role_id> roles;
	    } Subsystem;
		
		typedef structure {
			mapping_id id;
			string name;
			list<Subsystem> subsystems;
			list<FunctionalRole> roles;
			list<Complex> complexes;
	    } Mapping;
		
		typedef structure {
			mapping_id map;
			workspace_id workspace;
			string auth;
	    } get_mapping_params;
	    /*
			Annotates contigs object creating a genome object        
	    */
    authentication optional;
    
65. funcdef subsystem_of_roles(subsystem_of_roles_params params) returns (mapping<string,subsysclasses> output);
    
	    typedef tuple<string,string> subsysclass;
	    typedef mapping<string,subsysclass> subsysclasses;
	    typedef structure {
			list<string> roles;
			string map;
			string map_workspace;
	    } subsystem_of_roles_params;
	    /*
			Returns subsystems for list roles       
	    */
	    authentication optional;

66. funcdef adjust_mapping_role(adjust_mapping_role_params params) returns (FunctionalRole output);
    
		/* Input parameters for the "adjust_mapping_role" function.
			mapping_id map - ID of the mapping object to be edited
			workspace_id workspace - ID of workspace containing mapping to be edited
			string role - identifier for role to be edited
			bool new - boolean indicating that a new role is being added
			string name - new name for the role
			string feature - representative feature MD5
			list<string> aliasesToAdd - list of new aliases for the role
			list<string> aliasesToRemove - list of aliases to remove for role
			bool delete - boolean indicating that role should be deleted
			string auth - the authentication token of the KBase account changing workspace permissions; must have 'admin' privelages to workspace (an optional argument; user is "public" if auth is not provided)
			
		*/
		typedef structure {
			mapping_id map;
			workspace_id workspace;
			string role;
			bool new;
			string name;
			string feature;
			list<string> aliasesToAdd;
			list<string> aliasesToRemove;
			bool delete;
			string auth;
	    } adjust_mapping_role_params;
	    /*
	        An API function supporting the curation of functional roles in a mapping object
	    */
	    authentication required;

67. funcdef adjust_mapping_complex(adjust_mapping_complex_params params) returns (Complex output);
	
		/* Input parameters for the "adjust_mapping_complex" function.
			mapping_id map - ID of the mapping object to be edited
			workspace_id workspace - ID of workspace containing mapping to be edited
			string complex - identifier for complex to be edited
			bool new - boolean indicating that a new complex is being added
			string name - new name for the role
			string feature - representative feature MD5
			list<string> rolesToAdd - roles to add to the complex
			list<string> rolesToRemove - roles to remove from the complex
			bool delete - boolean indicating that complex should be deleted
			string auth - the authentication token of the KBase account changing workspace permissions; must have 'admin' privelages to workspace (an optional argument; user is "public" if auth is not provided)
			
		*/
		typedef structure {
			mapping_id map;
			workspace_id workspace;
			string complex;
			bool new;
			string name;
			list<string> rolesToAdd;
			list<string> rolesToRemove;
			bool delete;
			string auth;
	    }adjust_mapping_complex_params;
	    /*
	        An API function supporting the curation of complexes in a mapping object
	    */
	    authentication required;

68. funcdef adjust_mapping_subsystem(adjust_mapping_subsystem_params params) returns (Subsystem output);
	
		/* Input parameters for the "adjust_mapping_subsystem" function.
			mapping_id map - ID of the mapping object to be edited
			workspace_id workspace - ID of workspace containing mapping to be edited
			string subsystem - identifier for subsystem to be edited
			bool new - boolean indicating that a new subsystem is being added
			string name - new name for the subsystem
			string type - new type for the subsystem
			string primclass - new class for the subsystem
			string subclass - new subclass for the subsystem
			list<string> rolesToAdd - roles to add to the subsystem
			list<string> rolesToRemove - roles to remove from the subsystem
			bool delete - boolean indicating that subsystem should be deleted
			string auth - the authentication token of the KBase account changing workspace permissions; must have 'admin' privelages to workspace (an optional argument; user is "public" if auth is not provided)
			
		*/
		typedef structure {
			mapping_id map;
			workspace_id workspace;
			string subsystem;
			bool new;
			string name;
			string type;
			string primclass;
			string subclass;
			list<string> rolesToAdd;
			list<string> rolesToRemove;
			bool delete;
			string auth;
	    }adjust_mapping_subsystem_params;
	    /*
	        An API function supporting the curation of subsystems in a mapping object
	    */
	    authentication required;
    
	
###Code relating to loading, retrieval, and curation of template models

69. funcdef get_template_model(get_template_model_params params) returns (TemplateModel output);

		typedef string temprxn_id;
		typedef structure {
			temprxn_id id;
			compartment_id compartment;
			reaction_id reaction;
			list<complex_id> complexes;
			string direction;
			string type;
	    } TemplateReaction;
	    
	    typedef tuple<compound_id compound,compartment_id compartment,string cpdclass,string universal,string coefficientType,string coefficient,list<tuple<string coeffficient,compound_id compound> > linkedCompounds> TemplateBiomassCompounds;
	    
	    typedef string tempbiomass_id;
	    typedef structure {
			tempbiomass_id id;
			string name;
			string type;
			string other;
			string protein;
			string dna;
			string rna;
			string cofactor;
			string energy;
			string cellwall;
			string lipid;
			list<TemplateBiomassCompounds> compounds;
	    } TemplateBiomass;
		
		typedef structure {
			template_id id;
			string name;
			string type;
			string domain;
			mapping_id map;
			workspace_id mappingws;
			list<TemplateReaction> reactions;
			list<TemplateBiomass> biomasses;
	    } TemplateModel;
		
		typedef structure {
			template_id templateModel;
			workspace_id workspace;
			string auth;
	    } get_template_model_params;
	    /*
			Retrieves the specified template model        
	    */
	    authentication optional;
    
70. funcdef import_template_fbamodel(import_template_fbamodel_params input) returns (object_metadata modelMeta);
	
		/* Input parameters for the "import_template_fbamodel" function.
			mapping_id map - ID of the mapping to associate the template model with (an optional argument; default is 'default')
			workspace_id mapping_workspace - ID of the workspace where the associated mapping is found (an optional argument; default is 'kbase')
			list<tuple<string id,string compartment,string direction,string type,list<string complex> complexes>> templateReactions - list of reactions to include in template model
			list<tuple<string name,string type,float dna,float rna,float protein,float lipid,float cellwall,float cofactor,float energy,float other,list<tuple<string id,string compartment,string cpdclass,string coefficientType,float coefficient,string conditions>> compounds>> templateBiomass - list of template biomass reactions for template model
			string name - name for template model
			string modelType - type of model constructed by template
			string domain - domain of template model
			template_id id - ID that should be used for the newly imported template model (an optional argument; default is 'undef')
			workspace_id workspace - ID of the workspace where the newly developed template model will be stored; also the default assumed workspace for input objects (a required argument)
			bool ignore_errors - ignores missing roles or reactions and imports template model anyway
			string auth - the authentication token of the KBase account changing workspace permissions; must have 'admin' privelages to workspace (an optional argument; user is "public" if auth is not provided)
			
		*/
	    typedef structure {
			mapping_id map;
			workspace_id mapping_workspace;
			list<tuple<string id,string compartment,string direction,string type,list<string> complexes>> templateReactions;
			list<tuple<string name,string type,float dna,float rna,float protein,float lipid,float cellwall,float cofactor,float energy,float other,list<tuple<string id,string compartment,string cpdclass,string coefficientType,float coefficient,string conditions>> compounds>> templateBiomass;
			string name;
			string modelType;
			string domain;
			template_id id;
			workspace_id workspace;
			bool ignore_errors;
			string auth;
	    } import_template_fbamodel_params;
	    /*
	        Import a template model from an input table of template reactions and biomass components
	    */
	    authentication required;
    
71. funcdef adjust_template_reaction(adjust_template_reaction_params params) returns (object_metadata modelMeta);

		typedef structure {
			template_id templateModel;
			workspace_id workspace;
			string reaction;
			bool clearComplexes;
			bool new;
			bool delete;
			compartment_id compartment;
			list<complex_id> complexesToAdd;
			list<complex_id> complexesToRemove;
			string direction;
			string type;
			string auth;
		} adjust_template_reaction_params;
		/*
			Modifies a reaction of a template model       
		*/
		authentication required;

72. funcdef adjust_template_biomass(adjust_template_biomass_params params) returns (object_metadata modelMeta);
	
		typedef structure {
			template_id templateModel;
			workspace_id workspace;
			string biomass;
			bool new;
			bool delete;
			bool clearBiomassCompounds;
			string name;
			string type;
			string other;
			string protein;
			string dna;
			string rna;
			string cofactor;
			string energy;
			string cellwall;
			string lipid;
			list<tuple<compound_id compound,compartment_id compartment>> compoundsToRemove;
			list<tuple<compound_id compound,compartment_id compartment,string cpdclass,string universal,string coefficientType,string coefficient,list<tuple<string coeffficient,compound_id compound> > linkedCompounds>> compoundsToAdd;
			string auth;
	    } adjust_template_biomass_params;
	    /*
			Modifies the biomass of a template model        
	    */
	    authentication required;

	

###Code relating to reconstruction, import, and analysis of regulatory models

73. funcdef add_stimuli(add_stimuli_params params) returns (object_metadata output);

	/* Input parameters for the "add_stimuli" function.
		
			string biochemid - ID of biochemistry with stimuli (optional)
			string biochem_workspace - ID of workspace with biochemistry with stimuli (optional)
			string stimuliid - ID for the stimuli to be created (optional)
			string name - Name for the stimuli (required)
			string abbreviation - Abbreviation for the stimuli (optional)
			string type - Type of the stimuli (required)
			list<string> compounds - Compounds associated with stimuli (optional)
			string workspace - ID of workspace where all output objects will be stored (optional argument, default is current workspace)
			string auth - the authentication token of the KBase account changing workspace permissions; must have 'admin' privelages to workspace (an optional argument; user is "public" if auth is not provided)
			
		*/
		typedef structure {
			string biochemid;
			string biochem_workspace;
			string stimuliid;
			string name;
			string abbreviation;
			string type;
			string description;
			list<string> compounds;
			string workspace;
			string auth;
	    } add_stimuli_params;
	    /*
			Adds a stimuli either to the central database or as an object in a workspace        
	    */
	    authentication required;
    
74. funcdef import_regulatory_model(import_regulatory_model_params params) returns (object_metadata output);    
  
	    typedef structure {
			kbase_id kbid;
			string name;
			string abbreviation;
			string description;
			string type;
			list<kbase_id> compound_kbids;
	    } Stimuli;
	    
	    typedef structure {
			kbase_id kbid;
			kbase_id stimuli_kbid;
			bool is_inhibitor;
			float strength;
			float min_concentration;
			float max_concentration;
			list<kbase_id> regulator_kbids;	
	    } RegulatoryModelRegulonStimuli;
	    
	    typedef structure {
			kbase_id kbid;
			string name;
			list<kbase_id> feature_kbids;
			list<RegulatoryModelRegulonStimuli> stimuli;
	    } RegulatoryModelRegulon;
	    
		typedef structure {
			kbase_id kbid;
			string name;
			string type;
			ws_ref genome_wsid;
			list<RegulatoryModelRegulon> regulons;
	    } RegulatoryModel;
		
		typedef structure {
			string regmodel_uid;
			workspace_id workspace;
			string genome;
			workspace_id genome_ws;
			string name;
			string type;
			list<tuple<string name,list<string> features,list<tuple<string stimuli,bool in_inhibitor,float strength,float min_conc,float max_conc,list<kbase_id> regulators>> stimuli>> regulons;
			string auth;
	    } import_regulatory_model_params;
	    /*
			Imports a regulatory model into the KBase workspace       
	    */
	    authentication required;
    
	

###Functions relating to comparison of models

75. funcdef compare_models(compare_models_params params) returns (ModelComparisonData output);
	   	/* Input parameters for the "compare_models" function.
		
			string tag - tag of error to be retrieved
			string auth - the authentication token of the KBase account changing workspace permissions; must have 'admin' privelages to workspace (an optional argument; user is "public" if auth is not provided)
			
		*/
		typedef structure {
			list<fbamodel_id> models;
			list<workspace_id> workspaces;
			string auth;
	    } compare_models_params;
	    
	    /* Data structure to hold model comparison data
		
			fbamodel_id model - id of the fba model
			workspace_id workspace - id of workspace with model
			string model_name - name of the fba model
			genome_id genome - id of the genome for the fba model
			string genome_name - name of the genome for the fba model
			int core_reactions - number of core reactions in the fba model
			int unique_reactions - number of unique reactions in the fba model
			
		*/
	    typedef structure {
			fbamodel_id model;
			workspace_id workspace;
			string model_name;
			genome_id genome;
			string genome_name;
			int gapfilled_reactions;
			int core_reactions;
			int noncore_reactions;
	    } ModelComparisonModel;
	    
	    /* Data structure to hold model reaction comparison data
		
			reaction_id reaction - id of the reaction
			compartment_id compartment - id of the reaction compartment
			string equation - equation for the reaction
			bool core - boolean indicating if the reaction is core
			mapping<fbamodel_id,list<feature_id> > model_features - map of models and features for reaction
			string role - role associated with the reaction
			string subsytem - subsystem associated with role
			string primclass - class one of the subsystem
			string subclass - class two of the subsystem
			int number_models - number of models with reaction
			float fraction_models - fraction of models with reaction
			
		*/
	    typedef structure {
			reaction_id reaction;
			string compartment;
			string equation;
			bool core;
			mapping<fbamodel_id,list<feature_id> > model_features;
			string role;
			string subsystem;
			string primclass;
			string subclass;
			int number_models;
			float fraction_models;
	    } ModelCompareReaction;
	    
	    /* Output structure for the "compare_models" function.
		
			list<ModelComparisonModel> model_comparisons;
			list<ModelCompareReaction> reaction_comparisons;
					
		*/
	    typedef structure {
			list<ModelComparisonModel> model_comparisons;
			list<ModelCompareReaction> reaction_comparisons;
			string auth;
	    } ModelComparisonData;
	    
	    /*
			Compares the specified models and computes unique reactions and core reactions
	    */
	    authentication optional;
    
   	

###Functions relating to comparison of genomes

76. funcdef compare_genomes(compare_genomes_params params) returns (object_metadata output);

		/* Input parameters for the "compare_genomes" function.
		
		list<genome_id> genomes
		list<workspace_id> workspaces
		string auth - the authentication token of the KBase account changing workspace permissions; must have 'admin' privelages to workspace (an optional argument; user is "public" if auth is not provided)
		
		*/
		typedef structure {
		string pangenome_id;
		string pangenome_ws;
		string protcomp_id;
		string protcomp_ws;
		string output_id;
		string workspace;
		} compare_genomes_params;
		/*
		Compares the specified genomes and computes unique features and core features
		*/
		authentication optional;
    

###Functions relating to construction of community models

77. funcdef import_metagenome_annotation(import_metagenome_annotation_params params) returns (object_metadata output);

	    /* Structure for the "MetagenomeAnnotationOTUFunction" object
			
			list<string> reference_genes - list of genes associated with hit
			string functional_role - annotated function
			string kbid - kbase ID of OTU function in metagenome
			int abundance - number of hits with associated role and OTU
			float confidence - confidence of functional role hit
			string confidence_type - type of functional role hit
					
		*/
	    typedef structure {
			string kbid;
			list<string> reference_genes;
			string functional_role;
			int abundance;
			float confidence;
	    } MetagenomeAnnotationOTUFunction;
	     
	    /* Structure for the "MetagenomeAnnotationOTU" object
		
			string name - name of metagenome OTU
			string kbid - KBase ID of OTU of metagenome object
			string source_id - ID used for OTU in metagenome source
			string source - source OTU ID
			list<MetagenomeAnnotationOTUFunction> functions - list of functions in OTU
			
		*/
	    typedef structure {
	    	float ave_confidence;
			float ave_coverage;
			string kbid;
			string name;
			string source_id;
			string source;
			list<MetagenomeAnnotationOTUFunction> functions;
	    } MetagenomeAnnotationOTU;
	    
	    /* Structure for the "MetagenomeAnnotation" object
		
			string type - type of metagenome object
			string name - name of metagenome object
			string kbid - KBase ID of metagenome object
			string source_id - ID used in metagenome source
			string source - source of metagenome data
			string confidence_type - type of confidence score
			list<MetagenomeAnnotationOTU> otus - list of otus in metagenome
			
		*/
	    typedef structure {
			string type;
			string name;
			string kbid;
			string source_id;
			string source;
			string confidence_type;
			list<MetagenomeAnnotationOTU> otus;
	    } MetagenomeAnnotation;
	    
	    /* Input parameters for the "import_metagenome_annotation" function.
		
			string metaanno_uid - ID to save metagenome in workspace
			workspace_id workspace - ID of workspace for metagenome object
			string source_id - ID used in metagenome data source
			string source - metagenome data source
			string type - type of metagenome
			string confidence_type - type of confidence score
			string name - name of metagenome
			list<tuple<list<string> genes,string functional_role,string otu,int abundance,float confidence,string confidence_type>> annotations;
			string auth - the authentication token of the KBase account changing workspace permissions; must have 'admin' privelages to workspace (an optional argument; user is "public" if auth is not provided)
			
		*/
		typedef structure {
			string metaanno_uid;
			workspace_id workspace;
			string source_id;
			string source;
			string type;
			string confidence_type;
			string name;
			list<tuple<list<string> genes,string functional_role,string otu,int abundance,float confidence>> annotations;
			string auth;
	    } import_metagenome_annotation_params;
	    
	    /*
			Imports metagenome annotation data into a metagenome annotation object
	    */
	    authentication required;
    
78. funcdef models_to_community_model(import_metagenome_annotation_params params) returns (object_metadata output);   	

			/* Input parameters for the "models_to_community_model" function.
			
			string model_uid - ID of community model
			workspace_id workspace - workspace where community model should be saved
			string name - name of community model
			list<tuple<string model_uid,string model_ws,float abundance>> models - models to be merged into community model
			string auth - the authentication token of the KBase account changing workspace permissions; must have 'admin' privelages to workspace (an optional argument; user is "public" if auth is not provided)
			
		*/
		typedef structure {
			string model_uid;
			workspace_id workspace;
			string name;
			list<tuple<string model_uid,string model_ws,float abundance>> models;
			string auth;
	    } models_to_community_model_params;
	    
	    /*
			Combines multiple single genome models into a single community model
	    */
	    authentication required;
   
79. funcdef metagenome_to_fbamodels(metagenome_to_fbamodels_params params) returns (list<object_metadata> outputs);

	   	/* Input parameters for the "metagenome_to_fbamodel" function.
		
			string model_uid - ID of community model
			workspace_id workspace - workspace where community model should be saved
			string name - name of community model
			list<tuple<string model_uid,workspace_id model_ws,float abundance>> models - models to be merged into community model
			string auth - the authentication token of the KBase account changing workspace permissions; must have 'admin' privelages to workspace (an optional argument; user is "public" if auth is not provided)
			
		*/
		typedef structure {
			mapping<string,string> model_uids;
			workspace_id workspace;
			string metaanno_uid;
			workspace_id metaanno_ws;
			float min_abundance;
			float confidence_threshold;
			int max_otu_models;
			int min_reactions;
			mapping<string,tuple<workspace_id template_ws,template_id template_uid>> templates;
			string auth;
	    } metagenome_to_fbamodels_params;
	    
	    /*
			Constructs models from metagenome annotation OTUs
	    */
	    authentication required;

80. funcdef import_expression(import_expression_params input) returns (object_metadata expression_meta); 
    
		    /*
		      ID of gene expression sample
		     */
		    typedef string sample_id;
		    /*
		      ID of gene expression sample series 
		     */
		    typedef string series_id;
		
		    /*
		      Normilized gene expression value
		     */
		    typedef float measurement;
		
		    typedef structure {
			    string sample_id;
			    mapping<feature_id, measurement> data_expression_levels_for_sample;
		    } ExpressionDataSample;
		
		        /* Input parameters for the "simulate_expression" function.
			
		    	   	mapping<sample_id, ExpressionDataSample> expression_data_sample_series - gene expression data (a required argument)
				series_id series -  ID of series (a required argument)
				string source_id - ID of the source (an optional argument: default is '')
				string source_date - Date of the source (an optional argument: default is '')
				string processing_comments - comment (an optional argument: default is '')
				string description - description (an optional argument: default is '')
				workspace_id workspace - workspace to contain the data (an optional argument: default is value of workspace argument)		
				string numerical_interpretation - Numerical interpretation
			*/
		    typedef structure {
			    mapping<sample_id, ExpressionDataSample> expression_data_sample_series;
			    series_id series;
			    string source_id;
			    string source_date;
			    string description;
			    string processing_comments;
			    workspace_id workspace;
			    genome_id genome_id;
			    string numerical_interpretation;
		    } import_expression_params;
		
		    /*
		      Import gene expression.
		    */
		    authentication required;
   

81. funcdef import_regulome(import_regulome_params input) returns (object_metadata regulome_meta);

	    /*
	     Import RegPrecise regulome.
	    */
	
	    typedef structure {
		    string name;
		    string class;
	    } effector;
	
	    typedef structure {
		string name;
		string locus;
	    } locus;
	
	    typedef list<locus> operon;
	
	    typedef structure {
		list<operon> operons;
		locus transcription_factor;
		list<effector> effectors;	
		string sign;
	    } regulon;
	
	    typedef structure {
		list<regulon> regulons;
		workspace_id workspace;
		workspace_id genome_workspace;
		genome_id genome_id;
	    } import_regulome_params;
	
	    authentication required;


    
82. funcdef create_promconstraint(CreatePromConstraintParameters params) returns (object_metadata promconstraint_meta);
		
		/*
		Named parameters for 'create_promconstraint' method.  Currently all options are required.
		
		genome_id genome_id             - the workspace ID of the genome to link to the prom object
		series_id series_id     - the workspace ID of the expression data collection needed to
		                                               build the PROM constraints.
		regulome_id  regulome_id        - the workspace ID of the regulatory network data to use
		promconstraint_id promconstraint_id - the the workspace ID for the new PROM constraint
		*/
		typedef structure {
		genome_id genome_id;
		series_id series_id;
		regulome_id regulome_id;
		promconstraint_id promconstraint_id;
		} CreatePromConstraintParameters;
		
		/*
		This method creates a set of Prom constraints for a given genome annotation based on a regulatory network
		and a collection of gene expression data stored on a workspace.  Parameters are specified in the
		CreatePromconstraintParameters object.  
		The ID of the new Prom constraints object is returned. The Prom constraints can then be used in conjunction
		with an FBA model using FBA Model Services.
		*/
		authentication required;


83. funcdef add_biochemistry_compounds(add_biochemistry_compounds_params params) returns (object_metadata output); 

			/*
			    Add specified compounds to specified biochemistry
			*/
			typedef structure {
			list<tuple<string abbreviation,string name,list<string> aliases,string formula,float charge,bool isCofactor,string structureString,string structureType,string id>> compounds;
			    string workspace;
			    string biochemistry;
			    string biochemistry_ws;
			    string output_id;
			} add_biochemistry_compounds_params;
			authentication required;

84. funcdef update_object_references(update_object_references_params params) returns (object_metadata output);
    
	    /*
	    	Update object references
	    */
	    typedef structure {
	    	string object;
	    	string object_workspace;
	    	
	    	string original_object;
	    	string original_workspace;
	    	string original_instance;
	    	
	    	string reference_field;
	    	
	    	string newobject;
	    	string newobject_workspace;
	    	string newobject_instance;
	    	
	    	bool create_newobject;
	    	bool update_subrefs;
	    	string output_id;
	    	string workspace;
	    } update_object_references_params;
	    authentication required;
    

###Functions relating to editing of genomes and models

85. funcdef add_reactions(add_reactions_params params) returns (object_metadata output);

	   	/* Input parameters for the "add_reactions" function.
		*/
		typedef structure {
			string model;
			string model_workspace;
			string output_id;
			string workspace;
			list<tuple<string reaction_id,string compartment,string direction,string gpr,string pathway,string name,string reference,string enzyme,string equation>> reactions;
	    } add_reactions_params;
	    /*
			Add new reactions to the model from the biochemistry or custom reactions
	    */
	    authentication required;
    
86. funcdef remove_reactions(remove_reactions_params params) returns (object_metadata output);

		/* Input parameters for the "remove_reactions" function.
		*/
		typedef structure {
			string model;
			string model_workspace;
			string output_id;
			string workspace;
			list<string> reactions;
	    } remove_reactions_params;
	    /*
			Remove reactions from the model
	    */
	    authentication required;
	    
87. funcdef modify_reactions(modify_reactions_params params) returns (object_metadata output);
	
		/* Input parameters for the "modify_reactions" function.
		*/
		typedef structure {
			string model;
			string model_workspace;
			string output_id;
			string workspace;
			list<tuple<string reaction_id,string direction,string gpr,string pathway,string name,string reference,string enzyme>> reactions;
	    } modify_reactions_params;
	    /*
			Modify reactions in the model
	    */
	    authentication required;
    
88. funcdef add_features(add_features_params params) returns (object_metadata output);
	
		/* Input parameters for the "add_features" function.
		*/
		typedef structure {
			string genome;
			string genome_workspace;
			string output_id;
			string workspace;
			list<tuple<feature_id feature,string function,string type,list<string> aliases,list<string> publications,list<string> annotations,string protein_translation,string dna_sequence,list<tuple<string,int,string,int>> locations>> genes;
	    } add_features_params;
	    /*
			Add new features to the genome
	    */
	    authentication required;

89. funcdef remove_features(remove_features_params params) returns (object_metadata output);
   	
		/* Input parameters for the "remove_features" function.
		*/
		typedef structure {
			string genome;
			string genome_workspace;
			string output_id;
			string workspace;
			list<string> features;
	    } remove_features_params;
	    /*
			Remove features from the genome
	    */
	    authentication required;
    
90. funcdef modify_features(modify_features_params params) returns (object_metadata output);
	
		/* Input parameters for the "modify_genes" function.
		*/
		typedef structure {
			string genome;
			string genome_workspace;
			string output_id;
			string workspace;
			list<tuple<feature_id feature,string function,string type,list<string> aliases,list<string> publications,list<string> annotations,string protein_translation,string dna_sequence,list<tuple<string,int,string,int>> locations>> genes;
	    } modify_features_params;
	    /*
			Modify features in the genome
	    */
	    authentication required;
    
    
###Functions relating to classification of genomes

91. funcdef import_trainingset(import_trainingset_params params) returns (object_metadata output);

	   	/* Input parameters for the "import_trainingset" function.
		*/
		typedef structure {
			list<tuple<string workspace_id,string genome_id,string class>> workspace_training_set;
			list<tuple<string database,string genome_id,string class,list<string> attributes>> external_training_set;
			string description;
			list<tuple<string class,string description>> class_data;
			string attribute_type;
			bool preload_attributes;
			string workspace;
			string output_id;
	    } import_trainingset_params;
	    /*
			Import a training set of genomes and classifications
	    */
	    authentication required;
    
92. funcdef preload_trainingset(preload_trainingset_params params) returns (object_metadata output);

		/* Input parameters for the "preload_trainingset" function.
		*/
		typedef structure {
			string trainingset;
			string trainingset_ws;
			string attribute_type;
			string workspace;
			string output_id;
	    } preload_trainingset_params;
	    /*
			Preloads a training set with attributes, cutting time to produce distinct classifiers
	    */
	    authentication required;
    
93. funcdef build_classifier(build_classifier_params params) returns (object_metadata output);	
   	
	   	/* Input parameters for the "build_classifier" function.
		*/
		typedef structure {
			string trainingset;
			string trainingset_ws;
			string attribute_type;
			string classifier_type;
			string workspace;
			string output_id;
	    } build_classifier_params;
	    /*
			Build a classifier for the input set of genomes
	    */
	    authentication required;
    
94. funcdef classify_genomes(classify_genomes_params params) returns (object_metadata output); 
   
	    /* Input parameters for the "classify_genomes" function.
		*/
		typedef structure {
			list<tuple<string workspace_id,string genome_id>> workspace_genomes; 
			list<tuple<string database,string genome_id>> external_genomes;
			string workspace;
			string output_id;
			string classifier_ws;
			string classifier;
	    } classify_genomes_params;
	    /*
			Build a classifier for the input set of genomes
	    */
	    authentication required;
    
    

###Functions relating to modeling of expression data

95. funcdef build_tissue_model(build_tissue_model_params params) returns (object_metadata output);

	   	/* Input parameters for the "build_tissue_model" function.
		*/
		typedef structure {
			string expsample_ws;
			string expsample;
			string model_ws;
			string model;
			string workspace;
			string output_id;
	    } build_tissue_model_params;
	    /*
			Build a tissue model based on the input expression data
	    */
	    authentication required;
 





#Types for FBAModel.spec

##Workspace Module
KBaseFBA

##Workspace with Data
?

###FBA
####Description 
FBA object holds the formulation and results of a flux balance analysis study

####Relationships
	Reference to regulome
	@id ws KBaseRegulation.Regulome
	*/
	typedef string regulome_ref;
	
	
	/*
	Reference to metabolic model
	@id ws KBaseFBA.FBAModel
	*/
	typedef string fbamodel_ref;
	
	/*
	Reference to PROM constraints
	@id ws KBaseFBA.PromConstraint
	*/
	typedef string promconstraint_ref;
	
	/*
	Reference to expression data
	@id ws KBaseExpression.ExpressionSample
	*/
	typedef string expression_sample_ref;
	
	/*
	Reference to a model template
	@id ws KBaseBiochem.Media
	*/
	typedef string media_ref;
	
	/*
	Reference to a phenotype set object
	@id ws KBasePhenotypes.PhenotypeSet
	*/
	typedef string phenotypeset_ref;
	
	/*
	Reference to a feature of a genome object
	@id subws KBaseGenomes.Genome.features.[*].id
	*/
	typedef string feature_ref;
	
	/*
	Reference to a reaction object in a model
	@id subws KBaseFBA.FBAModel.modelreactions.[*].id
	*/
	typedef string modelreaction_ref;
	
	/*
	Reference to a compound object in a model
	@id subws KBaseFBA.FBAModel.modelcompounds.[*].id
	*/
	typedef string modelcompound_ref;
	
	/*
	Reference to a phenotype simulation set object
	@id ws KBasePhenotypes.PhenotypeSimulationSet
	*/
	typedef string phenotypesimulationset_ref;
	
	/*
	Reference to a compound object
	@id subws KBaseBiochem.Biochemistry.compounds.[*].id
	*/
	typedef string compound_ref;
	
	/*
	Reference to a reaction object in a biochemistry
	@id subws KBaseBiochem.Biochemistry.reactions.[*].id
	*/
	typedef string reaction_ref;
	
	/*
	Reference to a compartment object
	@id subws KBaseBiochem.Biochemistry.compartments.[*].id
	*/
	typedef string compartment_ref;
	
	/*
	Reference to a biomass object in a model
	@id subws KBaseFBA.FBAModel.biomasses.[*].id
	*/
	typedef string biomass_ref;


####Fields
		fba_id id; (string)
		bool fva; (int)
		bool fluxMinimization; (int)
		bool findMinimalMedia; (int)
		bool allReversible; (int)
		bool simpleThermoConstraints; (int)
		bool thermodynamicConstraints; (int)
		bool noErrorThermodynamicConstraints; (int)
		bool minimizeErrorThermodynamicConstraints; (int)
		bool quantitativeOptimization; (int)
		bool maximizeObjective; (int)
		mapping<modelcompound_id, float> compoundflux_objterms;
		mapping<modelreaction_id, float> reactionflux_objterms;
		mapping<biomass_id, float> biomassflux_objterms;
		int comboDeletions;
		int numberOfSolutions;
		float objectiveConstraintFraction;
		float defaultMaxFlux;
		float defaultMaxDrainFlux;
		float defaultMinDrainFlux;
		float PROMKappa;
		float tintleW;
		float tintleKappa;
		bool decomposeReversibleFlux; (int)
		bool decomposeReversibleDrainFlux; (int)
		bool fluxUseVariables; (int)
		bool drainfluxUseVariables; (int)
		bool minimize_reactions; (int)
		regulome_ref regulome_ref; (string ws_ref)
		fbamodel_ref fbamodel_ref; (string ws_ref)
		promconstraint_ref promconstraint_ref; (string ws_ref)
		expression_sample_ref tintlesample_ref; (string ws_ref)
		media_ref media_ref; (string ws_ref)
		phenotypeset_ref phenotypeset_ref; (string ws_ref)
		list<feature_ref> geneKO_refs; (strings ws_refs)
		list<modelreaction_ref> reactionKO_refs; (strings ws_refs)
		list<modelcompound_ref> additionalCpd_refs; (strings ws_refs)
		mapping<string, float> uptakeLimits;
		mapping<modelreaction_id, float> minimize_reaction_costs;
		mapping<string, string> parameters;
		mapping<string, list<string>> inputfiles;
		list<FBAConstraint> FBAConstraints; (see below)
		list<FBAReactionBound> FBAReactionBounds; (see below)
		list<FBACompoundBound> FBACompoundBounds; (see below)
		float objectiveValue;
		mapping<string, list<string>> outputfiles;
		phenotypesimulationset_ref phenotypesimulationset_ref;
		list<FBACompoundVariable> FBACompoundVariables; (see below)
		list<FBAReactionVariable> FBAReactionVariables; (see below)
		list<FBABiomassVariable> FBABiomassVariables; (see below)
		list<FBAPromResult> FBAPromResults; (see below)
		list<FBATintleResult> FBATintleResults; (see below)
		list<FBADeletionResult> FBADeletionResults; (see below)
		list<FBAMinimalMediaResult> FBAMinimalMediaResults; (see below)
		list<FBAMetaboliteProductionResult> FBAMetaboliteProductionResults; (see below)
		list<FBAMinimalReactionsResult> FBAMinimalReactionsResults; (see below)
		list<QuantitativeOptimizationSolution> QuantitativeOptimizationSolutions; (see below)
		list<GapfillingSolution> gapfillingSolutions; (see below)
		
	Subobjects:	
		typedef structure {
		  string name;
		  float rhs;
		  string sign;
		  mapping<modelcompound_id, float> compound_terms;
		  mapping<modelreaction_id, float> reaction_terms;
		  mapping<biomass_id, float> biomass_terms;
		} FBAConstraint;
		
		typedef structure {
		  modelreaction_ref modelreaction_ref;
		  string variableType;
		  float upperBound;
		  float lowerBound;
		} FBAReactionBound;
		
		typedef structure {
		  modelcompound_ref modelcompound_ref;
		  string variableType;
		  float upperBound;
		  float lowerBound;
		} FBACompoundBound;

		typedef structure {
		  modelcompound_ref modelcompound_ref;
		  string variableType;
		  float upperBound;
		  float lowerBound;
		  string class;
		  float min;
		  float max;
		  float value;
		} FBACompoundVariable;
		
		typedef structure {
		  modelreaction_ref modelreaction_ref;
		  string variableType;
		  float upperBound;
		  float lowerBound;
		  string class;
		  float min;
		  float max;
		  float value;
		} FBAReactionVariable;
		
		typedef structure {
		  biomass_ref biomass_ref;
		  string variableType;
		  float upperBound;
		  float lowerBound;
		  string class;
		  float min;
		  float max;
		  float value;
		} FBABiomassVariable;
		
		typedef structure {
		  float objectFraction;
		  float alpha;
		  float beta;
		} FBAPromResult;
		
		typedef structure {
		  float originalGrowth;
		  float growth;
		  float originalObjective;
		  float objective;
		  mapping<conflict_state, feature_id> conflicts;
		} FBATintleResult;
		
		typedef structure {
		  list<feature_ref> feature_refs;
		  float growthFraction;
		} FBADeletionResult;
		
		typedef structure {
		  list<compound_ref> essentialNutrient_refs;
		  list<compound_ref> optionalNutrient_refs;
		} FBAMinimalMediaResult;
		
		typedef structure {
		  modelcompound_ref modelcompound_ref;
		  float maximumProduction;
		} FBAMetaboliteProductionResult;
		
		typedef structure {
		  string id;
		  bool suboptimal;
		  float totalcost;
		  list<modelreaction_ref> reaction_refs;
		  list<string> reaction_directions;
		} FBAMinimalReactionsResult;
		
		typedef structure {
		  string biomass_component;
		  float mod_coefficient;
		} QuantOptBiomassMod;
		
		typedef structure {
		  modelreaction_ref modelreaction_ref;
		  modelcompound_ref modelcompound_ref;
		  bool reaction;
		  float mod_upperbound;
		} QuantOptBoundMod;
		
		typedef structure {
		  float atp_synthase;
		  float atp_maintenance;
		  list<QuantOptBiomassMod> QuantOptBiomassMods;
		  list<QuantOptBoundMod> QuantOptBoundMods;
		} QuantitativeOptimizationSolution;
		
		typedef structure {
		  int round;
		  reaction_ref reaction_ref;
		  compartment_ref compartment_ref;
		  string direction;
		  int compartmentIndex;
		  list<feature_ref> candidateFeature_refs;
		} GapfillingReaction;
		
		typedef structure {
		  int round;
		  modelreaction_ref modelreaction_ref;
		} ActivatedReaction;
		
		typedef structure {
		  gapfillsol_id id;
		  float solutionCost;
		  list<modelcompound_ref> biomassRemoval_refs;
		  list<modelcompound_ref> mediaSupplement_refs;
		  list<modelreaction_ref> koRestore_refs;
		  bool integrated;
		  bool suboptimal;
		  float objective;
		  float gfscore;
		  float actscore;
		  float rejscore;
		  float candscore;
		  list<GapfillingReaction> rejectedCandidates;
		  list<modelreaction_ref> failedReaction_refs;
		  list<ActivatedReaction> activatedReactions;
		  list<GapfillingReaction> gapfillingSolutionReactions;
		} GapfillingSolution;

###FBAModel
####Description 
FBAModel object

####Relationships

		/*
		Reference to a model template
		@id ws KBaseGenomes.Genome
		*/
		typedef string genome_ref;
		
		/*
		Reference to a metagenome object
		@id ws KBaseGenomes.MetagenomeAnnotation
		*/
		typedef string metagenome_ref;
		
		/*
		Reference to an OTU in a metagenome
		@id subws KBaseGenomes.MetagenomeAnnotation.otus.[*].id
		*/
		typedef string metagenome_otu_ref;
		
		/*
		Reference to a model template
		@id ws KBaseFBA.ModelTemplate
		*/
		typedef string template_ref;
		
		/*
		Reference to a gapfilling object
		@id ws KBaseFBA.Gapfilling
		*/
		typedef string gapfill_ref;
		
		/*
		Reference to a FBA object
		@id ws KBaseFBA.FBA
		*/
		typedef string fba_ref;
		
		/*
		Reference to a model template
		@id ws KBaseBiochem.Media
		*/
		typedef string media_ref;
		
		/*
		Reference to a gapgen object
		@id ws KBaseFBA.Gapgeneration
		*/
		typedef string gapgen_ref;
		
		/*
		Reference to a compound object in a model
		@id subws KBaseFBA.FBAModel.modelcompounds.[*].id
		*/
		typedef string modelcompound_ref;
		
		/*
		Reference to a compartment object
		@id subws KBaseBiochem.Biochemistry.compartments.[*].id
		*/
		typedef string compartment_ref;
		
		/*
		Reference to a compound object
		@id subws KBaseBiochem.Biochemistry.compounds.[*].id
		*/
		typedef string compound_ref;
		
		/*
		Reference to a compartment object in a model
		@id subws KBaseFBA.FBAModel.modelcompartments.[*].id
		*/
		typedef string modelcompartment_ref;
		
		/*
		Reference to a reaction object in a biochemistry
		@id subws KBaseBiochem.Biochemistry.reactions.[*].id
		*/
		typedef string reaction_ref;
		
		/*
		Reference to a complex object
		@id subws KBaseOntology.Mapping.complexes.[*].id
		*/
		typedef string complex_ref;
		
		/*
		Reference to a feature of a genome object
		@id subws KBaseGenomes.Genome.features.[*].id
		*/
		typedef string feature_ref;


####Fields
		
		  fbamodel_id id; (string)
		  string source; 
		  source_id source_id; (string)
		  string name;
		  string type;
		  genome_ref genome_ref; (string)
		  metagenome_ref metagenome_ref; (string)
		  metagenome_otu_ref metagenome_otu_ref; (string)
		  template_ref template_ref; (string)
		  float ATPSynthaseStoichiometry;
		  float ATPMaintenance;
		  list<template_ref> template_refs; (strings)
		  list<ModelGapfill> gapfillings; (see below)
		  list<ModelGapgen> gapgens; (see below)
		  list<ModelQuantOpt> quantopts; (see below)
		  list<Biomass> biomasses; (see below)
		  list<ModelCompartment> modelcompartments; (see below)
		  list<ModelCompound> modelcompounds; (see below)
		  list<ModelReaction> modelreactions; (see below)
	
	Subtypes:	  
		  typedef structure {
		  gapfill_id id;
		  gapfill_id gapfill_id;
		  gapfill_ref gapfill_ref;
		  fba_ref fba_ref;
		  bool integrated;
		  string integrated_solution;
		  media_ref media_ref;
		} ModelGapfill;
		
		typedef structure {
		  gapgen_id id;
		  gapgen_id gapgen_id;
		  gapgen_ref gapgen_ref;
		  fba_ref fba_ref;
		  bool integrated;
		  string integrated_solution;
		  media_ref media_ref;
		} ModelGapgen;
		
		typedef structure {
		  bool integrated;
		  list<tuple<string, float, bool>> ReactionMaxBounds;
		  list<tuple<string, float>> UptakeMaxBounds;
		  list<tuple<string, string, float>> BiomassChanges;
		  float ATPSynthase;
		  float ATPMaintenance;
		} QuantOptSolution;
		
		typedef structure {
		  string id;
		  fba_ref fba_ref;
		  media_ref media_ref;
		  bool integrated;
		  int integrated_solution;
		  list<QuantOptSolution> solutions;
		} ModelQuantOpt;
		
		typedef structure {
		  modelcompound_ref modelcompound_ref;
		  float coefficient;
		} BiomassCompound;
		
		typedef structure {
		  biomass_id id;
		  string name;
		  float other;
		  float dna;
		  float rna;
		  float protein;
		  float cellwall;
		  float lipid;
		  float cofactor;
		  float energy;
		  list<BiomassCompound> biomasscompounds;
		} Biomass;
		
		typedef structure {
		  modelcompartment_id id;
		  compartment_ref compartment_ref;
		  int compartmentIndex;
		  string label;
		  float pH;
		  float potential;
		} ModelCompartment;
		
		typedef structure {
		  modelcompound_id id;
		  compound_ref compound_ref;
		  list<string> aliases;
		  string name;
		  float charge;
		  float maxuptake;
		  string formula;
		  modelcompartment_ref modelcompartment_ref;
		} ModelCompound;
		
		typedef structure {
		  modelcompound_ref modelcompound_ref;
		  float coefficient;
		} ModelReactionReagent
		
		typedef structure {
		  string role;
		  bool triggering;
		  bool optionalSubunit;
		  string note;
		  list<feature_ref> feature_refs;
		} ModelReactionProteinSubunit;
		
		typedef structure {
		  complex_ref complex_ref;
		  string note;
		  list<ModelReactionProteinSubunit> modelReactionProteinSubunits;
		} ModelReactionProtein;
		
		typedef structure {
		  modelreaction_id id;
		  reaction_ref reaction_ref;
		  string name;
		  list<string> aliases;
		  string pathway;
		  string reference;
		  string direction;
		  float protons;
		  float maxforflux;
		  float maxrevflux;
		  modelcompartment_ref modelcompartment_ref;
		  float probability;
		  list<ModelReactionReagent> modelReactionReagents;
		  list<ModelReactionProtein> modelReactionProteins;
		} ModelReaction;


###FBAModelSet
####Description 
A type describing a set of FBAModels, where each element of the set 
is an FBAModel object reference.

####Relationships

	/*
	Reference to metabolic model
	@id ws KBaseFBA.FBAModel
	*/
	typedef string fbamodel_ref;

####Fields
	
	string description;
	mapping<string, FBAModelSetElement> elements; (see below)
	
	typedef structure {
	  mapping<string, string> metadata;
	  fbamodel_ref ref;
	} FBAModelSetElement;

###Classifier
####Description 
Unknown

####Relationships

	/*
	Reference to a training set object
	@id ws KBaseFBA.ClassifierTrainingSet
	*/
	typedef string Trainingset_ref;

####Fields

	  string id;
	  string attribute_type;
	  string classifier_type;
	  Trainingset_ref trainingset_ref;
	  string data;
	  string readable;
	  int correctly_classified_instances;
	  int incorrectly_classified_instances;
	  int total_instances;
	  float kappa;
	  float mean_absolute_error;
	  float root_mean_squared_error;
	  float relative_absolute_error;
	  float relative_squared_error;
	  list<ClassifierClasses> classes;(see below)
	
	typedef structure {
	  string id;
	  string description;
	  float tp_rate;
	  float fb_rate;
	  float precision;
	  float recall;
	  float f_measure;
	  float ROC_area;
	  mapping<string, int> missclassifications;
	} ClassifierClasses;
	
	
###ClassifierResult
####Description 
Unknown

####Relationships

	/*
	Reference to a classifier object
	@id ws KBaseFBA.Classifier
	*/
	typedef string Classifier_ref;
	
	/*
	Reference to a model template
	@id ws KBaseGenomes.Genome
	*/
	typedef string genome_ref;

####Fields

	string id;
	Classifier_ref classifier_ref;
	list<WorkspaceGenomeClassPrediction> workspace_genomes; (see below)
	list<ExternalGenomeClassPrediction> external_genomes; (see below)
	
	typedef tuple<genome_ref, string, float> WorkspaceGenomeClassPrediction;
	
	typedef tuple<string, string, string, float> ExternalGenomeClassPrediction;

###ETC
####Description 
ElectronTransportChains (ETC) object

####Relationships
None

####Fields

	list<ETCPathwayObj> pathways; (see below)
	
	typedef structure {
	  list<string> reactions;
	} ETCStep;
	
	typedef structure {
	  string electron_acceptor;
	  list<ETCStep> steps;
	} ETCPathwayObj;
	

###Gapfilling
####Description 
GapFilling object holds data on the formulations and solutions of a gapfilling analysis

####Relationships

	/*
	Reference to a FBA object
	@id ws KBaseFBA.FBA
	*/
	typedef string fba_ref;
	
	/*
	Reference to a model template
	@id ws KBaseBiochem.Media
	*/
	typedef string media_ref;
	
	/*
	Reference to metabolic model
	@id ws KBaseFBA.FBAModel
	*/
	typedef string fbamodel_ref;
	
	/*
	Reference to probabilistic annotation
	@id ws KBaseProbabilisticAnnotation.ProbAnno
	*/
	typedef string probanno_ref;
	
	/*
	Reference to a reaction object in a biochemistry
	@id subws KBaseBiochem.Biochemistry.reactions.[*].id
	*/
	typedef string reaction_ref;
	
	/*
	Reference to a compartment object
	@id subws KBaseBiochem.Biochemistry.compartments.[*].id
	*/
	typedef string compartment_ref;
	
	/*
	Reference to a compound object in a model
	@id subws KBaseFBA.FBAModel.modelcompounds.[*].id
	*/
	typedef string modelcompound_ref;
	
	/*
	Reference to a reaction object in a model
	@id subws KBaseFBA.FBAModel.modelreactions.[*].id
	*/
	typedef string modelreaction_ref;
	
	/*
	Reference to a feature of a genome object
	@id subws KBaseGenomes.Genome.features.[*].id
	*/
	typedef string feature_ref;

####Fields

	typedef structure {
	  gapfill_id id; (string)
	  fba_ref fba_ref;
	  media_ref media_ref;
	  fbamodel_ref fbamodel_ref;
	  probanno_ref probanno_ref;
	  bool mediaHypothesis; (int)
	  bool biomassHypothesis; (int)
	  bool gprHypothesis; (int)
	  bool reactionAdditionHypothesis; (int)
	  bool balancedReactionsOnly; (int)
	  bool completeGapfill; (int)
	  bool simultaneousGapfill; (int)
	  list<reaction_ref> guaranteedReaction_refs;
	  list<reaction_ref> targetedreaction_refs;
	  list<reaction_ref> blacklistedReaction_refs;
	  list<compartment_ref> allowableCompartment_refs;
	  float reactionActivationBonus;
	  float drainFluxMultiplier;
	  float directionalityMultiplier;
	  float deltaGMultiplier;
	  float noStructureMultiplier;
	  float noDeltaGMultiplier;
	  float biomassTransporterMultiplier;
	  float singleTransporterMultiplier;
	  float transporterMultiplier;
	  int timePerSolution;
	  int totalTimeLimit;
	  mapping<reaction_ref, float> reactionMultipliers;
	  list<GapfillingSolution> gapfillingSolutions; (see below)
	} Gapfilling;
	
	typedef structure {
	  int round;
	  reaction_ref reaction_ref;
	  compartment_ref compartment_ref;
	  string direction;
	  int compartmentIndex;
	  list<feature_ref> candidateFeature_refs;
	} GapfillingReaction;
	
	typedef structure {
	  int round;
	  modelreaction_ref modelreaction_ref;
	} ActivatedReaction;
	
	typedef structure {
	  gapfillsol_id id;
	  float solutionCost;
	  list<modelcompound_ref> biomassRemoval_refs;
	  list<modelcompound_ref> mediaSupplement_refs;
	  list<modelreaction_ref> koRestore_refs;
	  bool integrated;
	  bool suboptimal;
	  float objective;
	  float gfscore;
	  float actscore;
	  float rejscore;
	  float candscore;
	  list<GapfillingReaction> rejectedCandidates;
	  list<modelreaction_ref> failedReaction_refs;
	  list<ActivatedReaction> activatedReactions;
	  list<GapfillingReaction> gapfillingSolutionReactions;
	} GapfillingSolution;

###Gapgeneration
####Description 
GapGeneration object holds data on formulation and solutions from gapgen analysis

####Relationships

	/*
	Reference to a FBA object
	@id ws KBaseFBA.FBA
	*/
	typedef string fba_ref;
	
	/*
	Reference to metabolic model
	@id ws KBaseFBA.FBAModel
	*/
	typedef string fbamodel_ref;
	
	/*
	Reference to a model template
	@id ws KBaseBiochem.Media
	*/
	typedef string media_ref;
	
	/*
	Reference to a compound object in a model
	@id subws KBaseFBA.FBAModel.modelcompounds.[*].id
	*/
	typedef string modelcompound_ref;
	
	/*
	Reference to a reaction object in a model
	@id subws KBaseFBA.FBAModel.modelreactions.[*].id
	*/
	typedef string modelreaction_ref;

####Fields

	typedef structure {
	  gapgen_id id; (string)
	  fba_ref fba_ref;
	  fbamodel_ref fbamodel_ref;
	  bool mediaHypothesis; (int)
	  bool biomassHypothesis; (int)
	  bool gprHypothesis; (int)
	  bool reactionRemovalHypothesis; (int)
	  media_ref media_ref;
	  media_ref referenceMedia_ref;
	  int timePerSolution;
	  int totalTimeLimit;
	  list<GapgenerationSolution> gapgenSolutions; (see below)
	} Gapgeneration;
	
	typedef structure {
	  modelreaction_ref modelreaction_ref;
	  string direction;
	} GapgenerationSolutionReaction;
	
	typedef structure {
	  gapgensol_id id;
	  float solutionCost;
	  list<modelcompound_ref> biomassSuppplement_refs;
	  list<modelcompound_ref> mediaRemoval_refs;
	  list<modelreaction_ref> additionalKO_refs;
	  bool integrated;
	  bool suboptimal;
	  list<GapgenerationSolutionReaction> gapgenSolutionReactions;
	} GapgenerationSolution;

###ModelTemplate
####Description 
ModelTemplate object holds data on how a model is constructed from an annotation

####Relationships

	/*
	Reference to a mapping object
	@id ws KBaseOntology.Mapping
	*/
	typedef string mapping_ref;
	
	/*
	Reference to a biochemistry object
	@id ws KBaseBiochem.Biochemistry
	*/
	typedef string Biochemistry_ref;
	
	/*
	Template reaction ID
	@id external
	*/
	typedef string templatereaction_id;
	
	/*
	Reference to a reaction object in a biochemistry
	@id subws KBaseBiochem.Biochemistry.reactions.[*].id
	*/
	typedef string reaction_ref;
	
	/*
	Reference to a compartment object
	@id subws KBaseBiochem.Biochemistry.compartments.[*].id
	*/
	typedef string compartment_ref;
	
	/*
	Reference to a complex object
	@id subws KBaseOntology.Mapping.complexes.[*].id
	*/
	typedef string complex_ref;
	
	/*
	Reference to a compound object
	@id subws KBaseBiochem.Biochemistry.compounds.[*].id
	*/
	typedef string compound_ref;

####Fields

	typedef structure {
	  modeltemplate_id id; (string)
	  string name;
	  string modelType;
	  string domain;
	  mapping_ref mapping_ref;
	  Biochemistry_ref biochemistry_ref;
	  list<TemplateReaction> templateReactions; (see below)
	  list<TemplateBiomass> templateBiomasses; (see below)
	} ModelTemplate;
	
	typedef structure {
	  templatereaction_id id;
	  reaction_ref reaction_ref;
	  compartment_ref compartment_ref;
	  list<complex_ref> complex_refs;
	  string direction;
	  string GapfillDirection;
	  string type;
	  float base_cost;
	  float forward_penalty;
	  float reverse_penalty;
	} TemplateReaction;
	
	typedef structure {
	  templatebiomasscomponent_id id;
	  string class;
	  compound_ref compound_ref;
	  compartment_ref compartment_ref;
	  string coefficientType;
	  float coefficient;
	  list<compound_ref> linked_compound_refs;
	  list<float> link_coefficients;
	} TemplateBiomassComponent;
	
	typedef structure {
	  templatebiomass_id id;
	  string name;
	  string type;
	  float other;
	  float dna;
	  float rna;
	  float protein;
	  float lipid;
	  float cellwall;
	  float cofactor;
	  float energy;
	  list<TemplateBiomassComponent> templateBiomassComponents;
	} TemplateBiomass;

###PromConstraint
####Description 
An object that encapsulates the information necessary to apply PROM-based constraints to an FBA model. This
includes a regulatory network consisting of a set of regulatory interactions (implied by the set of TFtoTGmap
objects) and interaction probabilities as defined in each TargetGeneProbabilities object.  A link the the annotation
object is required in order to properly link to an FBA model object.  A reference to the expression_data_collection
used to compute the interaction probabilities is provided for future reference.


####Relationships

	/*
	Reference to a model template
	@id ws KBaseGenomes.Genome
	*/
	typedef string genome_ref;
	
	/*
	Reference to expression data
	@id ws KBaseExpression.ExpressionSeries
	*/
	typedef string expression_series_ref;
	
	/*
	Reference to regulome
	@id ws KBaseRegulation.Regulome
	*/
	typedef string regulome_ref;

####Fields

	typedef structure {
	  string id;
	  genome_ref genome_ref;
	  list<TFtoTGmap> transcriptionFactorMaps; (see below)
	  expression_series_ref expression_series_ref;
	  regulome_ref regulome_ref;
	} PromConstraint;
	
	typedef structure {
	  string transcriptionFactor_ref;
	  list<TargetGeneProbabilities> targetGeneProbs;
	} TFtoTGmap;
	
	typedef structure {
	  string target_gene_ref;
	  float probTGonGivenTFoff;
	  float probTGonGivenTFon;
	} TargetGeneProbabilities;

###ReactionSensitivityAnalysis
####Description 
Object for holding reaction knockout sensitivity results

####Relationships

	/*
	Reference to metabolic model
	@id ws KBaseFBA.FBAModel
	*/
	typedef string fbamodel_ref;
	
	/*
	Reference to a reaction object in a model
	@id subws KBaseFBA.FBAModel.modelreactions.[*].id
	*/
	typedef string modelreaction_ref;

####Fields

	typedef structure {
	  string id;
	  fbamodel_ref fbamodel_ref;
	  string type;
	  bool deleted_noncontributing_reactions; (int)
	  bool integrated_deletions_in_model; (int)
	  list<ReactionSensitivityAnalysisReaction> reactions; (see below)
	  list<ReactionSensitivityAnalysisCorrectedReaction> corrected_reactions; (see below)
	} ReactionSensitivityAnalysis;
	
	typedef structure {
	  modelreaction_ref modelreaction_ref;
	  float normalized_required_reaction_count;
	  list<modelreaction_id> required_reactions;
	} ReactionSensitivityAnalysisCorrectedReaction;
	
	typedef structure {
	  string id;
	  modelreaction_ref modelreaction_ref;
	  float growth_fraction;
	  bool delete; (int)
	  bool deleted; (int)
	  string direction;
	  float normalized_activated_reaction_count;
	  list<modelcompound_id> biomass_compounds; (strings)
	  list<modelreaction_id> new_inactive_rxns; (strings)
	  list<feature_id> new_essentials; (strings)
	} ReactionSensitivityAnalysisReaction;


#Types for Biochem.spec

##Workspace Module
KBaseBiochem

##Workspace with Data
?

###Biochemistry
####Description 
Biochemistry object

####Relationships

	/*
	Reference to a compound object in a biochemistry
	@id subws KBaseBiochem.Biochemistry.compounds.[*].id
	*/
	typedef string compound_ref;
	
	/*
	Reference to a reaction object in a biochemistry
	@id subws KBaseBiochem.BiochemistryStructures.structures.[*].id
	*/
	typedef string structure_ref;
	
	/*
	Reference to a cue object in a biochemistry
	@id subws KBaseBiochem.Biochemistry.cues.[*].id
	*/
	typedef string cue_ref;
	
	/*
	Reference to a reaction object in a biochemistry
	@id subws KBaseBiochem.Biochemistry.reactions.[*].id
	*/
	typedef string reaction_ref;
	
	/*
	Reference to a compartment object in a biochemistry
	@id subws KBaseBiochem.Biochemistry.compartments.[*].id
	*/
	typedef string compartment_ref;

####Fields

	typedef structure {
	  biochem_id id; (string)
	  string name;
	  string description;
	  list<Compartment> compartments; (see below)
	  list<Compound> compounds; (see below)
	  list<Reaction> reactions; (see below)
	  list<ReactionSet> reactionSets; (see below)
	  list<CompoundSet> compoundSets; (see below)
	  list<Cue> cues; (see below)
	  mapping<compound_id, mapping<string, list<string>>> compound_aliases;
	  mapping<reaction_id, mapping<string, list<string>>> reaction_aliases;
	} Biochemistry;
	
	typedef structure {
	  cue_id id; (string)
	  string name;
	  string abbreviation;
	  string formula;
	  string unchargedFormula;
	  float mass;
	  float defaultCharge;
	  float deltaG;
	  float deltaGErr;
	  bool smallMolecule; (int)
	  int priority;
	  string structure_key;
	  string structure_data;
	  string structure_type;
	} Cue;
	
	typedef structure {
	  compoundset_id id;
	  string name;
	  string class;
	  string type;
	  list<compound_ref> compound_refs;
	} CompoundSet;
	
	typedef structure {
	  reactionset_id id;
	  string name;
	  string class;
	  string type;
	  list<reaction_ref> reaction_refs;
	} ReactionSet;
	
	typedef structure {
	  reaction_id id;
	  string name;
	  string abbreviation;
	  string md5;
	  string direction;
	  string thermoReversibility;
	  string status;
	  float defaultProtons;
	  float deltaG;
	  float deltaGErr;
	  reaction_ref abstractReaction_ref;
	  mapping<cue_ref, float> cues;
	  list<Reagent> reagents; (see below)
	} Reaction;
	
	typedef structure {
	  compound_ref compound_ref;
	  compartment_ref compartment_ref;
	  float coefficient;
	  bool isCofactor;
	} Reagent;
	
	typedef structure {
	  compound_id id;
	  bool isCofactor;
	  string name;
	  string abbreviation;
	  string md5;
	  string formula;
	  string unchargedFormula;
	  float mass;
	  float defaultCharge;
	  float deltaG;
	  float deltaGErr;
	  compound_ref abstractCompound_ref;
	  list<compound_ref> comprisedOfCompound_refs;
	  structure_ref structure_ref;
	  mapping<cue_ref, float> cues;
	  mapping<int, list<float>> pkas;
	  mapping<int, list<float>> pkbs;
	} Compound;
	
	typedef structure {
	  compartment_id id;
	  string name;
	  int hierarchy;
	} Compartment;

###BiochemistryStructures
####Description 
BiochemistryStructures object

####Relationships
None

####Fields

	typedef structure {
	  biochemstruct_id id; (string)
	  string name;
	  string description;
	  list<CompoundStructure> structures; (see below)
	} BiochemistryStructures;
	
	typedef structure {
	  structure_id id; (string)
	  string type;
	  string data;
	} CompoundStructure;

###Media
####Description 
Media object

####Relationships

	/*
	Reference to a compound object in a biochemistry
	@id subws KBaseBiochem.Biochemistry.compounds.[*].id
	*/
	typedef string compound_ref;

####Fields

	typedef structure {
	  media_id id; (string)
	  string name;
	  source_id source_id;
	  string source;
	  string protocol_link;
	  bool isDefined; (int)
	  bool isMinimal; (int)
	  bool isAerobic; (int)
	  string type;
	  string pH_data;
	  float temperature;
	  string atmosphere;
	  string atmosphere_addition;
	  list<MediaReagent> reagents; (see below)
	  list<MediaCompound> mediacompounds; (see below)
	} Media;
	
	typedef structure {
	  string id;
	  string name;
	  float concentration;
	  string concentration_units;
	  float molecular_weight;
	  mapping<string, float> associated_compounds;
	} MediaReagent;
	
	typedef structure {
	  compound_ref compound_ref;
	  float concentration;
	  float maxFlux;
	  float minFlux;
	} MediaCompound;

###MetabolicMap
####Description 
Metabolic Map object

####Relationships

	/*
	Reference to a compound object in a metabolic map
	@id subws KBaseBiochem.MetabolicMap.compounds.[*].id
	*/
	typedef string mapcompound_ref;
	
	/*
	Reference to a compound object in a metabolic map
	@id subws KBaseBiochem.MetabolicMap.linkedmaps.[*].id
	*/
	typedef string maplink_ref;

####Fields

	typedef structure {
	  map_id id; (string)
	  string name;
	  string source_id;
	  string source;
	  string link;
	  string description;
	  list<string> reaction_ids;
	  list<string> compound_ids;
	  list<ReactionGroup> groups; (see below)
	  list<MapReaction> reactions; (see below)
	  list<MapCompound> compounds; (see below)
	  list<MapLink> linkedmaps; (see below)
	} MetabolicMap;
	
	typedef structure {
	  list<string> rxn_ids;
	  int x;
	  int y;
	  list<tuple<int, int>> substrate_path;
	  list<tuple<int, int>> product_path;
	  string spline;
	  string dasharray;
	} ReactionGroup;
	
	typedef structure {
	  int id;
	  mapcompound_ref compound_ref;
	} MapReactionReactant;
	
	typedef structure {
	  string id;
	  bool reversible;
	  string name;
	  string ec;
	  string shape;
	  string link;
	  int h;
	  int w;
	  int y;
	  int x;
	  list<string> rxns;
	  list<MapReactionReactant> substrate_refs;
	  list<MapReactionReactant> product_refs;
	} MapReaction;
	
	typedef structure {
	  string id;
	  string label;
	  int label_x;
	  int label_y;
	  string name;
	  string shape;
	  string link;
	  int h;
	  int w;
	  int y;
	  int x;
	  list<string> cpds;
	  list<maplink_ref> link_refs;
	} MapCompound;
	
	typedef structure {
	  string id;
	  string map_ref;
	  string name;
	  string shape;
	  string link;
	  int h;
	  int w;
	  int y;
	  int x;
	  map_id map_id;
	} MapLink;

#Types for Expression.spec
This is copied from the expression module.  Since this is a copy the spec may inconsistent with the actual WS spec.
Please see https://github.com/kbase/design_docs/blob/master/data/Expression.md


#Types for Genome.spec

##Workspace Module
KBaseGenomes

##Workspace with Data
KBasePublicGenomesV5

###Genome
####Description 
Genome object

####Relationships

	/*
	Reference to a ContigSet object containing the contigs for this genome in the workspace
	    @id ws KBaseGenomes.ContigSet
	*/
	typedef string ContigSet_ref;

####Fields
	
	typedef structure {
	  Genome_id id; (string)
	  string scientific_name;
	  string domain;
	  int genetic_code;
	  int dna_size;
	  int num_contigs;
	  list<Contig> contigs; (see below)
	  list<int> contig_lengths;
	  list<Contig_id> contig_ids; strings
	  string source;
	  source_id source_id;
	  string md5;
	  string taxonomy;
	  float gc_content;
	  int complete;
	  list<publication> publications; (see below)
	  list<Feature> features; (see below)
	  ContigSet_ref contigset_ref; 
	  Genome_quality_measure quality;
	  list<Close_genome> close_genomes; (see below) 
	  list<Analysis_event> analysis_events; (see below)
	} Genome;
	
	typedef structure {
	  Contig_id id;
	  int length;
	  string md5;
	  string sequence;
	  int genetic_code;
	  string cell_compartment;
	  string replicon_type;
	  string replicon_geometry;
	  string name;
	  string description;
	  Bool complete;
	} Contig;
	
	typedef tuple<int, string, string, string, string, string, string> publication;
	
	typedef structure {
	  float frameshift_error_rate;
	  float sequence_error_rate;
	} Genome_quality_measure;
	
	typedef structure {
	  Genome_id genome;
	  float closeness_measure;
	} Close_genome;
	
	typedef structure {
	  Analysis_event_id id;
	  string tool_name;
	  float execution_time;
	  list<string> parameters;
	  string hostname;
	} Analysis_event;
	
	See Feature in the Feature section below.


###Feature
####Description 
Feature object. Structure for a single feature of a genome

####Relationships
None

####Fields

	typedef structure {
	  Feature_id id;
	  list<tuple<Contig_id, int, string, int>> location;
	  string type;
	  string function;
	  string md5;
	  string protein_translation;
	  string dna_sequence;
	  int protein_translation_length;
	  int dna_sequence_length;
	  list<publication> publications;
	  list<string> subsystems;
	  list<ProteinFamily> protein_families;
	  list<string> aliases;
	  list<tuple<string, float>> orthologs;
	  list<annotation> annotations;
	  list<subsystem_data> subsystem_data;
	  list<regulon_data> regulon_data;
	  list<atomic_regulon> atomic_regulons;
	  list<coexpressed_fid> coexpressed_fids;
	  list<co_occurring_fid> co_occurring_fids;
	  Feature_quality_measure quality;
	  Analysis_event feature_creation_event;
	} Feature;
	
	publication is the same as in the Genome object above. 
	
	/*
	Structure for a protein family
	        @optional query_begin query_end subject_begin subject_end score evalue subject_description release_version
	*/
	typedef structure {
	  string id;
	  string subject_db;
	  string release_version;
	  string subject_description;
	  int query_begin;
	  int query_end;
	  int subject_begin;
	  int subject_end;
	  float score;
	  float evalue;
	} ProteinFamily;
	
	typedef tuple<string, string, float> annotation;
	
	/*
	Structure for subsystem data (from CDMI API)
	*/
	typedef tuple<string, string, string> subsystem_data;
	
	/*
	Structure for regulon data (from CDMI API)
	*/
	typedef tuple<string, list<Feature_id>, list<Feature_id>> regulon_data;
	
	/*
	Structure for an atomic regulon (from CDMI API)
	*/
	typedef tuple<string, int> atomic_regulon;
	
	/*
	Structure for coexpressed fids (from CDMI API)
	*/
	typedef tuple<Feature_id, float> coexpressed_fid;
	
	/*
	Structure for co-occurring fids (from CDMI API)
	*/
	typedef tuple<Feature_id, float> co_occurring_fid;
	
	/*
	@optional weighted_hit_count hit_count existence_priority overlap_rules pyrrolysylprotein truncated_begin truncated_end existence_confidence frameshifted selenoprotein
	*/
	typedef structure {
	  Bool truncated_begin; (int)
	  Bool truncated_end; (int)
	  float existence_confidence;
	  Bool frameshifted; (int)
	  Bool selenoprotein; (int)
	  Bool pyrrolysylprotein; (int)
	  list<string> overlap_rules;
	  float existence_priority;
	  float hit_count;
	  float weighted_hit_count;
	} Feature_quality_measure;
	
	Analysis_event is the same as in the Genome object above. 

###ContigSet
####Description 
Some top level info about the contig set and then details for each contig.  Essentially is an assembly.

####Relationships

	/*
	Reference to a reads file in shock
	@id shock
	*/
	typedef string Reads_ref;
	
	/*
	Reference to a fasta file in shock
	@id shock
	*/
	typedef string Fasta_ref;


####Fields

	typedef structure {
	  ContigSet_id id;
	  string name;
	  string md5;
	  source_id source_id;
	  string source;
	  string type;
	  Reads_ref reads_ref;
	  Fasta_ref fasta_ref;
	  list<Contig> contigs; (see below)
	} ContigSet;
	
	typedef structure {
	  Contig_id id;
	  int length;
	  string md5;
	  string sequence;
	  int genetic_code;
	  string cell_compartment;
	  string replicon_type;
	  string replicon_geometry;
	  string name;
	  string description;
	  Bool complete; (int)
	} Contig;


###GenomeComparison
####Description 
GenomeComparisonData object: this object holds information about a multigenome comparison.
NOTE: This is not the same thing as the ProteomeComparison object in the GenomeComparisonRepo.

####Relationships

	Reference to a Proteome Comparison object in the workspace
	@id ws GenomeComparison.ProteomeComparison
	*/
	typedef string Protcomp_ref;
	
	/*
	Reference to a Pangenome object in the workspace
	@id ws KBaseGenomes.Pangenome
	*/
	typedef string Pangenome_ref;
	
	/*
	Reference to a Genome object in the workspace
	@id ws KBaseGenomes.Genome
	*/
	typedef string Genome_ref;

####Fields

	typedef structure {
	  string id;
	  string name;
	  int core_functions;
	  int core_families;
	  Protcomp_ref protcomp_ref;
	  Pangenome_ref pangenome_ref;
	  list<GenomeComparisonGenome> genomes; (see below)
	  list<GenomeComparisonFamily> families; (see below)
	  list<GenomeComparisonFunction> functions; (see below)
	} GenomeComparison;
	
	typedef structure {
	  int core;
	  mapping<string, list<tuple<Feature_id, int, float>>> genome_features;
	  string id;
	  list<tuple<Reaction_id, string>> reactions;
	  string subsystem;
	  string primclass;
	  string subclass;
	  int number_genomes;
	  float fraction_genomes;
	  float fraction_consistent_families;
	  string most_consistent_family;
	} GenomeComparisonFunction;
	
	typedef structure {
	  int core;
	  mapping<string, list<tuple<Feature_id, list<int>, float>>> genome_features;
	  string id;
	  string type;
	  string protein_translation;
	  int number_genomes;
	  float fraction_genomes;
	  float fraction_consistent_annotations;
	  string most_consistent_role;
	} GenomeComparisonFamily;
	
	typedef structure {
	  string id;
	  Genome_ref genome_ref;
	  mapping<string, tuple<int, int>> genome_similarity;
	  string name;
	  string taxonomy;
	  int features;
	  int families;
	  int functions;
	} GenomeComparisonGenome;


###GenomeDomainData
####Description 
GenomeDomainData object: this object holds all data regarding protein domains in a genome in KBase

####Relationships

	/*
	Reference to a Genome object in the workspace
	@id ws KBaseGenomes.Genome
	*/
	typedef string Genome_ref;

####Fields

	typedef structure {
	  string id;
	  Genome_id genome_id;
	  string scientific_name;
	  Genome_ref genome_ref;
	  int num_domains;
	  int num_features;
	  list<Domain> domains; (see below)
	  list<FeatureDomainData> featuredomains; (see below)
	} GenomeDomainData;
	
	typedef structure {
	  string id;
	  string source_id;
	  string type;
	  string name;
	  string description;
	} Domain;
	
	/*
	FeatureDomain - a subobject holding information on how a domain appears in a gene
	*/
	typedef structure {
	  string id;
	  string feature_id;
	  string feature_ref;
	  string function;
	  int feature_length;
	  list<tuple<string, int, int, int, int, float, float, float, float, float, float>> domains;
	} FeatureDomainData;

###MetagenomeAnnotation
####Description 
MetagenomeAnnotation

####Relationships
None

####Fields

	typedef structure {
	  string type;
	  string name;
	  string id;
	  string source_id;
	  string source;
	  string confidence_type;
	  list<MetagenomeAnnotationOTU> otus; (see below)
	} MetagenomeAnnotation;
	
	typedef structure {
	  string id;
	  list<string> reference_genes;
	  string functional_role;
	  int abundance;
	  float confidence;
	} MetagenomeAnnotationOTUFunction;
	
	typedef structure {
	  float ave_confidence;
	  float ave_coverage;
	  string id;
	  string name;
	  string source_id;
	  string source;
	  list<MetagenomeAnnotationOTUFunction> functions; (see above)
	} MetagenomeAnnotationOTU;

###Pangenome
####Description 
Pangenome object: this object holds all data regarding a pangenome

####Relationships

	/*
	Reference to a Genome object in the workspace
	@id ws KBaseGenomes.Genome
	*/
	typedef string Genome_ref;

####Fields

	typedef structure {
	  string id;
	  string name;
	  string type;
	  list<Genome_ref> genome_refs;
	  list<OrthologFamily> orthologs;
	} Pangenome;
	
	typedef structure {
	  string id;
	  string type;
	  string function;
	  string md5;
	  string protein_translation;
	  list<tuple<string, float, string>> orthologs;
	} OrthologFamily;
	
###ProbabilisticAnnotation
####Description 
Object to carry alternative functions and probabilities for genes in a genome    

####Relationships

	/*
	Reference to a Genome object in the workspace
	@id ws KBaseGenomes.Genome
	*/
	typedef string Genome_ref;


####Fields

	typedef structure {
	  ProbabilisticAnnotation_id id;
	  Genome_ref genome_ref;
	  mapping<Feature_id, list<function_probability>> roleset_probabilities; (see below)
	  list<Feature_id> skipped_features;
	} ProbabilisticAnnotation; (strings)
	
	/*
	A function_probability is a (annotation, probability) pair associated with a gene
	An annotation is a "///"-delimited list of roles that could be associated with that gene.
	*/
	typedef tuple<string, float> function_probability;

#Types for GenomeComparison.spec
This is copied from the GenomeComparison repo module.  Since this is a copy the spec may inconsistent with the actual WS spec.
Please see https://github.com/kbase/genome_comparison/blob/master/GenomeComparison.spec
NOTE: This is not the same thing as the GenomeComparison object in the KBaseFBAModeling repo Genomes spec that contains a GenomeComparison typed object.


#Types for Metabolome.spec

##Workspace Module - NOTE THE SPEC EXISTS BUT THERE APPEARS TO BE NO REGISTERED WS OBJECTS
Unknown 

##Workspace with Data
Unknown

##Author
I think Sam Seaver made this part.

###MetabolomeSample
####Description 
This appears to be a similar data object to the ExpressionSample.  I am quessing he is making this type to put his stuff into the expression sample.

####Relationships

####Fields

	    typedef structure {
	        string id;
	        string source_id;
	        sample_type type;
	        string numerical_interpretation;
	        string description;
	        string title;
	        int data_quality_level;
	        float original_median;
		string external_source_date;
	        data_metabolome_levels_for_sample metabolome_levels; 
		biochemistry_id biochemistry_id; 
	        metabolome_ontology_terms metabolome_ontology_terms;
	        metabolome_sample_id default_control_sample; 
	        metabolome_sample_ids averaged_from_samples; 
	        Protocol protocol; 
	        Strain strain; 
	        persons persons;
	        string data_source; 
	        string shock_url;
	        string processing_comments;
	        metabolome_series_ids metabolome_series_ids;
	        string characteristics;
	    } MetabolomeSample;


###MetabolomeSeries
####Description 
This appears to be a similar data object to the ExpressionSeries.  But instead of mapping samples to genomes it appears to be mapping samples to biochemistries.

####Relationships

	    /* 
	        KBase BiochemistryID 
	        id ws KB.Biochmistry
	
	        "ws" may change to "to" in the future 
	    */
	    typedef string biochemistry_id;

####Fields

	    typedef structure { 
	        string id; 
	        string source_id;
	        biochemistry_metabolome_sample_ids_map biochemistry_metabolome_sample_ids_map; (see below)
	        string title; 
	        string summary;
	        string design; 
	        string publication_id; 
		string external_source_date;
	    } MetabolomeSeries; 
	    
	    /* map between biochemistry ids and a list of samples from that biochemistry in this sample */
	    typedef mapping<biochemistry_id biochemistry_id, metabolome_sample_ids> biochemistry_metabolome_sample_ids_map; 


###MetabolomeReplicateGroup
####Description 
This appears to be a similar data object to the ExpressionReplicateGroup.  

####Relationships

	    /*
	       id for the metabolome sample
	
	       @id ws KBaseMetabolome.MetabolomeSample
	
	       "ws" may go to "to" in the future
	    */
	    typedef string metabolome_sample_id;

####Fields

	    typedef structure {
	        string id;
	        metabolome_sample_ids metabolome_sample_ids;
	    } MetabolomeReplicateGroup;


#Types for Ontology.spec
This is copied from the ontology_service repo module.  Since this is a copy the spec may inconsistent with the actual WS spec.
Please see https://github.com/kbase/ontology_service/blob/master/workspace.spec


#Types for Phenotypes.spec

##Workspace Module - 
KBasePhenotypes

##Workspace with Data
Unknown


###PhenotypeSet
####Description 
PhenotypeSet object contains a set of phenotype objects

####Relationships

	/*
	Reference to a feature of a genome object
	@id ws KBaseGenomes.Genome
	*/
	typedef string genome_ref;
	
	/*
	Reference to a mapping object
	@id ws KBaseBiochem.Media
	*/
	typedef string media_ref;
	
	/*
	Reference to a feature of a genome object
	@id subws KBaseGenomes.Genome.features.[*].id
	*/
	typedef string feature_ref;
	
	/*
	Reference to a compound object
	@id subws KBaseBiochem.Biochemistry.compounds.[*].id
	*/
	typedef string compound_ref;

####Fields

	typedef structure {
	  phenotypeset_id id;
	  source_id source_id;
	  string source;
	  string name;
	  genome_ref genome_ref;
	  list<Phenotype> phenotypes; (see below)
	  string importErrors;
	  string type;
	} PhenotypeSet;
	
	typedef structure {
	  phenotype_id id;
	  media_ref media_ref;
	  list<feature_ref> geneko_refs;
	  list<compound_ref> additionalcompound_refs;
	  float normalizedGrowth;
	  string name;
	} Phenotype;

###PhenotypeSimulationSet
####Description 
PhenotypeSimulationSet object holds data on simulations of many phenotypes

####Relationships

	/*
	Reference to a model object
	@id ws KBaseFBA.FBAModel
	*/
	typedef string fbamodel_ref;
	
	/*
	Reference to a PhenotypeSet object
	@id ws KBasePhenotypes.PhenotypeSet
	*/
	typedef string phenotypeset_ref;
	
	/*
	Reference to a PhenotypeSet object
	@id subws KBasePhenotypes.PhenotypeSet.phenotypes.[*].id
	*/
	typedef string phenotype_ref;

####Fields

	typedef structure {
	  phenosimset_id id;
	  fbamodel_ref fbamodel_ref;
	  phenotypeset_ref phenotypeset_ref;
	  list<PhenotypeSimulation> phenotypeSimulations; (see below)
	} PhenotypeSimulationSet;
	
	typedef structure {
	  phenosim_id id;
	  phenotype_ref phenotype_ref;
	  float simulatedGrowth;
	  float simulatedGrowthFraction;
	  int numGapfilledReactions;
	  list<string> gapfilledReactions;
	  string phenoclass;
	} PhenotypeSimulation;

#Types for ProbabilisticAnnotation.spec

##Workspace Module - 
ProbabilisticAnnotation

##Author 
Mike Mundy

##Workspace with Data
Unknown

###ProbAnno
####Description 
Object to carry alternative functions and probabilities for genes in a genome   

####Relationships

	NOTE THESE ARE NOT WS REFERENCES
	
	/*
	A string identifier for a genome.
	*/
	typedef string genome_id;
	
	/*
	A string identifier for a workspace. Any string consisting of alphanumeric characters and "-" is acceptable.
	*/
	typedef string workspace_id;

####Fields

	typedef structure {
	  probanno_id id;
	  genome_id genome;
	  workspace_id genome_workspace;
	  mapping<feature_id, list<function_probability>> roleset_probabilities; (see below)
	  list<feature_id> skipped_features; (strings)
	} ProbAnno;
	
	/*
	A function_probability is a (annotation, probability) pair associated with a gene
	An annotation is a "///"-delimited list of roles that could be associated with that gene.
	*/
	typedef tuple<string, float> function_probability;

###RxnProbs
####Description 
Object to hold reaction probabilities for a genome  

####Relationships

	NOTE THESE ARE NOT WS REFERENCES
	
	/*
	A string identifier for a workspace. Any string consisting of alphanumeric characters and "-" is acceptable.
	*/
	typedef string workspace_id;
	
	/*
	A string identifier for a genome.
	*/
	typedef string genome_id;
	
	/*
	A string identifier for a probabilistic annotation object.
	*/
	typedef string probanno_id;
	
	/*
	A string identifier for a reaction object.
	*/
	typedef string reaction_id;

####Fields

	typedef structure {
	  rxnprobs_id id; (string)
	  template_id template_model;
	  workspace_id template_workspace;
	  genome_id genome; (string, not ws reference)
	  workspace_id genome_workspace; (string, not ws reference)
	  probanno_id probanno; (string, not ws reference)
	  workspace_id probanno_workspace; (string, not ws reference)
	  list<reaction_probability> reaction_probabilities; (see below)
	} RxnProbs;
	
	/*
	Data structure to hold probability of a reaction
	
	        reaction_id reaction - ID of the reaction
	        float probability - Probability of the reaction
	        string type - Type of complexes ("HASCOMPLEXES" or "NOCOMPLEXES")
	        string complex_info - Detailed information on complexes
	        string gene_list - List of genes most likely to be attached to reaction
	*/
	typedef tuple<reaction_id, float, string, string, string> reaction_probability;


#Types for Regulation.spec

##Workspace Module - 
KBaseRegulation

I suspect this is copied from another repo, and therefore has the possibility of being inconsistent

##Author
Pavel

##Workspace with Data
Unknown


###Regulome
####Description 
Represents regulome - collection of regulons for a given genome

####Relationships

	/*
	Represents WS reference to a genome object
	@id ws KBaseGenomes.Genome
	*/
	typedef string genome_ref;

####Fields

	typedef structure {
	  regulome_id regulome_id;
	  regulome_source regulome_source;
	  string regulome_name;
	  Genome genome;
	  list<Regulon> regulons; (see below)
	  list<Evidence> evidesnces; (see below)
	} Regulome;
	
	typedef structure {
	  regulon_id regulon_id;
	  Regulator regulator; (see below)
	  list<Effector> effectors; (see below)
	  list<TranscriptionFactor> tfs; (see below)
	  list<RegulatedOperon> operons; (see below)
	  list<Evidence> evidesnces; (see below)
	} Regulon;
	
	typedef structure {
	  operon_id operon_id;
	  list<Gene> genes; (see below)
	  list<RegulatorySite> sites; (see below)
	} RegulatedOperon;
	
	typedef structure {
	  regulatory_site_id regulatory_site_id;
	  string sequence;
	  int position;
	  float score;
	  regulatory_mechanism regulatory_mechanism;
	  list<Evidence> evidesnces; (note misspelled)
	} RegulatorySite;
	
	typedef structure {
	  evidence_type evidence_type;
	  string pubmed_id;
	} Evidence;
	
	typedef structure {
	  gene_id gene_id;
	  string locus_tag;
	  string name;
	} Gene;
	
	typedef structure {
	  transcription_factor_id transcription_factor_id;
	  string locus_tag;
	  string name;
	} TranscriptionFactor;
	
	typedef structure {
	  effector_id effector_id;
	  string effector_class;
	  string effector_name;
	} Effector;
	
	typedef structure {
	  regulator_id regulator_id;
	  regulation_type regulation_type;
	  string regulator_name;
	  string taxonomy;
	  string tf_family;
	  string rfam_id;
	} Regulator;
	
	typedef structure {
	  genome_id genome_id;
	  genome_ref genome_ref;
	  string genome_name;
	  int ncbi_taxonomy_id;
	} Genome;

#Types for RegulatoryFBA.spec
##Workspace Module - THIS DOES NOT APPEAR TO BE REGISTERED WITH THE WORKSPACE AT ALL
Unknown 

##Workspace with Data
Unknown

The spec itself is very small and is below:

	module KBaseRegulatoryFBA {
	     /*
	      Genome feature
	      */
	    typedef string feature_id;
	    /*
	      Expresion sample id
	    */
	    typedef string expression_sample_id;
	    /*
	      collection of eflux expression scores for each feature in a genome,
	      representing a single gene expression sample
	    */
	    typedef structure {
		    mapping<feature_id, float> eflux_scores;
		    string expression_sample_ref;
	    } EfluxExpressionSample
	    /*
	      Eflux values computed for an entire gene expression series
	    */
	    typedef structure {
		string eflux_collection_id;
		mapping<expression_sample_id, EfluxExpressionSample> efluxExpressionSamples;
	    } EfluxExpressionCollection;
	};































































































