Aula 4
================

## Pacotes

``` r
library(ggplot2)
library(tidyverse)
```

## Carregando base de dados do Titanic

``` r
titanic <- read_csv("https://wilkelab.org/SDS375/datasets/titanic.csv") %>%
    as_tibble() %>%
    select(age, sex, class, survived) %>%
    arrange(age, sex, class)
```

## Fazendo histogramas

``` r
titanic %>% 
    ggplot(aes(age)) + 
    geom_histogram()
```

![](aula4_files/figure-gfm/gráfico%201-1.png)<!-- -->

## Mudando a largura das caixas

``` r
titanic %>% 
    ggplot(aes(age)) +
    geom_histogram(binwidth = 5)
```

![](aula4_files/figure-gfm/gráfico%202-1.png)<!-- -->

## Escolhendo o centro das caixas

``` r
titanic %>% 
    ggplot(aes(age)) +
    geom_histogram(
        binwidth = 5,
        center = 2.5
    )
```

![](aula4_files/figure-gfm/gráfico%203-1.png)<!-- -->

## Gráficos de densidade

``` r
titanic %>% 
    ggplot(aes(age)) +
    geom_density(fill = "skyblue")
```

![](aula4_files/figure-gfm/gráfico%204-1.png)<!-- -->

## Alterando a medição da densidade

``` r
titanic %>% 
    ggplot(aes(age)) +
    geom_density(
        fill = "skyblue",
        bw = 0.5, #considerado pequeno
        kernel = "gaussian" #centro padrão
    )
```

![](aula4_files/figure-gfm/gráfico%205-1.png)<!-- -->

## Mudando o formato e aumento a medição

``` r
titanic %>% 
    ggplot(aes(age)) +
    geom_density(
        fill = "skyblue",
        bw = 2, #considerado moderado
        kernel = "rectangular"
    )
```

![](aula4_files/figure-gfm/gráfico%206-1.png)<!-- -->

## Outros tipos de gráfico de densidade

-   É possível mudar o parâmetro `stat` dos `geoms_` para que eles virem
    uma função de densidade

-   O primeiro exemplo é do `geom_area`:

``` r
titanic %>% 
    ggplot(aes(age)) +
    geom_area(
        stat = "density",
        fill = "skyblue"
    )
```

![](aula4_files/figure-gfm/gráfico%207-1.png)<!-- -->

-   O segundo exemplo é do `geom_line`:

``` r
titanic %>% 
    ggplot(aes(age)) + 
    geom_line(
        stat = "density"
    )
```

![](aula4_files/figure-gfm/gráfico%208-1.png)<!-- -->

-   É necessário notar dois pontos importantes:
    -   O primeiro é que é possível alterar o parâmetro `stat` em
        qualquer `geom`
    -   Além disso, o parâmetro `stat` carrega consigo outros parâmetros
        quando utilizado
        -   Seria possível portanto mudar o parâmetro `bw` na função
            `geom_line`, mesmo que esse não seja normalmente usado nessa
            função
