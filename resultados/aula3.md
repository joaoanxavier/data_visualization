Aula 3
================

## Pacotes

``` r
library(tidyverse)
library(ggplot2)
library(knitr)
library(palmerpenguins)
```

## Dados utilizados nos primeiros gráficos

``` r
boxoffice <- tibble(
  rank = 1:5,
  title = c("Star Wars", "Jumanji", "Pitch Perfect 3", "Greatest Showman", "Ferdinand"),
  amount = c(71.57, 36.17, 19.93, 8.81, 7.32) # million USD
)
```

## Primeira exibição (ruim)

``` r
boxoffice %>% 
    ggplot(aes(title, amount)) +
    geom_col()
```

![](aula3_files/figure-gfm/gráfico%201-1.png)<!-- -->

## Segunda exibição (melhor)

``` r
boxoffice %>% 
    ggplot(aes(fct_reorder(title, amount), amount)) +
    geom_col()
```

![](aula3_files/figure-gfm/gráfico%202-1.png)<!-- -->

## Com o eixo invertido

``` r
 boxoffice %>% 
    ggplot(aes(amount, fct_reorder(title, amount))) +
    geom_col() +
    xlab("Arrecadação em milhões de dólares") +
    ylab(NULL)
```

![](aula3_files/figure-gfm/gráfico%203-1.png)<!-- -->

# Pinguins!

## Usando geom\_bar para contar as espécies de pinguins

-   `geom_bar` só pode ter argumento um dos eixos

``` r
penguins %>% 
    ggplot(aes(y = species)) +
    geom_bar()
```

![](aula3_files/figure-gfm/gráfico%204-1.png)<!-- -->

## Reordenando gráficos

-   Existem duas maneiras de fazer isso

-   A primeira manualmente com `fct_relevel`:

``` r
penguins %>% 
    ggplot(aes(y = fct_relevel(species, "Chinstrap", "Gentoo", "Adelie"))) +
    geom_bar() +
    ylab(NULL) #Removendo o eixo y por motivos de visualização
```

![](aula3_files/figure-gfm/gráfico%205-1.png)<!-- -->

-   E com `fct_reorder` como já vimos:

``` r
penguins %>% 
    ggplot(aes(y = fct_reorder(species, species, length)))+
    geom_bar() +
    ylab(NULL)
```

![](aula3_files/figure-gfm/gŕafico%206-1.png)<!-- -->

## Contando os machos e as fêmeas, separando-os por cor

``` r
penguins %>% 
    ggplot(aes(sex, fill = species)) +
    geom_bar()
```

![](aula3_files/figure-gfm/gráfico%206-1.png)<!-- -->

-   Removendo os NA’s usando tidyverse:

``` r
penguins %>% 
    filter(!is.na(sex)) %>% 
    ggplot(aes(sex, fill = species)) +
    geom_bar()
```

![](aula3_files/figure-gfm/gráfico%207-1.png)<!-- -->

## Posicionando as barras de uma maneira diferente

``` r
penguins %>% 
    filter(!is.na(sex)) %>% 
    ggplot(aes(sex, fill = species)) +
    geom_bar(position = "dodge")
```

![](aula3_files/figure-gfm/gráfico%208-1.png)<!-- -->

-   Também é possível usar `position = "stack"` para manter o primeiro
    visual
-   Além disso, com `position = "fill"` o eixo y é mudado para a escala
    de 100%
