# Biostatistics For Public Health Final Project

Here's the R markdown for analyzing the dataset that represents the relationship between smoking mothers and babies health conditions.

---


```{r}
library(tidyverse) 
```

Download the Babies dataset (Babies.rda) from the following link https://goo.gl/7NrADr
```{r}
load("Babies.rda")
```
Let’s take a glimpse of the dataset
```{r}
glimpse(Babies)
```

The first a few rows of the dataset
```{r}
head(Babies)
```

**Mom’s smoking and baby’s weight** 
```{r}
 ggplot(Babies) +
  geom_boxplot(aes(x = smoke, y = weight))
```

![Fig1](https://github.com/user-attachments/assets/86e3c0c1-9076-455e-953a-450bdc437b10)


**Mom’s smoking and baby’s weight with reordered x-axis**
```{r}
 ggplot(Babies) +
  geom_boxplot(aes(x = reorder(smoke, weight, FUN = median), y = weight))
```

![Fig2](https://github.com/user-attachments/assets/661e3fda-9bdc-4235-beee-10a6587ca384)


**Mom’s race and baby’s weight**

```{r}
 ggplot(Babies) +
  geom_boxplot(aes(x = reorder(mom.race, weight, FUN = median), y = weight))
```

**Dad’s race and baby’s weight**

```{r}
 ggplot(Babies) +
  geom_boxplot(aes(x = reorder(dad.race, weight, FUN = median), y = weight))
```

The box length gives an indication of the sample variability and the line across the box shows where the sample is centred. The position of the box in its whiskers and the position of the line in the box also tells us whether the sample is symmetric or skewed, either to the right or left.

**Mom’s race and baby’s weight and dad’s race**
```{r}
ggplot(Babies) +
  geom_boxplot(aes(x = reorder(mom.race, weight, FUN = median), y = weight)) +
  geom_jitter(aes(x = reorder(mom.race, weight, FUN = median), y = weight, color = dad.race), alpha = 0.5)
```

**Mom’s height and moms’s weight**
```{r}
ggplot(Babies) +
  geom_point(aes(x = mom.height, y = mom.weight, color = mom.race), alpha = 0.5) +
  geom_smooth(aes(x = mom.height, y = mom.weight), method = "lm")

```

```{r}
model = lm (data = Babies, formula = mom.weight ~ mom.height)
summary(model)
```

**Dad’s height and dad’s weight**
```{r}
ggplot(Babies) +
  geom_point(aes(x = dad.height, y = dad.weight, color = mom.race), alpha = 0.5) +
  geom_smooth(aes(x = dad.height, y = dad.weight), method = "lm")
```

```{r}
model = lm (data = Babies, formula = dad.weight ~ dad.height)
summary(model)
```

**Mom’s weight and dad’s weight**
```{r}
ggplot(Babies) +
  geom_point(aes(x = mom.weight, y = dad.weight, color = mom.race, shape = dad.race), alpha = 0.5)
```

```{r}
model = lm (data = Babies, formula = dad.weight ~ mom.weight)
summary(model)
```

**Mom’s smoking and mom’s education**
```{r}
 ggplot(Babies) +
  geom_bar(aes(x = smoke, fill = mom.edu), position = "fill")
```

**Mom’s smoking and the family’s income**
```{r}
ggplot(Babies) +
  geom_bar(aes(x = smoke, fill = income), position = "fill")
```

**Mom’s race and mom’s weight**
```{r}
ggplot(Babies %>% na.omit()) +
  geom_boxplot(aes(x = reorder(mom.race, mom.weight, FUN = median), y = mom.weight))
```

**Dad’s race and dad’s weight**
```{r}
ggplot(Babies %>% na.omit()) +
  geom_boxplot(aes(x = reorder(dad.race, dad.weight, FUN = median), y = dad.weight))
```
