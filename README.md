<p align="center">
  <img src="./img/title.svg" width="400px"></img>
  <h5 align="center">Ready-to-use <code>ggplot2</code> theme</h5>
</p>
<br>

This is a `ggplot2` theme I use on my [blog](http://erikjanvankesteren.nl/blog/) and elsewhere. You can use it and adapt it if you want. It's designed to be truly plug-and-play. See [below](#example-plots) for examples.

<p align="center">
  <br/>
  <img src="./img/plot.png" width="70%"></img>
  <br/>
</p>


As with any software project, this has a collection of dependencies it builds on:

- The [trafford data lab theme](https://github.com/traffordDataLab/assets/blob/master/theme/ggplot2/theme_lab.R) was one of the main inspirations.
- It uses Mozilla's [Fira Sans](https://mozilla.github.io/Fira/) font because it is beautiful.
- Fonts in `R` graphics are notoriously difficult. The package [`extrafont`](https://github.com/wch/extrafont) solves this.
- Of course, one of the main dependencies is [`ggplot2`](https://github.com/tidyverse/ggplot2).
- I used [coolors](https://coolors.co/) to generate the colours.


## Installation
```R
devtools::install_github("vankesteren/firatheme")
```

## Example plots
Below you can find some example plots made using `theme_fira()`

### Dots and lines
```R
library(ggplot2)
library(firatheme)

ggplot(mtcars, aes(x = mpg*0.43, y = wt*0.4535924, colour = factor(cyl))) +
       geom_point(size = 2) + geom_smooth(se = FALSE) +
       labs(title = "Car weight vs efficiency",
            x = "Efficiency (km/l)",
            y = "Weight (1000 kg)",
            colour = "Cylinders") +
       theme_fira() +
       scale_colour_fira()

firaSave("plot.png", device = "png")
```
![plt](./img/plot.png)

### Bar graph

```R
library(ggplot2)
library(firatheme)

ggplot(chickwts, aes(x = feed, y = weight)) +
  geom_bar(stat = "identity", width=0.8, fill = firaCols[1]) +
  labs(title = "Chicken weights by feed type",
       y = "Weight (grams)",
       x = "") +
  theme_fira()
```

![chk](./img/chick.png)


### Boxplot

```R
library(ggplot2)
library(firatheme)

ggplot(iris, aes(y = Sepal.Length, x = Species, fill = Species)) +
  geom_boxplot(col = firaCols[4], width = 0.5, size = 1) +
  labs(y = "Sepal Length", title = "Iris data") +
  theme_fira() +
  scale_fill_fira() +
  theme(legend.position = "none")
```

![iris](./img/iris.png)

### More lines
```R
library(ggplot2)
library(firatheme)

ggplot(airquality, aes(y = Ozone, x = 1:nrow(airquality))) +
  geom_line(colour = firaCols[2], size = 0.7) +
  geom_point(colour = firaCols[2], size = 1.7) +
  geom_smooth(colour = firaCols[1], size = 0.7,se = FALSE) +
  labs(title = "Ozone in New York", x = "Days") +
  theme_fira()
```

![oz](./img/ozone.png)


## Colours
The colour palette of `firatheme` is available through `firaCols` and `firaPalette()`. In `ggplot` objects, you should use `scale_fill_fira()` and `scale_colour_fira()` for mapped variables. Optionally, the argument `continuous = TRUE` can be passed.
![col](./img/firacols.png)

Using the palette functions, you can get any number of colours from the palette, for example `firaPalette(n = 25)` --- the last image in the figure below:
![cols](./img/firapalette.png)
