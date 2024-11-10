# Palmer Penguins: Análise prática


Nesse singelo trabalho me proponho a realizar uma pequena análise sobre as difenças
morfológicas entre os pinguíns fêmeas e machos das espécies Gentoo, Chistrap e
Adelie. Outra percepção que demosntro nessa análise é a variedade destas espécies
nas ilhas ao redor do arqupélogo de Palmer, localizado na Antártica.


## Introdução


Utilizei O conjunto de dados pinguíns de Palmer que reúne várias informações sobre
dismorfismo sexual, variabilidade ambiental e medidas de tamanhos estruturais entre
os pinguíns machos e fêmeas de três espécies: Adelie, Chistrap e Gentoo.Os dados
foram coletados e compartilhados pela [Dr. Kristen Gorman](https://www.uaf.edu/cfos/people/faculty/detail/kristen-gorman.php) e [Palmer
Station Antarctica LTER](https://pallter.marine.rutgers.edu/).


## Preparando meu ambiente

Nota: Começo Importando o pacote `palmerpenguins` e `tidyverse` que para esse caso,
o conjunto de pacotes `Tidyverse` é mais que necessário para o que preciso para
concluir este trabalho.

```{r}
library(tidyverse)
library(palmerpenguins)
```

## Correlação entre peso corporal e o tamanho da nadadeira entre as espécies


Para evitar quaisquer problemas com valores vazios no dataset, vamos começar removendo-os
e assim prosseguir com nossa análise.


```{r}
new_penguins <- penguins %>%
  drop_na()
head(new_penguins)
```

Agora que removemos todos os valores vazios, vamos prosseguir com nossa análise.


```{r}
ggplot2::ggplot(new_penguins, aes(x = flipper_length_mm, y = body_mass_g)) +
  geom_point(aes(colour = species, shape = species)) +
  geom_smooth(method = "loess") +
  xlab("Tamanho da nadadeira mm") +
  ylab("Massa corpórea g") +
  labs(title = "Relação entre tamanho corporal e tamanho de nadadeira",
       colour = "Espécie", shape = "Espécie")

```


Nesse gráfico conseguimos perceber facilmente a diferença entre as  3 espécies
considerenado peso corporal e o tamanho das nadadeiras. Os Gentoo possuem nadadeiras
maiores e também maior peso corporal.


## Diferença do dismorfismo sexual entre as espécies.


Vamos identificar as diferenças morfológicas entre os sexos entre as espécies.


```{r}
ggplot2::ggplot(new_penguins, aes(x = species, y = body_mass_g)) +
  geom_violin(aes(fill = species)) +
  facet_wrap(~sex) +
  xlab("Espécie") +
  ylab("Massa corporal g") +
  labs(title = "Diferença corpórea de macho e fêmea",
       fill = "Espécie")
```


O que conseguemios ver aqui nessa viz é que os Gentoo são maiores, tanto machos
quanto fêmeas, e as as outras espécies têm tamanhos bem semelhantes. Porém, independente
da espécie, todas as fêmeas são menores que os machos.


```{r}
ggplot2::ggplot(new_penguins, aes(x = bill_length_mm, y = bill_depth_mm)) +
  geom_boxplot(aes(fill = species)) +
  facet_wrap(~sex) +
  xlab("Comprimento do bico mm") +
  ylab("Largura do bico mm") +
  labs(title = "Dismorfismo sexual de largura e comprimento de bico entre macho e fêmea",
       fill = "Espécie")
```


Novamente o que percebemos nesse gráfico é a diferença de machos e fêmeas, independente da espécie;
As fêmeas possuem bicos mais curtos e menos largos em relação aos machos. Agora, é perceptível que
os Chinstrap são os que mais possuem longos bicos e mais largos também , seguidos pelos Gentoo que
apesar de bicos longos, eles não são tão largos. Em contrapartida, os Adelie, exibem largos bicos e
com pouco comprimento.


## Variabilidade no ambiente

Chegamos agora na análise sobre os locais onde encontramos uma certa frequeências
das espécies.


```{r}
ggplot2::ggplot(new_penguins, aes(x = island, fill = species)) +
  geom_bar(position = "fill") +
  xlab("Ilha") +
  ylab("Número de pinguíns") +
  labs(title = "Variedade do ambiente",
       fill = "Espécie")

```


Com relação a frequência das espécies no ambiente do arquipélago de Palmer o que
percebemos? o que conseguimos tirar como conclusão é que as espécies Gentoo e Chistrap
tem uma frequência mais acentuada em ilhas específicas; Na ilha Biscoe é o local
onde localizamos as espécies Gentoo, e os Chistrap na ilha Dream, em contra partida,
os Adelie apresentam uma frequência em todas as três ilhas.


## Conclusão


Com essa análise simples conseguimos responder algumas respostas:

* Existe uma diferença morfológica entre machos e fêmeas independente da espécie:

  Em ambas as espécies: Adelie, gentoo e Chistrap os machos são maiores em peso
  corporal, bicos mais largos e compridos.

* Diferenças quanto a estrutura corporal entre as 3 espécies analisadas:

  Identificamos que a espécie Gentoo são maiores em peso corporal em relação
  aos Chistrap e Adelie.

  Outra percepção é que quanto maior o pinguin, maior é sua nadadeira.

* A frequência e distribuição das espécies nas ilhas Dream, Torgersen e Biscoe.

  As espécies Gentoo e Chistrap são encontrados com mais frequência nas ilhas:
  Biscoe e Dream respectivamente

  Quanto aos pinguíns  Adelie, são observados em todas as três ilhas.

  ![](./assets/linkedin_icon.png)  [Linkedin](https:/www.linkedin.com/in/marianadiniz93)