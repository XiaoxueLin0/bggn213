Class 7 functions and packages
================
Xiaoxue Lin
1/30/2019

Functions revisited
-------------------

load (i.e. **source**) our rescale() function from last day

``` r
source("http://tinyurl.com/rescale-R")
```

test this function

``` r
rescale(1:5)
```

    ## [1] 0.00 0.25 0.50 0.75 1.00

``` r
#' rescale(c(1:5, "string"))
```

We want to make this function more robust to these "string"" types of errors two functions to use, warning() and stop()

``` r
#rescale2(c(1:5, "string"))
```

``` r
is.numeric(1:5)
```

    ## [1] TRUE

``` r
is.numeric("string")
```

    ## [1] FALSE

``` r
is.numeric(c(1:5, "string"))
```

    ## [1] FALSE

``` r
!is.numeric(1:5)
```

    ## [1] FALSE

``` r
x <- c( 1, 2, NA, 3, NA)
y<-c(NA,3,NA,3, 4)
```

``` r
is.na(x)
```

    ## [1] FALSE FALSE  TRUE FALSE  TRUE

``` r
is.na(y)
```

    ## [1]  TRUE FALSE  TRUE FALSE FALSE

``` r
sum(is.na (x) & is.na (y)) #this is a snippet
```

    ## [1] 1

``` r
# which(is.na(x) & is.na(y)) indicates where in the vector is the true element
```

Now take our working snippet and make first function

``` r
both_na <- function (x,y) {
  # Check for NA elements in both input vectors
  sum(is.na (x) & is.na (y))
}
```

``` r
x <- c( NA, NA, NA)
y1 <- c( 1, NA, NA)
y2 <- c( 1, NA, NA, NA)
y3 <- c( 1, NA, NA, NA, NA)
```

``` r
# What will this return?
both_na(x,y2)
```

    ## Warning in is.na(x) & is.na(y): longer object length is not a multiple of
    ## shorter object length

    ## [1] 3

When comparing x with y2, the last NA with y2 has no paring, so the first element of x is added on to the end of x to pair with y2.

``` r
both_na <- function (x, y) {
  if(length(x) != length(y)) {
stop("Input x and y should be vectors of the same length")
# be easily missed especially in scripts.
}
  na.in.both <- ( is.na(x) & is.na(y) )
  na.number  <- sum(na.in.both)
  na.which   <- which(na.in.both)
  message("Found ", na.number, " NA's at position(s):",
          paste(na.which, collapse=", ") )
  return( list(number=na.number, which=na.which) )
}
```

``` r
library("bio3d")
data <- system.file("examples/ediaspora.gexf.xml", package = "bio3d")
#sigma(data)
```

``` r
#install.packages("ggplot2")
```

``` r
#install.packages("plotly")
```

``` r
library(ggplot2)
library(plotly)
```

    ## 
    ## Attaching package: 'plotly'

    ## The following object is masked from 'package:ggplot2':
    ## 
    ##     last_plot

    ## The following object is masked from 'package:stats':
    ## 
    ##     filter

    ## The following object is masked from 'package:graphics':
    ## 
    ##     layout

``` r
p <- ggplot(data = diamonds, aes(x = cut, fill = clarity)) +
            geom_bar(position = "dodge")
ggplotly(p)
```

<!--html_preserve-->

<script type="application/json" data-for="htmlwidget-bd740c13c6104a608fdf">{"x":{"data":[{"orientation":"v","width":[0.1125,0.1125,0.1125,0.1125,0.112500000000001],"base":[0,0,0,0,0],"x":[0.60625,1.60625,2.60625,3.60625,4.60625],"y":[210,96,84,205,146],"text":["count:  210<br />cut: Fair<br />clarity: I1","count:   96<br />cut: Good<br />clarity: I1","count:   84<br />cut: Very Good<br />clarity: I1","count:  205<br />cut: Premium<br />clarity: I1","count:  146<br />cut: Ideal<br />clarity: I1"],"type":"bar","marker":{"autocolorscale":false,"color":"rgba(68,1,84,1)","line":{"width":1.88976377952756,"color":"transparent"}},"name":"I1","legendgroup":"I1","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":[0.1125,0.1125,0.1125,0.1125,0.112500000000001],"base":[0,0,0,0,0],"x":[0.71875,1.71875,2.71875,3.71875,4.71875],"y":[466,1081,2100,2949,2598],"text":["count:  466<br />cut: Fair<br />clarity: SI2","count: 1081<br />cut: Good<br />clarity: SI2","count: 2100<br />cut: Very Good<br />clarity: SI2","count: 2949<br />cut: Premium<br />clarity: SI2","count: 2598<br />cut: Ideal<br />clarity: SI2"],"type":"bar","marker":{"autocolorscale":false,"color":"rgba(70,51,126,1)","line":{"width":1.88976377952756,"color":"transparent"}},"name":"SI2","legendgroup":"SI2","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":[0.1125,0.1125,0.1125,0.1125,0.112500000000001],"base":[0,0,0,0,0],"x":[0.83125,1.83125,2.83125,3.83125,4.83125],"y":[408,1560,3240,3575,4282],"text":["count:  408<br />cut: Fair<br />clarity: SI1","count: 1560<br />cut: Good<br />clarity: SI1","count: 3240<br />cut: Very Good<br />clarity: SI1","count: 3575<br />cut: Premium<br />clarity: SI1","count: 4282<br />cut: Ideal<br />clarity: SI1"],"type":"bar","marker":{"autocolorscale":false,"color":"rgba(54,92,141,1)","line":{"width":1.88976377952756,"color":"transparent"}},"name":"SI1","legendgroup":"SI1","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":[0.1125,0.1125,0.1125,0.1125,0.112500000000001],"base":[0,0,0,0,0],"x":[0.94375,1.94375,2.94375,3.94375,4.94375],"y":[261,978,2591,3357,5071],"text":["count:  261<br />cut: Fair<br />clarity: VS2","count:  978<br />cut: Good<br />clarity: VS2","count: 2591<br />cut: Very Good<br />clarity: VS2","count: 3357<br />cut: Premium<br />clarity: VS2","count: 5071<br />cut: Ideal<br />clarity: VS2"],"type":"bar","marker":{"autocolorscale":false,"color":"rgba(39,127,142,1)","line":{"width":1.88976377952756,"color":"transparent"}},"name":"VS2","legendgroup":"VS2","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":[0.1125,0.1125,0.1125,0.112500000000001,0.112500000000001],"base":[0,0,0,0,0],"x":[1.05625,2.05625,3.05625,4.05625,5.05625],"y":[170,648,1775,1989,3589],"text":["count:  170<br />cut: Fair<br />clarity: VS1","count:  648<br />cut: Good<br />clarity: VS1","count: 1775<br />cut: Very Good<br />clarity: VS1","count: 1989<br />cut: Premium<br />clarity: VS1","count: 3589<br />cut: Ideal<br />clarity: VS1"],"type":"bar","marker":{"autocolorscale":false,"color":"rgba(31,161,135,1)","line":{"width":1.88976377952756,"color":"transparent"}},"name":"VS1","legendgroup":"VS1","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":[0.1125,0.1125,0.1125,0.112500000000001,0.112500000000001],"base":[0,0,0,0,0],"x":[1.16875,2.16875,3.16875,4.16875,5.16875],"y":[69,286,1235,870,2606],"text":["count:   69<br />cut: Fair<br />clarity: VVS2","count:  286<br />cut: Good<br />clarity: VVS2","count: 1235<br />cut: Very Good<br />clarity: VVS2","count:  870<br />cut: Premium<br />clarity: VVS2","count: 2606<br />cut: Ideal<br />clarity: VVS2"],"type":"bar","marker":{"autocolorscale":false,"color":"rgba(74,193,109,1)","line":{"width":1.88976377952756,"color":"transparent"}},"name":"VVS2","legendgroup":"VVS2","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":[0.1125,0.1125,0.1125,0.112500000000001,0.112500000000001],"base":[0,0,0,0,0],"x":[1.28125,2.28125,3.28125,4.28125,5.28125],"y":[17,186,789,616,2047],"text":["count:   17<br />cut: Fair<br />clarity: VVS1","count:  186<br />cut: Good<br />clarity: VVS1","count:  789<br />cut: Very Good<br />clarity: VVS1","count:  616<br />cut: Premium<br />clarity: VVS1","count: 2047<br />cut: Ideal<br />clarity: VVS1"],"type":"bar","marker":{"autocolorscale":false,"color":"rgba(159,218,58,1)","line":{"width":1.88976377952756,"color":"transparent"}},"name":"VVS1","legendgroup":"VVS1","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":[0.1125,0.1125,0.1125,0.112500000000001,0.112500000000001],"base":[0,0,0,0,0],"x":[1.39375,2.39375,3.39375,4.39375,5.39375],"y":[9,71,268,230,1212],"text":["count:    9<br />cut: Fair<br />clarity: IF","count:   71<br />cut: Good<br />clarity: IF","count:  268<br />cut: Very Good<br />clarity: IF","count:  230<br />cut: Premium<br />clarity: IF","count: 1212<br />cut: Ideal<br />clarity: IF"],"type":"bar","marker":{"autocolorscale":false,"color":"rgba(253,231,37,1)","line":{"width":1.88976377952756,"color":"transparent"}},"name":"IF","legendgroup":"IF","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null}],"layout":{"margin":{"t":26.2283105022831,"r":7.30593607305936,"b":40.1826484018265,"l":48.9497716894977},"plot_bgcolor":"rgba(235,235,235,1)","paper_bgcolor":"rgba(255,255,255,1)","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187},"xaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[0.4,5.6],"tickmode":"array","ticktext":["Fair","Good","Very Good","Premium","Ideal"],"tickvals":[1,2,3,4,5],"categoryorder":"array","categoryarray":["Fair","Good","Very Good","Premium","Ideal"],"nticks":null,"ticks":"outside","tickcolor":"rgba(51,51,51,1)","ticklen":3.65296803652968,"tickwidth":0.66417600664176,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(255,255,255,1)","gridwidth":0.66417600664176,"zeroline":false,"anchor":"y","title":"cut","titlefont":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187},"hoverformat":".2f"},"yaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[-253.55,5324.55],"tickmode":"array","ticktext":["0","1000","2000","3000","4000","5000"],"tickvals":[0,1000,2000,3000,4000,5000],"categoryorder":"array","categoryarray":["0","1000","2000","3000","4000","5000"],"nticks":null,"ticks":"outside","tickcolor":"rgba(51,51,51,1)","ticklen":3.65296803652968,"tickwidth":0.66417600664176,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(255,255,255,1)","gridwidth":0.66417600664176,"zeroline":false,"anchor":"x","title":"count","titlefont":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187},"hoverformat":".2f"},"shapes":[{"type":"rect","fillcolor":null,"line":{"color":null,"width":0,"linetype":[]},"yref":"paper","xref":"paper","x0":0,"x1":1,"y0":0,"y1":1}],"showlegend":true,"legend":{"bgcolor":"rgba(255,255,255,1)","bordercolor":"transparent","borderwidth":1.88976377952756,"font":{"color":"rgba(0,0,0,1)","family":"","size":11.689497716895},"y":0.913385826771654},"annotations":[{"text":"clarity","x":1.02,"y":1,"showarrow":false,"ax":0,"ay":0,"font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187},"xref":"paper","yref":"paper","textangle":-0,"xanchor":"left","yanchor":"bottom","legendTitle":true}],"hovermode":"closest","barmode":"relative"},"config":{"doubleClick":"reset","modeBarButtonsToAdd":[{"name":"Collaborate","icon":{"width":1000,"ascent":500,"descent":-50,"path":"M487 375c7-10 9-23 5-36l-79-259c-3-12-11-23-22-31-11-8-22-12-35-12l-263 0c-15 0-29 5-43 15-13 10-23 23-28 37-5 13-5 25-1 37 0 0 0 3 1 7 1 5 1 8 1 11 0 2 0 4-1 6 0 3-1 5-1 6 1 2 2 4 3 6 1 2 2 4 4 6 2 3 4 5 5 7 5 7 9 16 13 26 4 10 7 19 9 26 0 2 0 5 0 9-1 4-1 6 0 8 0 2 2 5 4 8 3 3 5 5 5 7 4 6 8 15 12 26 4 11 7 19 7 26 1 1 0 4 0 9-1 4-1 7 0 8 1 2 3 5 6 8 4 4 6 6 6 7 4 5 8 13 13 24 4 11 7 20 7 28 1 1 0 4 0 7-1 3-1 6-1 7 0 2 1 4 3 6 1 1 3 4 5 6 2 3 3 5 5 6 1 2 3 5 4 9 2 3 3 7 5 10 1 3 2 6 4 10 2 4 4 7 6 9 2 3 4 5 7 7 3 2 7 3 11 3 3 0 8 0 13-1l0-1c7 2 12 2 14 2l218 0c14 0 25-5 32-16 8-10 10-23 6-37l-79-259c-7-22-13-37-20-43-7-7-19-10-37-10l-248 0c-5 0-9-2-11-5-2-3-2-7 0-12 4-13 18-20 41-20l264 0c5 0 10 2 16 5 5 3 8 6 10 11l85 282c2 5 2 10 2 17 7-3 13-7 17-13z m-304 0c-1-3-1-5 0-7 1-1 3-2 6-2l174 0c2 0 4 1 7 2 2 2 4 4 5 7l6 18c0 3 0 5-1 7-1 1-3 2-6 2l-173 0c-3 0-5-1-8-2-2-2-4-4-4-7z m-24-73c-1-3-1-5 0-7 2-2 3-2 6-2l174 0c2 0 5 0 7 2 3 2 4 4 5 7l6 18c1 2 0 5-1 6-1 2-3 3-5 3l-174 0c-3 0-5-1-7-3-3-1-4-4-5-6z"},"click":"function(gd) { \n        // is this being viewed in RStudio?\n        if (location.search == '?viewer_pane=1') {\n          alert('To learn about plotly for collaboration, visit:\\n https://cpsievert.github.io/plotly_book/plot-ly-for-collaboration.html');\n        } else {\n          window.open('https://cpsievert.github.io/plotly_book/plot-ly-for-collaboration.html', '_blank');\n        }\n      }"}],"cloud":false},"source":"A","attrs":{"7abe5c30d93b":{"x":{},"fill":{},"type":"bar"}},"cur_data":"7abe5c30d93b","visdat":{"7abe5c30d93b":["function (y) ","x"]},"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.2,"selected":{"opacity":1},"debounce":0},"base_url":"https://plot.ly"},"evals":["config.modeBarButtonsToAdd.0.click"],"jsHooks":[]}</script>
<!--/html_preserve-->
