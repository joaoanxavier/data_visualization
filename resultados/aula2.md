Aula 2 - Prática dos Slides
================
João Xavier
02/03/2021

-   Pacotes usados

``` r
library(tidyverse)
library(ggplot2)
```

-   Gerando a base de dados
    -   Além do que o autor fez adicionei uma coluna com as temperaturas
        em graus Celsius

``` r
link <- "https://wilkelab.org/SDS375/datasets/tempnormals.csv"
temperatures <- read_csv(link) %>% 
    mutate(
        location = factor(
            location, levels = c("Death Valley", "Chicago", "Houston", "San Diego")
        ),
        temperature_celsius = (temperature - 32) * 5/9 
    )
```

1.  **Gráfico de linha simples**

``` r
temperatures %>% 
    ggplot(
        aes(day_of_year, temperature_celsius,
            color = location)
        ) +
    geom_line()
```

![](aula2_files/figure-gfm/Gráfico%201-1.png)<!-- -->

1.  **Gráfico de cor**

``` r
temperatures %>% 
    ggplot(
        aes(day_of_year, location,
            color = temperature)
        ) +
    geom_point(size = 5)
```

![](aula2_files/figure-gfm/Gráfico%202-1.png)<!-- -->

1.  **Boxplot**

``` r
temperatures %>% 
    ggplot(
        aes(month, temperature,
            color = location)
        ) +
    geom_boxplot()
```

![](aula2_files/figure-gfm/Gráfico%203-1.png)<!-- -->

1.  **Violim**

-   Usando facet\_wrap para criar 4 gŕaficos separados
    -   Não se esquecer usar vars() na função facet\_wrap

``` r
temperatures %>% 
    ggplot(aes(month, temperature,
               fill = location)) +
    geom_violin() +
    facet_wrap(vars(location))
```

![](aula2_files/figure-gfm/Gráfico%204-1.png)<!-- -->

-   **Comentário geral**: notar a diferença entre os argumento fill e
    color em aes()
    -   Fill colore todo o interior do geom, enquanto color apenas a
        parte externa
    -   Alguns tipos de geom suportam ambos os argumentos
