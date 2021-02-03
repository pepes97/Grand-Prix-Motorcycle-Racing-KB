1. RETURN ALL MANAGERS WHO ARE BOTH TEAM MANAGER AND GENERAL MANAGER OF A SCUDERIA WHICH HAS HEADQUARTERS IN ITALY

PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>

PREFIX owl: <http://www.w3.org/2002/07/owl#>

PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>

PREFIX : <http://www.semanticweb.org/sveva/ontologies/2021/0/moto#>

SELECT DISTINCT ?m

WHERE { 	

		?m :isTeamManagerOf ?t.

		?m :isGeneralManagerOf ?s.

		?s :hasHeadquarterIn :Italy.
}

2. RETURN THE MANUFACTURERS AND ALL THE OFFICIAL TEAMS OF IT, AND IF THERE ARE ALSO SATELLITE TEAMS
	
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>

PREFIX owl: <http://www.w3.org/2002/07/owl#>

PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>

PREFIX : <http://www.semanticweb.org/sveva/ontologies/2021/0/moto#>

SELECT ?m ?o ?s

WHERE { 		

		?o :isOfficialTeamOf ?m.

		OPTIONAL {?s :isSatelliteTeamOf ?m.}

}

3. RETURN ALL TEAMS WHO HAVE RIDER WHO HAS WON AT LEAST ONE WORLD WORLD IN MOTOGP

PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>

PREFIX owl: <http://www.w3.org/2002/07/owl#>

PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>

PREFIX : <http://www.semanticweb.org/sveva/ontologies/2021/0/moto#>

SELECT DISTINCT ?t

WHERE { 	

	?rr rdfs:subClassOf :Rider.

	?p rdfs:subPropertyOf :isRiderOf.

	?r :hasWonMotoCategory :MotoGP.

	{?r rdf:type ?rr.

	?r ?p ?t.}

	union {?r rdf:type :Rider.

	             ?r :isRiderOf ?t}
}

4. RETURNS THE SPONSORS WHO ARE SPONSORS OF BOTH OFFICIAL TEAMS AND AT LEAST ONE SATELLITE TEAM AND ALSO,
THESE SPONSORS ARE ALSO SPONSORS OF RIDERS OF THOSE TEAMS.

PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>

PREFIX owl: <http://www.w3.org/2002/07/owl#>

PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>

PREFIX : <http://www.semanticweb.org/sveva/ontologies/2021/0/moto#>

SELECT DISTINCT ?s

	WHERE { 	
			?s :isOfficialSponsorOf ?t1.
			?s :isSatelliteSponsorOf ?t2.
			?s :isRiderSponsorOf ?r1.
			?s :isRiderSponsorOf ?r2.
			?r1 :isSeasonRiderOf ?t1.
			?r2 :isSeasonRiderOf ?t2.

		
	}

1. RETURN THE TEAMMATES AND THE CORRESPONDING TEAMS
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>

PREFIX owl: <http://www.w3.org/2002/07/owl#>

PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>

PREFIX : <http://www.semanticweb.org/sveva/ontologies/2021/0/moto#>

SELECT DISTINCT ?r1 ?r2 ?m

	WHERE { 		
		?r1 :isSeasonRiderOf ?m.
	        ?r2 :isSeasonRiderOf ?m.
		?r1 :name ?n1.
		?r2 :name ?n2.
		FILTER(?n1 < ?n2)	
}

6. RETURN ALL RIDERS OF THE SEASON AND THEIR AGE, WHO HAVE WON AT LEAST 20 RACES OR HAVE ARRIVED
SECONDS IN AT LEAST 30 RACES OR THIRD PARTIES IN AT LEAST 35 RACES


PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>

PREFIX owl: <http://www.w3.org/2002/07/owl#>

PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>

PREFIX : <http://www.semanticweb.org/sveva/ontologies/2021/0/moto#>


SELECT DISTINCT ?r ?a

WHERE{
    
	?sr  rdfs:subClassOf :Rider.
	?r rdf:type ?sr.
	?r :age ?a.
	{?r :first ?f.
	FILTER (?f > 20)}
	UNION {
		?r :second ?s
	                	FILTER(?s >30)}
	UNION {
		?r :third ?t.
		FILTER(?t >35)}			
}
