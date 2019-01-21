---
title: "Seminar2b_Ninadh"
author: "Ninadh"
date: "1/18/2019"
output: html_document
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```

```{r}
library(ggplot2)
library(tidyverse)
library(dplyr)
library(tibble)
```

Part 1

looking at mpg data frame

```{r}
ggplot2::mpg
```

point graph to create a graph with displ on the x-axis and hwy on the y-axis:

```{r}
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy)) +
	geom_line(aes(x=displ, y=hwy))
```

the plot wiht the line displays a negative corelation of displ with hwy.

```{r} 
# to have the car class in different colors
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy, color = class))
```

```{r}
# the class in differnet size
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy, size = class))
```

Part2 : layering

```{r}
#better still, i can layer it up
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy, color = class)) +
	geom_smooth(aes(displ, hwy))
```

```{r}
# just wanted to have fun with the color gradient in year
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy, color = year)) +
	geom_smooth(aes(displ, hwy))

```

grouping the cars by class

```{r}
mpg %>%
	group_by(class) %>%
	summarise (fuel_effeciency = mean (hwy))
```

it worked, lets now assign it

```{r}
avr_eff <-(mpg %>%
	group_by(class) %>%
	summarise (fuel_effeciency = mean (hwy)))
```


```{r}
ggplot(avr_eff) +
	geom_bar(aes(class, fuel_effeciency), stat = "identity")
```

making it more beautiful
```{r}
ggplot(avr_eff) +
	geom_bar(aes(class, fuel_effeciency, fill = class), stat = "identity") +
	xlab("Vehicle type") +
	ylab("Fuel effeciency (miles/gallon)")
```

```{r}
#to reverse the y-axis
ggplot(avr_eff) +
	geom_bar(aes(class, fuel_effeciency, fill = class), stat = "identity") +
	xlab("Vehicle type") +
	ylab("Fuel effeciency (miles/gallon)") +
	scale_y_reverse()
```

```{r}
#to flip the x,y-axis
ggplot(avr_eff) +
	geom_bar(aes(class, fuel_effeciency, fill = class), stat = "identity") +
	xlab("Vehicle type") +
	ylab("Fuel effeciency (miles/gallon)") +
	coord_flip()
```


```{r}
# I particularly like this one
ggplot(avr_eff) +
	geom_bar(aes(class, fuel_effeciency, fill = class), stat = "identity") +
	xlab("Vehicle type") +
	ylab("Fuel effeciency (miles/gallon)") +
	coord_polar()
```

lets facet the graph

```{r}
ggplot(data = mpg, 
       mapping = aes(x = displ, y = hwy)) +
  geom_point() +
	xlab("Vehicle type") +
	ylab("Fuel effeciency (miles/gallon)") +
  facet_wrap(~class)
```

Part 3: Deliverables

```{r}
# tadaaa
ggplot(mpg) +
	geom_point(aes(displ, hwy, color = class, size = class))
```



