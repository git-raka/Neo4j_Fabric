# fabric


## CONFIGURATION REFERENCES

https://neo4j.com/docs/operations-manual/current/fabric/queries/ 

https://neo4j.com/docs/operations-manual/current/tutorial/fabric-tutorial/

https://neo4j.com/blog/getting-started-with-neo4j-fabric/


## neo4j.conf

dbms.mode=SINGLE

fabric.database.name=fabric

#fabric.routing.servers=server1:7687,server2:7687

fabric.graph.0.name=nonebp1

fabric.graph.0.uri=neo4j://13.213.9.193:7687,neo4j://18.138.58.226:7687,neo4j://13.213.68.70:7687

fabric.graph.0.database=nonebp1

fabric.graph.1.name=movies

fabric.graph.1.uri=neo4j://13.213.9.193:7687,neo4j://18.138.58.226:7687,neo4j://13.213.68.70:7687

fabric.graph.1.database=movies

fabric.graph.2.name=nonebp2

fabric.graph.2.uri=neo4j://13.229.248.26:7687,neo4j://54.151.255.109:7687,neo4j://13.213.44.173:7687

fabric.graph.2.database=nonebp2

fabric.graph.3.name=northwind

fabric.graph.3.uri=neo4j://13.229.248.26:7687,neo4j://54.151.255.109:7687,neo4j://13.213.44.173:7687

fabric.graph.3.database=northwind



DATABASES:

nonebp1
movies
nonebp2
northwind

## USING QUERIES

UNION

USE fabric.nonebp1
MATCH (n:NE_CUSTOMER) RETURN n.NOCUSTOMER, n.NAMACUSTOMER LIMIT 10
UNION
USE fabric.nonebp2
MATCH (n:NE_CUSTOMER) RETURN n.NOCUSTOMER, n.NAMACUSTOMER SKIP 10 LIMIT 10 


CORRELATE (Across Clusters)

CALL {
  USE fabric.nonebp1
  MATCH (n:NE_CUSTOMER)-[:HAS_KONTRAK]-(:NE_KONTRAK)
  RETURN n.NOCUSTOMER AS custId, n.NAMACUSTOMER LIMIT 100
}
CALL {
  USE fabric.nonebp2
  WITH custId
  MATCH (kontrak:NE_KONTRAK)
  WHERE kontrak.NOCUSTOMER = custId
  RETURN kontrak LIMIT 10
}
RETURN kontrak.NOKONTRAK, kontrak.TGLKONTRAK




## CREATE

USE fabric.nonebp1
CREATE (u:User {uid:1})



