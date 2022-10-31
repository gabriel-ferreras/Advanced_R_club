---
title: "Chapter_3_GFG"
output: 
  html_document: 
    keep_md: yes
date: "2022-10-30"
---

## QUIZ

1.  The classical are character, double, integers and logical. The rare types are complex and raw.

2.  Information associated with a vector in pairs of name-value like names or class. You can see them using attributes() and set them individually using attr()

3.  In a list and data frames the elements can be of different types, unlike in matrices and atomic vectors.

4.  Both yes.

5.  Tibbles are an improved lazier version of data frames. They do not use row names, enhanced print, they do not coerce when being created strings to factors, and provide stricter subsetting methods.

## EXERCISES

# Atomic vectors

1.  


```r
?raw
?complex
```

Complex vectors can be created with complex. The vector can be specified either by giving its length, its real and imaginary parts, or modulus and argument. (Giving just the length generates a vector of complex zeroes.)

To create a raw vector you can either use raw(length = x) indicating the length of the vector desired, or use as.raw(x) to coerce into raw.

-   raw creates a raw vector of the specified length. Each element of the vector is equal to 0. Raw vectors are used to store fixed-length sequences of bytes.

-   as.raw attempts to coerce its argument to be of raw type. The (elementwise) answer will be 0 unless the coercion succeeds (or if the original value successfully coerces to 0).

2.  

c(1, FALSE) will create a (1,0) double vector. c("a", 1) will create a ("a", "1") character vector. c(TRUE, 1L) will create a (1L, 1L) integer vector.


```r
c(1, FALSE)
```

```
## [1] 1 0
```

```r
c("a", 1)
```

```
## [1] "a" "1"
```

```r
c(TRUE, 1L)
```

```
## [1] 1 1
```

3.  

1 == "1" is TRUE because 1 is coerced into "1". -1 \< FALSE is TRUE because FALSE is coerced into 0. "one" \< 2 because 2 is coerced into "2" which cannot be compared against "one".


```r
1 == "1"
```

```
## [1] TRUE
```

```r
-1 < FALSE
```

```
## [1] TRUE
```

```r
"one" < 2
```

```
## [1] FALSE
```

4.  

NA must be a logical so it does not coerce a logical vector into another type of vector as the logical is the lowest priority in the vector social pyramid.


```r
c(FALSE, NA_character_)
```

```
## [1] "FALSE" NA
```

5.  


```r
?is.atomic
?is.numeric
?is.vector
```

is.atomic is true for the atomic types ("logical", "integer", "numeric", "complex", "character" and "raw") and NULL.

The default method for is.numeric returns TRUE if its argument is of mode "numeric" (type "double" or type "integer") and not a factor, and FALSE otherwise. That is, is.integer(x) \|\| is.double(x), or (mode(x) == "numeric") && !is.factor(x).

If mode = "any", is.vector may return TRUE for the atomic modes, list and expression. For any mode, it will return FALSE if x has any attributes except names.

# Attributes

1.  


```r
#View(setNames)
#View(unname)
```

2.  


```r
x<-c(1,2,3)
dim(x)
```

```
## NULL
```

```r
nrow(x)
```

```
## NULL
```

```r
ncol(x)
```

```
## NULL
```

```r
NROW(x)
```

```
## [1] 3
```

```r
NCOL(x)
```

```
## [1] 1
```

3.  


```r
x1 <- array(1:5, c(1, 1, 5))
x2 <- array(1:5, c(1, 5, 1))
x3 <- array(1:5, c(5, 1, 1))
x1
```

```
## , , 1
## 
##      [,1]
## [1,]    1
## 
## , , 2
## 
##      [,1]
## [1,]    2
## 
## , , 3
## 
##      [,1]
## [1,]    3
## 
## , , 4
## 
##      [,1]
## [1,]    4
## 
## , , 5
## 
##      [,1]
## [1,]    5
```

```r
x2
```

```
## , , 1
## 
##      [,1] [,2] [,3] [,4] [,5]
## [1,]    1    2    3    4    5
```

```r
x3
```

```
## , , 1
## 
##      [,1]
## [1,]    1
## [2,]    2
## [3,]    3
## [4,]    4
## [5,]    5
```

4.  


```r
test<-structure(1:5, comment = "my attribute")
help(structure)
attributes(test)
```

```
## $comment
## [1] "my attribute"
```

```r
attr(test, which="comment")
```

```
## [1] "my attribute"
```

# S3 atomic vectors

1.  


```r
x<-c(1,2,3,4,2,3,1,3,8,6,8,9,7,10)
y<-table(x)
attributes(y)
```

```
## $dim
## [1] 9
## 
## $dimnames
## $dimnames$x
## [1] "1"  "2"  "3"  "4"  "6"  "7"  "8"  "9"  "10"
## 
## 
## $class
## [1] "table"
```

```r
typeof(y)
```

```
## [1] "integer"
```

2.  


```r
f1 <- factor(letters)
f1
```

```
##  [1] a b c d e f g h i j k l m n o p q r s t u v w x y z
## Levels: a b c d e f g h i j k l m n o p q r s t u v w x y z
```

```r
attributes(f1)
```

```
## $levels
##  [1] "a" "b" "c" "d" "e" "f" "g" "h" "i" "j" "k" "l" "m" "n" "o" "p" "q" "r" "s"
## [20] "t" "u" "v" "w" "x" "y" "z"
## 
## $class
## [1] "factor"
```

```r
levels(f1) <- rev(levels(f1))
f1
```

```
##  [1] z y x w v u t s r q p o n m l k j i h g f e d c b a
## Levels: z y x w v u t s r q p o n m l k j i h g f e d c b a
```

```r
attributes(f1)
```

```
## $levels
##  [1] "z" "y" "x" "w" "v" "u" "t" "s" "r" "q" "p" "o" "n" "m" "l" "k" "j" "i" "h"
## [20] "g" "f" "e" "d" "c" "b" "a"
## 
## $class
## [1] "factor"
```

3.  

f2 has the levels in the original order but the vector inverted. f3 has the levels in the reverse order but the vector in right order.


```r
f2 <- rev(factor(letters))
f2
```

```
##  [1] z y x w v u t s r q p o n m l k j i h g f e d c b a
## Levels: a b c d e f g h i j k l m n o p q r s t u v w x y z
```

```r
attributes(f2)
```

```
## $levels
##  [1] "a" "b" "c" "d" "e" "f" "g" "h" "i" "j" "k" "l" "m" "n" "o" "p" "q" "r" "s"
## [20] "t" "u" "v" "w" "x" "y" "z"
## 
## $class
## [1] "factor"
```

```r
f3 <- factor(letters, levels = rev(letters))
f3
```

```
##  [1] a b c d e f g h i j k l m n o p q r s t u v w x y z
## Levels: z y x w v u t s r q p o n m l k j i h g f e d c b a
```

```r
attributes(f3)
```

```
## $levels
##  [1] "z" "y" "x" "w" "v" "u" "t" "s" "r" "q" "p" "o" "n" "m" "l" "k" "j" "i" "h"
## [20] "g" "f" "e" "d" "c" "b" "a"
## 
## $class
## [1] "factor"
```

# Lists

1.  

-   Elements can be of different types.
-   Each element in a list is a reference to another object.
-   Create list with list(), not c().
-   Lists are recursive, they can contain other lists.

2.  


```r
#View(as.vector)
```

3.  


```r
date <- as.Date("1970-02-01")
str(date)
```

```
##  Date[1:1], format: "1970-02-01"
```

```r
attributes(date)
```

```
## $class
## [1] "Date"
```

```r
now <- as.POSIXct("2018-08-01 22:00", tz = "UTC")
str(now)
```

```
##  POSIXct[1:1], format: "2018-08-01 22:00:00"
```

```r
attributes(now)
```

```
## $class
## [1] "POSIXct" "POSIXt" 
## 
## $tzone
## [1] "UTC"
```

```r
v1<-c(date, now)
str(v1)
```

```
##  Date[1:2], format: "1970-02-01" "2018-08-01"
```

```r
attributes(v1)
```

```
## $class
## [1] "Date"
```

```r
v2<-unlist(list(date, now))
str(v2)
```

```
##  num [1:2] 3.10e+01 1.53e+09
```

```r
attributes(v2)
```

```
## NULL
```

c() coerces the date-time into date, unlist just converts everything into numeric.

# Data frames and tibbles


```r
library(tibble)
dplyr::starwars
```

```
## # A tibble: 87 × 14
##    name        height  mass hair_…¹ skin_…² eye_c…³ birth…⁴ sex   gender homew…⁵
##    <chr>        <int> <dbl> <chr>   <chr>   <chr>     <dbl> <chr> <chr>  <chr>  
##  1 Luke Skywa…    172    77 blond   fair    blue       19   male  mascu… Tatooi…
##  2 C-3PO          167    75 <NA>    gold    yellow    112   none  mascu… Tatooi…
##  3 R2-D2           96    32 <NA>    white,… red        33   none  mascu… Naboo  
##  4 Darth Vader    202   136 none    white   yellow     41.9 male  mascu… Tatooi…
##  5 Leia Organa    150    49 brown   light   brown      19   fema… femin… Aldera…
##  6 Owen Lars      178   120 brown,… light   blue       52   male  mascu… Tatooi…
##  7 Beru White…    165    75 brown   light   blue       47   fema… femin… Tatooi…
##  8 R5-D4           97    32 <NA>    white,… red        NA   none  mascu… Tatooi…
##  9 Biggs Dark…    183    84 black   light   brown      24   male  mascu… Tatooi…
## 10 Obi-Wan Ke…    182    77 auburn… fair    blue-g…    57   male  mascu… Stewjon
## # … with 77 more rows, 4 more variables: species <chr>, films <list>,
## #   vehicles <list>, starships <list>, and abbreviated variable names
## #   ¹​hair_color, ²​skin_color, ³​eye_color, ⁴​birth_year, ⁵​homeworld
```

1.  Yes, both:


```r
data.frame(x=c(), y=c())
```

```
## data frame with 0 columns and 0 rows
```

```r
data.frame()
```

```
## data frame with 0 columns and 0 rows
```

2.  You get an error:


```r
#data.frame(x=c(1,2,3), y=c(4,5,6), row.names = c("Algo", "Otro", "Algo"))
```

3.  It creates a matrix:


```r
df<-data.frame(x=c(1,2,3), y=c(4,5,6))
t(df)
```

```
##   [,1] [,2] [,3]
## x    1    2    3
## y    4    5    6
```

```r
t(t(df))
```

```
##      x y
## [1,] 1 4
## [2,] 2 5
## [3,] 3 6
```

```r
is.data.frame(t(df))
```

```
## [1] FALSE
```

```r
is.matrix(t(df))
```

```
## [1] TRUE
```

```r
is.data.frame(t(t(df)))
```

```
## [1] FALSE
```

```r
is.matrix(t(t(df)))
```

```
## [1] TRUE
```

As it creates a matrix it coerces elements to the same kind.


```r
df<-data.frame(x=c("1","2","3"), y=c(4,5,6))
t(df)
```

```
##   [,1] [,2] [,3]
## x "1"  "2"  "3" 
## y "4"  "5"  "6"
```

```r
t(t(df))
```

```
##      x   y  
## [1,] "1" "4"
## [2,] "2" "5"
## [3,] "3" "6"
```

```r
is.data.frame(t(df))
```

```
## [1] FALSE
```

```r
is.matrix(t(df))
```

```
## [1] TRUE
```

```r
is.data.frame(t(t(df)))
```

```
## [1] FALSE
```

```r
is.matrix(t(t(df)))
```

```
## [1] TRUE
```

If one of the columns is a list it kind of messes up and counts each element of the list as a column, repeating by the number of rows, as it needs to convert the list to atomic vectors:


```r
df<-data.frame(x=list(1,"hey",3), y=c(4,5,6))
t(df)
```

```
##         [,1]  [,2]  [,3] 
## x.1     "1"   "1"   "1"  
## x..hey. "hey" "hey" "hey"
## x.3     "3"   "3"   "3"  
## y       "4"   "5"   "6"
```

```r
t(t(df))
```

```
##      x.1 x..hey. x.3 y  
## [1,] "1" "hey"   "3" "4"
## [2,] "1" "hey"   "3" "5"
## [3,] "1" "hey"   "3" "6"
```

```r
is.data.frame(t(df))
```

```
## [1] FALSE
```

```r
is.matrix(t(df))
```

```
## [1] TRUE
```

```r
is.data.frame(t(t(df)))
```

```
## [1] FALSE
```

```r
is.matrix(t(t(df)))
```

```
## [1] TRUE
```

4.  

Similar to the examples before, if coerces to the same kind all elements, and if one column is a list it creates a mess. Data.matrix incorporates each column separately, without coercing and allowing lists.


```r
df<-data.frame(x=c("uu","hey","aa"), y=c(4,5,6))
as.matrix(df)
```

```
##      x     y  
## [1,] "uu"  "4"
## [2,] "hey" "5"
## [3,] "aa"  "6"
```

# NULL
