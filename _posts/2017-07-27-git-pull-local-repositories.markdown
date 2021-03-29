---
layout: post
title:  "Pull nos projetos git de um repositório local"
date:   2017-07-27 14:27:43 -0300
categories: linux git
---

Olá Pessoal, esse é meu primeiro post aqui no blog e para testar resolvi escrever sobre algo simples.
Esses dias precisei fazer clone de vários projetos git aqui no trabalho e toda hora que testava algum projeto esquecia de fazer pull, ou fazia em um e não fazia em outro, já deu para imaginar. Então criei um pequeno script maroto para atualizar tudo de uma vez.

{% highlight shell %}
#!/bin/sh
for d in ./*/ ;
do
 (cd "$d" && git pull);
done
{% endhighlight %}

O script entra em todos diretórios e vai atualizando.
Isso é tudo, see you next!


