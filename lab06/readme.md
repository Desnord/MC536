## Tarefa de Cypher e o FDA Adverse Event Reporting System (FAERS)

## Exercício 1

Escreva uma sentença em Cypher que crie o medicamento de nome `Metamizole`, código no DrugBank `DB04817`.

### Resolução
~~~cypher
CREATE (:Drug {drugbank: "DB04817", name:"Metamizole"})
~~~

## Exercício 2

Considerando que a `Dipyrone` e `Metamizole` são o mesmo medicamento com nomes diferentes, crie uma aresta com o rótulo `:SameAs` que ligue os dois.

### Resolução
~~~cypher
MATCH (met:Drug {name:"Metamizole"})
MATCH (dip:Drug {name:"Dipyrone"})
CREATE (met)-[:SameAs]->(dip)
~~~

## Exercício 3

Use o `DELETE` para excluir o relacionamento que você criou (apenas ele).

### Resolução
~~~cypher
MATCH (met)-[del:SameAs]->(dip)
DELETE del
~~~

## Exercício 4

Faça a projeção em relação a Patologia, ou seja, conecte patologias que são tratadas pela mesma droga.

### Resolução
~~~cypher
MATCH (pat:Pathology)-[a]->(p:Drug)<-[b]-(pat2:Pathology)
MERGE (pat)<-[r:Relates]->(pat2)
~~~

## Exercício 5

Construa um grafo ligando os medicamentos aos efeitos colaterais (com pesos associados) a partir dos registros das pessoas, ou seja, se uma pessoa usa um medicamento e ela teve um efeito colateral, o medicamento deve ser ligado ao efeito colateral.

### Resolução
~~~cypher

MATCH (d:Drug)
MATCH (s:SideEffect)

CREATE (d)-[h:HasEffect]->(s)
where d.drugbank = s.drugbank

~~~

## Exercício 6

Que tipo de análise interessante pode ser feita com esse grafo?
- todas as ocorrências de efeitos colaterais da dipirona.

Proponha um tipo de análise e escreva uma sentença em Cypher que realize a análise.

### Resolução
~~~cypher
MATCH (d:Drug)
MATCH (s:SideEffect)

MATCH (d)-[h:HasEffect]->(s)
where s.codedrug = 'Dipyrone'
RETURN h
~~~
