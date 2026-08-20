#Análise Exploratória do Catálogo Netflix

Este projeto é uma análise exploratória do catálogo de filmes e séries da Netflix, feita em planilha (Google Sheets), usando tabelas dinâmicas para responder perguntas sobre o perfil do conteúdo disponibilizado pela plataforma.

Tratamento e correção dos dados

Antes de montar as análises, identifiquei um problema de qualidade nos dados: o dataset original trazia a duração de cada título como um texto único (ex: "90 min" ou "2 Seasons"), misturando número e unidade na mesma célula — o que impedia filtrar ou comparar valores numericamente.

Para resolver isso, separei essa informação em duas colunas novas: duration_number (o valor numérico, ex: 90) e duration_type (a unidade, "min" para filmes ou "Season"/"Seasons" para séries). Essa segunda coluna, aliás, precisou ser reconstruída com uma fórmula própria, porque os valores originais estavam inconsistentes em uma parte relevante da base (filme aparecendo com unidade de temporada, e vice-versa). A fórmula usada foi:

=SE(B2="Movie"; "min"; SE(D2>1; "Seasons"; "Season"))

Ou seja: se o título é um filme, a unidade é sempre "min"; caso contrário (série), verifica o número de temporadas em duration_number para decidir entre singular ("Season") e plural ("Seasons"). Com a separação e essa correção, ficou possível fazer análises numéricas de verdade sobre a duração do conteúdo, em vez de depender de texto solto ou de um valor inconsistente.

Tabelas dinâmicas construídas

1. Distribuição por duração
Analisa a duração de filmes e séries. O resultado mostra uma dispersão nos dados — já que filmes e séries usam unidades de medida diferentes (minutos para filme, temporadas para série), a maior concentração aparece tanto em torno de 1 temporada (para séries) quanto na faixa de 90-94 minutos (para filmes), refletindo os dois padrões de duração mais comuns do catálogo.

2. Total de filmes vs. séries (com gráfico)
Compara a quantidade total de filmes e séries no catálogo. O resultado mostra que os filmes são maioria em relação às séries.

3. Top 10 países que mais produzem conteúdo
Ranking dos 10 países com mais títulos publicados. Uma decisão metodológica importante aqui: o dataset inclui coproduções (títulos creditados a mais de um país ao mesmo tempo, como "Estados Unidos, Alemanha"). Para manter o ranking mais preciso, considerei apenas os títulos com um único país de produção, excluindo as coproduções dessa contagem.

4. Quantidade de títulos por ano
Tabela cruzando ano de lançamento com título, mostrando quantos títulos foram lançados a cada ano. 2018 foi o ano com maior número de lançamentos no catálogo.

5. Quantidade de títulos por ano, segmentado por tipo (filme/série)
Mesma análise anterior, mas agora dividindo entre filmes e séries por ano. Confirma que 2018 segue sendo o ano de pico, puxado principalmente por um número maior de filmes lançados naquele ano.
