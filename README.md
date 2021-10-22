# Usando SQL'S NATIVAS

Ao realizar um requisito tive a necessidade de usar SQL nativa, pois iria se utilizar de UNION, uma das partes mais chatas e na recuperação dos dados, pois a magica do Hibernate quando usado JPQL não acontece. Procurei como foi feito em situações parecidas e no sistema tem varias maneiras, porém a que eu mais gostei irei mostrar abaixo usando imagens.

Primeiramente iremos criar nosso DTO como mostrado na imagem abaixo. <br />
![ItemAtaMenorValorDTO](https://i.ibb.co/KxLkFtn/dto.png)

Agora na sua consulta nativa sera necessário utilizar alias com os mesmos nomes dos atributos do DTO.
![Alias na consulta nativa](https://i.ibb.co/sVQvrHV/alias.png)

No Java para como isso vai estar em uma String você precisa escapar as aspas("SELECT ItemAtas.AI_ID as \\"idItemAta\\", ... ")

Agora basta antes de executar a Query você registrar  a classe que vai fazer essa transformação.
![Metodo SetResultTransformer](https://i.ibb.co/nf6wry6/transform.png)

Com isso vai cria sua instancia já populada com os dados. Por baixo dos panos essa classe utiliza-se de **Java Reflection**,
para mais detalhes basta conferir a [Documentação.](https://docs.jboss.org/hibernate/orm/3.2/api/org/hibernate/transform/AliasToBeanResultTransformer.html)
