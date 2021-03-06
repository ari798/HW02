HW02\_B\_Graph-Mimic
================
Ariana Tortolani

``` r
library("ggplot2")
library("magrittr") #so I can do some piping
data("diamonds")
data("mpg")
data("iris")
theme_set(theme_bw()) #I'll give you this one, you can set the theme individually for graphs
#or you can set the theme for all the graphs using theme_set()
#theme_bw() is best theme (IMO)

#for graph 3:
library("ggrepel")
```

## HW02 Part B

For this part of the HW, the goal is to try to recreate the graphs I
make from scratch. I will only provide the MD, not the actual code I
used to create it besides which data I use to create it. The rest will
be up to you.

Try for all 4, but if you are struggling don’t worry about it. Try your
best for each, if you don’t get everything that’s what the peer-review
is for. :smile:

### Graph 1

``` r
data("diamonds")
#hint think about the *position* the bars are in...
```

Using the diamonds dataset, make this graph:
![](HW02_B_Mimic_files/figure-gfm/unnamed-chunk-2-1.png)<!-- -->

``` r 
ggplot(diamonds, aes(cut, fill = clarity)) +
  geom_bar(position = position_dodge()) +
  labs(title = "My Diamond Collection", 
       subtitle = "Boxplot representing the number of diamonds in my diamond collection by \ntype of cut quality and clarity of diamond") +
  theme(plot.title = element_text(size = 14, face = "bold", hjust = 0.5)) +
  labs (x = "Diamond Cut", y = "Number of Diamonds") +
  annotate(geom = "text", x = 4, y = 4500, label = "My Best Diamonds,\nof course") +
  annotate("rect", xmin = 4.5, xmax = 5.5, ymin = 0, ymax = 5000, alpha = 0.25)

```

My Graph:
![MY GRAPH](HW02_B_Mimic_starter_files/figure-gfm/graph1 code-1.png)<!-- -->

### Graph 2

``` r
data("iris")
```

Using the iris dataset, make this graph:

    ## `geom_smooth()` using formula 'y ~ x'

![](HW02_B_Mimic_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->

```r 

iris$NewOrder <- factor(iris$Species, levels = c("versicolor","setosa","virginica"))

ggplot(iris, aes(Sepal.Length, Petal.Length, color = Species, shape = Species)) +
  geom_point() +
  geom_smooth(method = lm, se = FALSE, color = "black") +
  facet_wrap(vars(NewOrder), scales = "free_y") 

```

My Graph:
![MY GRAPH](HW02_B_Mimic_starter_files/figure-gfm/graph 2 code-1.png)<!-- -->

### Graph 3

You’ll need the information in this first box to create the graph

``` r
data("mpg")
corvette <- mpg[mpg$model == "corvette",]
#install
require("ggrepel") #useful for making text annotations better, hint hint
set.seed(42)
```

Now using the mpg dataset and the corvette dataset, make this graph:

![](HW02_B_Mimic_files/figure-gfm/unnamed-chunk-6-1.png)<!-- -->

```r

ggplot(mpg, aes(displ,hwy)) +
  geom_point() + 
  geom_point(data = corvette, color = "blue") +
  geom_text_repel(data = corvette, aes(label = paste("Corvette,",year))) +
  scale_x_continuous(limits = c(1,8), breaks = seq(1,8,1)) +
  labs(title = "Corvettes are a bit of an outlier") 
  

```

My Graph:
![MY GRAPH](HW02_B_Mimic_starter_files/figure-gfm/graoh 3 code-1.png)<!-- -->


There is a trick to getting the model and year to print off together.
`paste()` is a useful function for this, also pasting together parts of
file names and parts of urls together.

### Graph 4

``` r
data(mpg)

#hint for the coloring, colorbrewer and you can set palette colors and make your graphs colorblind friendly
library(RColorBrewer)
display.brewer.all(colorblindFriendly = T) #take a look at the colorblindfriendly options
```

![](HW02_B_Mimic_files/figure-gfm/unnamed-chunk-7-1.png)<!-- -->

The above graph lets you see some colobrlind friendly palettes. For the
graph below, I used Set2.

Now using the above mpg dataset, make this graph

![](HW02_B_Mimic_files/figure-gfm/unnamed-chunk-8-1.png)<!-- -->


```r

ggplot(mpg, aes(cty, class)) +
  geom_jitter(aes(fill = class, color = class)) + #i dont think my points here are accurate (aka like the example figure) but i am not sure how else to get them
  scale_color_brewer(palette="Set2") +
  geom_boxplot(fill = NA, outlier.shape = NA) +
  labs(title = "Horizontal BoxPlot of City MPG and Car Class",
       x = "Car Class",
       y = "City mpg") +
  scale_x_continuous(breaks = seq(10,35,5))

```

My Graph:
![MY GRAPH](HW02_B_Mimic_starter_files/figure-gfm/graph 4 code-1.png)<!-- -->
