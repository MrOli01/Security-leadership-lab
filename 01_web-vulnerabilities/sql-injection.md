# O que é Injeção de SQL (SQLi)

Injeção de SQL é uma vulnerabilidade de segurança na web, que permite que um invasor interfira nas consultas que um aplicativo realiza ao seu banco de dados. Isso pode permitir que um invasor visualize dados que normalmente não consegue recuperar. Isso pode incluir dados pertencentes a outros usuários ou quaisquer outros dados que o aplicativo possa acessar.

Em muitos casos, um invasor pode modificar ou excluir esses dados, causando alterações persistentes no conteúdo ou no comportamento do aplicativo. Existem situações que um invasor pode escalar um ataque de injeção de SQL para comprometer o servidor subjacente ou outra infraestrutura de back-end. Isso também pode permitir ataques de negação de serviço.

---

# Qual seria o impacto de um ataque de SQLi bem-sucedido?

Um ataque de injeção de SQL bem-sucedido pode resultar em acesso não autorizado a dados confidenciais, como:

- Senhas.
- Detalhes do cartão de crédito.
- Informações pessoais do usuário.

Ataques de injeção de SQL têm sido utilizados em muitas violações de dados de alto perfil ao longo dos anos. Isso tem causado danos à reputação e multas regulatórias. Em alguns casos, um invasor pode obter uma backdoor persistente nos sistemas de uma organização, levando a um comprometimento de longo prazo que pode passar despercebido por um longo período.

---

# Como detectar vulnerabilidades de Injeção de SQLi?

Você pode detectar injeção de SQL manualmente usando um conjunto sistemático de testes em cada ponto de entrada do aplicativo. Para isso, você normalmente enviaria:

- O caractere de aspas simples `'` e procuraria por erros ou outras anomalias.
- Alguma sintaxe específica de SQL que avalia o valor base (original) do ponto de entrada e um valor diferente, e procura diferenças sistemáticas nas respostas do aplicativo.
- Condições booleanas como `OR 1=1` e `OR 1=2`, e procure diferenças nas respostas do aplicativo.
- Cargas úteis projetadas para disparar atrasos de tempo quando executadas em uma consulta SQL e procurar diferenças no tempo de resposta.
- Cargas úteis OAST projetadas para acionar uma interação de rede fora de banda quando executadas dentro de uma consulta SQL e monitorar quaisquer interações resultantes.

Como alternativa, você pode encontrar a maioria das vulnerabilidades de injeção de SQL de forma rápida e confiável usando o Burp Scanner.

---

# Como evitar injeção de SQL

Você pode evitar a maioria das instâncias de injeção de SQL usando consultas parametrizadas em vez de concatenação de strings dentro da consulta. Essas consultas parametrizadas também são conhecidas como "instruções preparadas".

O código a seguir é vulnerável à injeção de SQL porque a entrada do usuário é concatenada diretamente na consulta:

```java
String query = "SELECT * FROM products WHERE category = '"+ input + "'";
Statement statement = connection.createStatement();
ResultSet resultSet = statement.executeQuery(query);
