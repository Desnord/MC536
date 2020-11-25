## Tarefa de análises feitas no Cypher

## Exercício 1
Calcule o Pagerank do exemplo da Wikipedia em Cypher:

~~~cypher
LOAD CSV WITH HEADERS FROM 'https://raw.githubusercontent.com/santanche/lab2learn/master/network/pagerank/pagerank-wikipedia.csv' AS line

MERGE (p1:page {name:line.source})
MERGE (p2:page {name:line.target})
CREATE (p1)-[:link]->(p2)

CALL gds.graph.create('pagerank','page','link')

CALL gds.pageRank.stream('pagerank')
YIELD nodeId, score
RETURN gds.util.asNode(nodeId).name AS name, score
ORDER BY score DESC
~~~

## Exercício 2
Departing from a Drug-Drug graph created in a previous lab, whose relationship determines drugs taken together, apply a community detection in it to see the results:

~~~cypher
(escreva aqui a resolução em Cypher)
~~~
