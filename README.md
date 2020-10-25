# ANALYSIS-OF-DATA-WITH-R
Creating charts, graphs and charts with mtcars, diamond and facebook datasets
---
title: "Diamond datasets"
output:
  pdf_document: default
  html_document: default
  word_document: default
date: ""
theme: cerulean
---


## Name: PROJECT 6

### Analyzing  the diamond, mtcars and fake facebook dataset geneated from extrated from Kaggle and R inbuilt data respectively.

```{r}
diamonds<- read.csv("diamonds.csv", header = TRUE, sep = ",")
## Barplot for the cut and colour. columns in the dataset
barplot(table(diamonds$cut), main = "Barchart for the diamond cuts qualities")
barplot(table(diamonds$color), main = "Barchart for Diamond colors")
```

```{r}
### Pie Chart for both cuts and colors
pie(table(diamonds$cut), main = "Pie Chart for diamond cuts")
pie(table(diamonds$color), main = "Pie Chart for diamond colors")

### Adding percentages to the data.
diammond.table<-table(diamonds$cut)
diamond.percent<- 100*diammond.table/sum(diammond.table)
temp.name<- paste(format(diamond.percent, digits = 3, trim = T), "%", sep = "")
diamond.names<-paste(names(diammond.table), temp.name)
pie(diammond.table, labels = diamond.names)

### Percentages for colors
diammond.table<-table(diamonds$color)
diamond.percent<- 100*diammond.table/sum(diammond.table)
temp.name<- paste(format(diamond.percent, digits = 3, trim = T), "%", sep = "")
diamond.names<-paste(names(diammond.table), temp.name)
pie(diammond.table, labels = diamond.names)
```

```{r}
### Histogram for the some of the numerical variables.
hist(diamonds$carat, nclass = 50, main = "Weight of the Carats")
hist(diamonds$price, nclass = 20, main = "Diamond Prices")
```

```{r}
### Scatter plot for x and z in the diamond dataset
plot(diamonds$x, diamonds$z, xlab = "x", ylab = "z", main = "Scatter plot for x and z" )
```

```{r}
### Boxplot of carat and cut, and of color of the diamonds
boxplot(diamonds$carat~diamonds$cut, xlab = "carat", ylab ="cut" )
boxplot(diamonds$carat~diamonds$color, xlab = "carat", ylab ="color" )
```
```{r}
### Chi Square for cut and color.It doesnt matter about the position. 
chisq.test(table(diamonds$cut,diamonds$color))
chisq.test(table(diamonds$color,diamonds$cut))
```

```{r}
### Pearson correlation the quantitative variables
cor(diamonds$x, diamonds$y, use = "complete.obs")
cor(diamonds$y, diamonds$z, use = "complete.obs")
cor(diamonds$x, diamonds$z, use = "complete.obs")
cor(diamonds$carat, diamonds$z, use = "complete.obs")
cor(diamonds$carat, diamonds$depth, use = "complete.obs")
```

```{r}
### Anova between cut and carat, and with color.
anova(lm(diamonds$carat~diamonds$cut))
anova(lm(diamonds$carat~diamonds$color))
```


### Working with Mtcars dataset.
```{r}
head(mtcars)
### Regression of Miles Per Gallon on Weight of Cars
attach(mtcars)
plot(wt,mpg)
abline(lm(mpg~wt))
title("Regresion of Miles Per Gallon on Weight of Cars")
detach(mtcars)
```

```{r}
### Histogram of the Gross horsepower of the cars.
patr<- hist(mtcars$hp, breaks = 20, col = "blue", main = " Histogram of Car Horsepower", xlab = "Horsepower")
```

```{r}
### Boxplot
boxplot(drat~cyl, data = mtcars, xlab = "Cylinders", ylab = "Frequency", main= "Boxplot of Real axel ratio on Cylinder", col="green")
```

### Working with facebok dataset.
```{r}
facebook<- read.table("pseudo_facebook.txt", header = TRUE, sep = "\t")
summary(facebook)
plot(facebook$age, facebook$friend_count, xlab = "Age", ylab = "friends_count", pch=20, col="blue")

### Limiting the x variable (age) from 15 to 70 and y variable from 200 to 4000.
plot(facebook$age, facebook$friend_count, xlab = "Age", ylab = "friends_count", pch=20, col="blue", xlim =c(15,70), ylim = c(200,4000))

### Reducing over-plotting by adding some jitters to the the age and friends_count variables.
plot(jitter(facebook$age, amount = 0.20), jitter(facebook$friend_count, amount = 0.25), xlab = "Age", ylab = "friends_count", pch=20, col="blue", xlim =c(15,70), ylim = c(200,4000))

### Adding some transparency.
plot(jitter(facebook$age, amount = 0.20), jitter(facebook$friend_count, amount = 0.25), xlab = "Age", ylab = "friends_count", pch=20, col=gray(0.5, alpha = 0.05), xlim =c(15,70), ylim = c(200,4000))

### Transforming the data on a log scale. 
plot(jitter(facebook$age, amount = 0.20), jitter(facebook$friend_count, amount = 0.25), xlab = "Age", ylab = "friends_count", pch=20, col=gray(0.5, alpha = 0.05), xlim =c(15,70), ylim = c(200,4000), log = 'x')
```



