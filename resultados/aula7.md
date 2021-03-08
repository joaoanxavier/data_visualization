Aula 7
================

# Pacotes

``` r
library(tidyverse)
library(ggplot2)
library(colorspace)
library(gapminder)
```

# Carregando base de dados

``` r
temperatures <- read_csv("https://wilkelab.org/SDS375/datasets/tempnormals.csv") %>%
  mutate(
    location = factor(
      location, levels = c("Death Valley", "Houston", "San Diego", "Chicago")
    )
  ) %>%
  select(location, day_of_year, month, temperature)

temps_months <- read_csv("https://wilkelab.org/SDS375/datasets/tempnormals.csv") %>%
  group_by(location, month_name) %>%
  summarize(mean = mean(temperature)) %>%
  mutate(
    month = factor(
      month_name,
      levels = c("Jan", "Feb", "Mar", "Apr", "May", "Jun", "Jul", "Aug", "Sep", "Oct", "Nov", "Dec")
    ),
    location = factor(
      location, levels = c("Death Valley", "Houston", "San Diego", "Chicago")
    )
  ) %>%
  select(-month_name)
```

# Aprendendo sobre cores em gráficos

## Usando paleta de cores padrão

``` r
temps_months %>% 
    ggplot(aes(month, location, fill = mean)) +
    geom_tile(width = 0.95, height = 0.95) +
    coord_fixed(expand = FALSE) +
    theme_classic() +
    scale_fill_gradient() #Paleta de cores padrão
```

![](aula7_files/figure-gfm/padrão-1.png)<!-- -->

## `viridis_c`

``` r
temps_months %>% 
    ggplot(aes(month, location, fill = mean)) +
    geom_tile(width = 0.95, height = 0.95) +
    coord_fixed(expand = FALSE) +
    theme_classic() +
    scale_fill_viridis_c() #Paleta de cores padrão
```

![](aula7_files/figure-gfm/viridis_c-1.png)<!-- -->

### Definindo o parâmetro `option`

``` r
temps_months %>% 
    ggplot(aes(month, location, fill = mean)) +
    geom_tile(width = 0.95, height = 0.95) +
    coord_fixed(expand = FALSE) +
    theme_classic() +
    scale_fill_viridis_c(option = "B", begin = 0.15) #Paleta de cores padrão
```

![](aula7_files/figure-gfm/option%20b-1.png)<!-- -->

## Paleta YlGnBu

``` r
temps_months %>% 
    ggplot(aes(month, location, fill = mean)) +
    geom_tile(width = 0.95, height = 0.95) +
    coord_fixed(expand = FALSE) +
    theme_classic() +
    scale_fill_distiller(palette = "YlGnBu")
```

![](aula7_files/figure-gfm/YlGnBu-1.png)<!-- -->

# Pacote colorspace

Pacote usado para facilitar a organização da bagunça que é a sintaxe do
ggplot

A ideia do pacote é usar a seguinte sintaxe
**scale\_<aesthetic>*<datatype>*<colorscale>()**

## YlGnBu

``` r
temps_months %>% 
    ggplot(aes(month, location, fill = mean)) +
    geom_tile(width = 0.95, height = 0.95) +
    coord_fixed(expand = FALSE) +
    theme_classic() +
    scale_fill_continuous_sequential(palette = "YlGnBu", rev = FALSE)
```

![](aula7_files/figure-gfm/colorspace%20YlGnBu-1.png)<!-- -->

## Viridis

``` r
temps_months %>% 
    ggplot(aes(month, location, fill = mean)) +
    geom_tile(width = 0.95, height = 0.95) +
    coord_fixed(expand = FALSE) +
    theme_classic() +
    scale_fill_continuous_sequential(palette = "Viridis", rev = FALSE)
```

![](aula7_files/figure-gfm/colorspace%20Virids-1.png)<!-- -->

## Inferno

``` r
temps_months %>% 
    ggplot(aes(month, location, fill = mean)) +
    geom_tile(width = 0.95, height = 0.95) +
    coord_fixed(expand = FALSE) +
    theme_classic() +
    scale_fill_continuous_sequential(palette = "Inferno", begin = 0.15, rev = FALSE)
```

![](aula7_files/figure-gfm/colorspace%20Inferno-1.png)<!-- -->

# Paletas de cores qualitativas manualmente

## Padrão

O padrão no caso é `scale_color_hue()`

Infelizmente o autor não disponibilizou os dados para que eu pudesse
reproduzir os resultados, mas o principal da aula em relação a cores
está presente nos gráficos feitos com os dados de temperatura
