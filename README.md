# jbi_sample_conversions
Sample conversion rules and proofs as a demonstration for our JBI submission


##FILES:

source-to-domain conversion:

source_entity.ttl contains sample source entity data, as displayed in Listing 2 of the paper.

source_to_domain_conversion_rule.n3 contains sample source to domain conversion rule, as displayed in Lisiting 3 of the paper.

source_to_domain_query_rule.n3q contains a sample filtering rule, which passes only the triples generated by the conversion rule (domain entity) as output result. A conversion rule only adds inferenced triples to the input data, a filtering rule is required if the input data (in this example, the source_entity) needs to be excluded from the output result.

domain-to-application conversion:

domain_entity.ttl contains sample domain entity data, the content is consistent to Listing 4 of the paper, the difference is that the domain_entity.ttl file in this project is generated from the source-to-domain conversion.

domain_to_OMOP_conversion_rule.n3 contains sample domain to OMOP conversion rule, as displayed in Listing 5 of the paper.

domain_to_OMOP_query_rule.n3q contains a sample filtering rule, which passes only the triples generated by the conversion rule (OMOP entity) as output result.


##CONVERSION

The results are generated by EYE with the following commands:

source-to-domain conversion:
eye --nope source_entity.ttl source_to_domain_conversion_rule.n3 --query source_to_domain_query_rule.n3q >domain_entity.ttl

The content of the domain_entity.ttl is as displayed in Listing 4. 

domain-to-application conversion:
eye --nope domain_entity.ttl domain_to_OMOP_conversion_rule.n3 --query domain_to_OMOP_query_rule.n3q >OMOP_entity.ttl

The content of OMO_entity.ttl is as displayed in Listing 6.


##PROOF

As introduced in the paper, EYE can also generate proof for the conversion process.
The commands below generates proofs for the above mentioned conversion processes

eye source_entity.ttl source_to_domain_conversion_rule.n3 --query source_to_domain_query_rule.n3q >source_to_domain_proof.n3

eye domain_entity.ttl domain_to_OMOP_conversion_rule.n3 --query domain_to_OMOP_query_rule.n3q >domain_to_omop_proof.n3


In the generated proofs, the object of r:gives shows the conclusions of a conversion process, as what displayed in domain_entity.ttl or OMOP_entity.ttl.
The remaining of the proofs records actions such as data extractions or inferences that leads to the conclusions.
