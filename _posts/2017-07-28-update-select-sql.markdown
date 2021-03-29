---
layout: post
title:  "Update Select com SQL"
date:   2017-07-28 15:52:00 -0300
categories: sql
---

Olá pessoal, esse post será mais uma dica.
Alguma tempo atrás na minha vida de consultor, deparei-me com o seguinte cenário:
Rodou um job que alterou um monte de registros em uma tabela, apartir disso começou vários erros no ambiente de QA decorrentes dessas alterações indevidas...enfim, resumindo tinha que dar um jeito de resolver.
Sem mais delongas vamos ao problema/solução.
Essa dica é para quando temos que atualizar algum(ns) registros em uma tabela, porém antes disso temos que fazer uma consulta para descobrir o que teremos que atualizar, ou seja, fazer um UPDATE/SELECT.

{% highlight sql %}
UPDATE TableA SET COLUMN_A = 'NEW_VALUE', COLUMN_B = 'NEW_VALUE'
WHERE (column1, column2) in (SELECT (column1, column2) FROM TableA WHERE column3 = 'VALUE')
{% endhighlight %}

Utilizamos o retorno de um select como claúsula do WHERE.
Com isso resolvemos o problema.

Até a próxima dica.


