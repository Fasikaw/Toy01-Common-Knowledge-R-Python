# Study-[R & Python]
Computer science is fundamentally problem-solving. We can think of problem-solving as the process of taking some input (details about our problem) and generate some output (the solution to our problem). The "black box" in the middle is computer science. 




------------------------------------------------------------------------------------------------------------------------------------
# *R*
### 0. Basic
 - Check type : `class()`
 - Start: `head()`,`summary()`,`str()`
 - Convert type: `df %>% convert(num(a), fct(b), dte(c), chr(d), int(e), dbl(f,g))`: 
   - In the `df`, column`a` becomes numeric, column`b` becomes factor, column`c` becomes date, column`d` becomes character, column`e` becomes integer, column `f`,`g` become double. 
 - Convert type: `df %>% mutate(a = as.character(a), b = as.character(b), c = as.integer(c), d = as.double(d), e = as.numeric(e))`

### 1. vector
Vectors must contain the same type of data, that is the entries must all be of the **same type** such as: character, logical (TRUE or FALSE), or numeric. You can add values to a vector.
 - `c()` is a generic function that combines arguments to form a vector.
```
L <- c("Chris Saden", "Lauren Castellano","Sarah Spikes","Dean Eckles","Andy Brown", "Moira Burke","Kunal Chawla")

V <- c(100,200,300)
V <- seq(from=100, to=300, by=100)

N <- c(1:10); N
N <- c(N, 11:20); N
```
 [1]  1  2  3  4  5  6  7  8  9 10
 
 [1]  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20
 
 - `names()` gives names to the vector data
```
names(V) <- c(‘human’, ‘animal’, ‘tree’); V
```
<img src="https://user-images.githubusercontent.com/31917400/35448840-4aad3790-02b3-11e8-9d24-73dfa750662f.jpg" />

 - `nchar()` gives a vector that contains the number of characters for each of the names in
```
mystery = nchar(L); mystery
```
 [1] 11 17 12 11 10 11 12

 - Here we get a logical (or boolean) vector that tells us at what locations or indices in the vector where the number of characters for the name is equal to 11.
```
mystery == 11
L[mystery == 11]
```
 [1]  TRUE FALSE FALSE  TRUE FALSE  TRUE FALSE FALSE
 
 [1] "Chris Saden" "Dean Eckles" "Moira Burke"

### 2. matrix
```
A <- matrix(c(1,2,3,4,5,6), 2,3); A
```
<img src="https://user-images.githubusercontent.com/31917400/35448597-9944f66e-02b2-11e8-889d-68f9eb5dda76.jpg" />

```
b_num <- 1:6
b_dim <- c(2,3)
B <- matrix(b_num, b_dim); B
```
<img src="https://user-images.githubusercontent.com/31917400/35448597-9944f66e-02b2-11e8-889d-68f9eb5dda76.jpg" />

```
C <- matrix(nrow=2,ncol=3)
C[,1] <- c(1,2)
C[,2] <- c(3,4)
C[,3] <- c(5,6); C
```
<img src="https://user-images.githubusercontent.com/31917400/35448597-9944f66e-02b2-11e8-889d-68f9eb5dda76.jpg" />

**Q1.** Generate 20 random samples from Poisson with (lambda:2.5) and creating matrix with nrow=4, thus ncol=5 ?
```
P <- matrix(rpois(20, 2.5), nrow=4); P
qplot(rpois(20, 2.5), binwidth=1) 
```
<img src="https://user-images.githubusercontent.com/31917400/35449794-ed1f403e-02b5-11e8-9b3b-55dc0781d6f7.jpg" width="450" height="120" />

**Q2.** Generate 20 random samples from Exponential with (lambda:2.5), creating matrix with nrow=4, ncol=5, then generate 20 random samples from "CDF of Exponential" with (lambda:2.5), creating matrix with nrow=4, thus ncol=5 ? Write a sample generater in the 'inv_exp' function.
```
E <- matrix(rexp(20, 2.5), nrow=4); E

n <- 20
lambda <- 2.5
u <- runif(n)
x <- - log(1-u)/lambda

F <- matrix(x, nrow=4); F

qplot(x)

inv_exp <- function(n, lambda) {
  u <- runif(n)
  x <- - log(1-u)/lambda
  x
}

qplot(inv_exp(20, 2.5))
```
<img src="https://user-images.githubusercontent.com/31917400/35450381-c1047b0c-02b7-11e8-987d-1f2a9bb21369.jpg" width="650" height="170" />

 - `colSums()`,`rowSums()` give SUM of columns or rows in the matrix
```
A <- matrix(c(1,2,3,4,5,6), 2,3); A

b_num <- 1:6
b_dim <- c(2,3)
B <- matrix(b_num, b_dim); B
```
```
rowSums(A)
colSums(A)

apply(A, 1, sum) #1 is row
apply(A, 2, sum) #2 is col
```
 - `cbind()`,`rbind()` add them to the original matrix? 
```
A <- cbind(A, apply(A, 1, sum))
A <- rbind(A, apply(A, 2, sum)); A

B <- cbind(B, rowSums(B))
B <- rbind(B, colSums(B)); B
```
<img src="https://user-images.githubusercontent.com/31917400/35451170-3f2cecd8-02ba-11e8-8fd8-a53feea3fced.jpg" />

 - Re-label the headers..row, col
```
colnames(A) <- c(1:3, 'SUM')
rownames(A) <- c(1:2, 'SUM'); A
```
<img src="https://user-images.githubusercontent.com/31917400/35451432-21503d40-02bb-11e8-96ec-2ff03a525f99.jpg" />

### 3. dataframe
 - All entry vectors (columns) should be in the same length!
```
x1 <- c(8,2,6,4,5,3,7,1,9,10)
x2 <- c('d','i','i','i','e','i','g','i','i','c')
x3 <- c('TRUE','TRUE','FALSE','NA','FALSE','TRUE','NA','TRUE','FALSE','FALSE')
is.na(x3) <- x3=='NA' #'creating missing data..

X <- data.frame(x1, x2, x3); X
```
<img src="https://user-images.githubusercontent.com/31917400/35454550-5f1e278a-02c6-11e8-8f7e-bf0319932042.jpg" />

 - typical starting **DataFrame** !
```
names(X)
dim(X)
str(X) 
summary(X)
is.na(x3) 
sum(is.na(X)) 

apply(X, 2, is.na)
apply(apply(X, 2, is.na), 2, sum)

#delete all rows with 'na'
Y = na.omit(X); Y
```
<img src="https://user-images.githubusercontent.com/31917400/35455949-ccd5161c-02cb-11e8-8005-dc2f7825c297.jpg" width="650" height="170" />

>Want to drop some ?

`X$x3[4] <- X$x3[7] <- NULL` doesnt work.. WHY? it only works when it's an "entire column"..for example,
```
X$x3 <- NULL #:it works..
X[3, ] <- NULL #:it doesn't work..'NULL' only works with columns? 
X <- X[-3] #:it drops a column
X <- X[-3, ] #:it drops a row 
X <- X[-3:-5, ] #:it drops rows.....Use'-'when dropping rows..
```
 - Selection
```
X[ ,c(1,3)]
X[3:5, c(1,3)]
X[3,1:2]
X[sample(1:8, 4), ] #in all rows, choose 4 rows at random.. 
X[order(x1), ] #sort by row based on column 'x1' 
X[X$x1 > 5 & X$x2 == 'i', ] #what the fuck is the which??
X[which(X$x1 > 5 | X$x2 == 'i'), ]
X[ ,sapply(X, is.numeric)] #show all columns..that consist of numbers..WHY sapply()? 
X[-c(2,5), ] #show all rows except the row 2, 5
X[!(x2=='i'), ] #show all rows except x2 are 'i'
```
<img src="https://user-images.githubusercontent.com/31917400/35455062-73549034-02c8-11e8-98a1-9f41f2934e53.jpg" />

 - `table()` Counting the frequency
```
table(x1) 
table(x2)
table(x3)
table(x1, x2)
table(x1,x2,x3)
```
<img src="https://user-images.githubusercontent.com/31917400/35455444-ce4118ea-02c9-11e8-8442-05c39031bf9d.jpg" />

>poisson generates integers..then we can convert the table-result into a dataframe! 
```
y <- rpois(200, 1.5); y
table(y)
data.frame(table(y))
```
<img src="https://user-images.githubusercontent.com/31917400/35455633-a03e3562-02ca-11e8-9413-518d77c732a3.jpg" width="650" height="170" />

 - `sample(c())` random reproduction
```
A <- rep(c(1:3), each = 3)
A1 <- rep(c(1:3), 3)
df <- data.frame(A,A1); df

x <- runif(10); x #random uniform
y <- letters[5:14]; y 
z <- sample(c(rep('T',5), rep('F',5))); z #random T/F
yxz <- data.frame(y,x,z); yxz
```
<img src="https://user-images.githubusercontent.com/31917400/35456712-66d1cc5e-02ce-11e8-8f9d-a5480d50e2e8.jpg" />

 - `subset(data, cond, selecting vector)` select multiple columns at once.
```
subset(mtcars, mpg>=30|hp<60, c(vs,am))

mtcars[mtcars$mpg>=30|mtcars$hp<60, ]  # the above is better than this. 
```
<img src="https://user-images.githubusercontent.com/31917400/35457213-09931bf4-02d0-11e8-907d-19dfb93de2ab.jpg" width="650" height="120" />

 - `factor()` Factor variables are **categorical variables** that can be either numeric or string. There are a number of advantages to converting categorical variables to factor variables. First, they can be used in statistical modeling where they will be implemented correctly, i.e., they will then be assigned the correct number of **degrees of freedom**. Factor variables are also very useful in many different types of graphics. Furthermore, storing string variables as factor variables is a more efficient use of memory. The only required argument is a **vector of values** which can be either string or numeric. 
 - 'levels' argument: determines the categories of the factor variable, and the default is the sorted list of all distinct values. 
 - 'labels' argument: a vector of values that will be the labels of the categories in the levels argument. 
 - 'exclude' argument: defines which levels will be classified as NA in any output using the factor variable.
 
 - __The first factor 'a_f'__
`sample()` Generate a vector of binary data with the size of 20
```
a <- sample(0:1, 20, replace = TRUE); a
is.factor(a)
is.numeric(a)
```
<img src="https://user-images.githubusercontent.com/31917400/35465532-a72fd5b8-02f4-11e8-8c19-3d2b49288407.jpg" width="650" height="50" />

`factor(data, labels)` The first label, private, will correspond to a=0 and the second label, public, will correspond to a=1 because the order of the labels will follow the numeric order of the data. 
```
a_f <- factor(a, labels=c('private','public')); a_f
is.factor(a_f)
```
<img src="https://user-images.githubusercontent.com/31917400/35465601-0db89c8e-02f5-11e8-8d00-51efc620128d.jpg" width="650" height="80" />

 - __The second factor 'ses_f'__
Generate a string variable called ses (socio-economic status) in the same size as 'a' 
```
ses <- c("low", "middle", "low", "low", "low", "low", "middle", "low", "middle",
         "middle", "middle", "middle", "middle", "high", "high", "low", "middle",
         "middle", "low", "high")
is.character(ses)
```
[1] TRUE

Creating another factor variable called 'ses_f'
```
ses_f <- factor(ses)
is.factor(ses_f)
levels(ses_f)
```
[1] "high"  "low"  "middle"

>The problem here is that the levels are ordered according to the alphabetical order of the categories of 'ses'.

`factor(data, levels)` In order to fix the ordering we need to use the levels argument to indicate the "correct ordering" of the categories.
```
ses.f <- factor(ses, levels = c("low", "middle", "high"))
is.factor(ses.f)
levels(ses_f)
```
[1] "high"  "low"  "middle"

`ordered(levels)` We can also create 'ordered factor'. This function has the same arguments as the `factor()`. 
```
ses_order <- ordered(ses, levels=c("low", "middle", "high"))
is.factor(ses_order)
levels(ses_order)
```
[1] "low"  "middle"  "high"  

 - __Adding or dropping 'levels'__

**Let's add a level !** 
```
ses_f[21] <- 'veryhigh'
ses_f
```
[1] low middle low low low low middle low middle middle middle middle middle high high low middle middle low high [NA] 
 
We can see that instead of changing from “high” to “very.high”, the label was changed from “high” to [NA]. 

To do this correctly, we need to first add the new level, “very.high”, to the factor variable 'ses.f' which we do by using the factor function with the levels argument. Then we can finally add an element to the factor variable from the new level.
```
ses_f <- factor(ses_f, levels = c(levels(ses_f), "veryhigh"))
ses_f[21] <- "veryhigh"
ses_f
```
[1] low middle low low low low middle low middle middle middle middle middle high high low middle middle low high veryhigh

**Let's drop the level.** Note! you cannot directly remove the factor, so need to create new variable 'ses_ff' and assign factor again.  
```
ses_ff <- ses_f[ses_f != "veryhigh"]; ses_ff
ses_ff <- factor(ses_ff)
levels(ses_ff)
```
[1] "high"  "low"  "middle"

 - __Visualizing__ 
 
Create an additional continuous variable called 'read' with a size 0f 20 which contains the reading scores.
```
read <- c(34, 39, 63, 44, 47, 47, 57, 39, 48, 47, 34, 37, 47, 47, 39, 47, 47, 50, 28, 60)
```
Combining all the variables in a data frame
```
combo <- data.frame(a, a_f, ses, ses_f, read); combo
table(a, ses)
table(a_f, ses_f)
```
<img src="https://user-images.githubusercontent.com/31917400/35466579-efc15312-02fc-11e8-9ca0-7bab35f1fa01.jpg" width="650" height="140" />

`bwplot()` As in the tables the factor variable will indicate a better ordering of the graphs as well as add useful labels.
```
library(lattice)
bwplot(a_f ~ read | ses_ff, data = combo, layout = c(2, 2))
```
<img src="https://user-images.githubusercontent.com/31917400/35466646-7f937c22-02fd-11e8-914c-82a833c4eb2d.jpg" width="400" height="300" />

### 4. Simple Data formatting before Visualization 
Datasets should be manipulated into a specified format. Not all datasets look nice. Sometimes we pull data from different sources such as - webpage, pdf, etc. We may need to reshape or rearrange our data into different format. This is a necessary step prior to conducting DataAnalysis. Load your data and get it in the right format before you can visualize it. #There are also packages to help with formatting, mainly 'dplyr' and 'tidyr'. 
 - 1.Loaded data from CSV files
 - 2.Subsetted data frames
 - 3.Edited data to make it easier to manage
 - 4.Merged multiple datasets
The dataset here is state-level data from the United States Census Bureau's American Community Survey. It shows income averages for various demographics.

__1. Load files__
```
income <- read.csv("C:/Users/Minkun/Desktop/classes_1/NanoDeg/1.Data_AN/L7/---New R/data/ACS_13_5YR_S1903/ACS_13_5YR_S1903.csv")
head(income, 2)
str(income)
```
<img src="https://user-images.githubusercontent.com/31917400/35473029-aaa84e0a-0371-11e8-9986-d1bbe8b067c0.jpg" width="700" height="130" />

Sometimes, Be more specific. R treated the column of data as numeric instead of a character, but 'GEO.id2' is str. You can specify this 
with the 'colClasses' argument. Note:'stringsAsFactors' is set to FALSE. Just do this always.
```
income <- read.csv("C:/~/ACS_13_5YR_S1903/ACS_13_5YR_S1903.csv", stringsAsFactors=FALSE, sep=",", colClasses=c("GEO.id2"="character"))
income <- read.csv("C:/~/ACS_13_5YR_S1903/ACS_13_5YR_S1903.tsv", stringsAsFactors=FALSE, sep="\t", colClasses=c("GEO.id2"="character"))
income <- read.csv("http://datasets.flowingdata.com/tuts/2015/load-data/ACS_13_5YR_S1903.csv", stringsAsFactors=FALSE, sep=",", colClasses=c("GEO.id2"="character"))

income[1:5,c(1,2)]
```
<img src="https://user-images.githubusercontent.com/31917400/35473069-55b5fc2a-0372-11e8-882a-b8a5e8b45137.jpg" width="600" height="60" />

__2. Subset__

Maybe you just want to look at income estimates for the total population for now. This is the first seven columns (with the first two indicating region)
```
income_total <- income[,1:7]
head(income_total, 3)
summary(income_total)
```
<img src="https://user-images.githubusercontent.com/31917400/35473102-f8baa470-0372-11e8-9f56-9266927324c3.jpg" width="600" height="100" />

You can also subset based on values using `subset()`. Let's say, maybe you only want to look at states in the 'upper quartile'.
```
income_upper <- subset(income_total, HC02_EST_VC02 >= 58985)
```

>You can also remove rows with missing values in any of the fields. 
```
income_wo_na <- na.omit(income); income_wo_na 
income_wo_na <- na.omit(income_total); income_wo_na 
```
In this case, you get an empty data frame, because every state has at least one missing value amongst the 153 fields. In contrast, if you ran the function with income_total, you’d just get the same data frame, because no values are missing for the first seven columns.

__3. Edit__

Change column names
```
names(income_total) <- c("id", "FIPS", "name", "households", "households_moe", "med_income", "med_income_moe")
```
In income_total, you have **median** and **margin of error(moe)**. Maybe you want to add a column for minimum and another for maximum. That’s the median income column plus and minus the margin of error. 
```
income_total$med_min <- income_total$med_income - income_total$med_income_moe
income_total$med_max <- income_total$med_income + income_total$med_income_moe
```
Convert existing column (units to the thousands). When you divide a vector by a single number, the operation is performed on each element of that vector. Same with other basic operations.
```
income_total$med_min <- income_total$med_min / 1000
income_total$med_max <- income_total$med_max / 1000
```
__4. Merge__

Load the datasets.
```
income2008 <- read.csv("C:/Users/Minkun/Desktop/classes_1/NanoDeg/1.Data_AN/L7/---New R/data/ACS_08_3YR_S1903/ACS_08_3YR_S1903.csv", stringsAsFactors=FALSE, sep=",", colClasses=c("GEO.id2"="character"))
income2013 <- read.csv("C:/Users/Minkun/Desktop/classes_1/NanoDeg/1.Data_AN/L7/---New R/data/ACS_13_5YR_S1903/ACS_13_5YR_S1903.csv", stringsAsFactors=FALSE, sep=",", colClasses=c("GEO.id2"="character"))
```

Subset
```
income2008p <- income2008[,c("GEO.id2", "HC02_EST_VC02", "HC02_MOE_VC02")]
income2013p <- income2013[,c("GEO.id2", "HC02_EST_VC02", "HC02_MOE_VC02")]
```

Rename headers. For the **id**, which is actually a FIPS (Federal Information Processing Standards) code, we make it the same in both datasets.
```
names(income2008p) <- c("FIPS", "med2008", "moe2008")
names(income2013p) <- c("FIPS", "med2013", "moe2013")
```

Combine and bring this together
```
income0813 <- merge(income2008p, income2013p, by="FIPS")
head(income0813, 3)
```
<img src="https://user-images.githubusercontent.com/31917400/35473242-ef2a6290-0374-11e8-8da3-d4c83f591431.jpg" width="500" height="40" />

Save these two data frames as CSV files to use later on in a different program. Specify the dataframe, file destination, and the separator. Row names are used by default, but I typically set it to "FALSE".
```
write.table(income_total, "C:/Users/Minkun/Desktop/classes_1/NanoDeg/1.Data_AN/L7/---New R/data/income-totals.csv", row.names=FALSE, sep=",")
write.table(income0813, "C:/Users/Minkun/Desktop/classes_1/NanoDeg/1.Data_AN/L7/---New R/data/income-2008-13.csv", row.names=FALSE, sep=",")
```



------------------------------------------------------------------------------------------------------------------------------------
# *Python*
### 0. Basic
 - Check type: `type()` 
 - Start: `head()`,`describe()`,`info()`
 - Convert type: `int()`, `float()`, `str()`, `list()`
   - ex) `list('AB')` --- ['A', 'B']
   
__STR__  
 - '$'`.join(str)`
   - city = 'scjen%$38' then, '$'.join(city) --> 's$c$j$e$n$%$$$3$8'
 - in string, \n :start a new line, \t :create a tab space
   - print('Python is\n great!')
   - print('Python is\t great!')
 - METHOD for string (Methods are related to functions but each is associated with specific types) 
   - str`.lower()` / str`.upper()` / str`.capitalize()`
   - str`.count('char')`
   - sentence {}`.format(variable)` 
   - str`.split()`
   - str`.strip('char')` ---note:only works for char in the 'first' and 'last'.  
   - str`.replace("morning", "night")`
   - str1`.index(str2)`
  
__LIST__
 - Built-in function for **LIST**
   - indirect: 
     - sum(list), len(list), max(list), min(list), join(list), sorted(list, reverse=T/F)
     - 'char'.join(list) ---> returns a str consisting of the list elements joined by a separator.
       - 'and'.join(x) ---> 'AandBandCandD'
   - direct: 
     - list`.sort()`, list`.reverse()`  
     - list`.append(value)`, list`.extend(variable)`, list`.insert(index, value)`,
     - list`.remove(value)`, list`.clear()`  
     - list`.count(value)`, 
     - list`.index(value, beg-i, end-i)` shows the location of the value..within the given range..
     - list`.pop(i)` returns the value of i index. the default is the last item.
     - 

__LOOP__
 - 1. Basic with LIST: 
   - instead of retrieving the item indexes and looking up each element, we can just loop over our list using a plain "for-in" loop.
 ```
colors = ["red", "green", "blue", "purple"]

for color in colors:
    print(color)
 ```
 - 2. Basic(Range of length) with LIST
 ```
colors = ["red", "green", "blue", "purple"]

for i in range(len(colors)):
    print(colors[i])
---------------------------------------------------------------------------
presidents = ["Washington", "Adams", "Jefferson", "Madison", "Monroe", "Adams", "Jackson"]

for i in range(len(presidents)):
    print("President {}: {}".format(i + 1, presidents[i]))
 ```
 - 3. while with LIST: 
   - mimic the behavior of our traditional C-style 
 ```
colors = ["red", "green", "blue", "purple"]

i = 0
while i < len(colors):
    print(colors[i])
    i += 1
 ```
 - 4. Index & item with LIST
   - loop over a list and retrieve both the index and the value of each item in the list
   - `start=1` option to enumerate here is optional. If we didn’t specify this, we’d start counting at `0` by default.
 ```
presidents = ["Washington", "Adams", "Jefferson", "Madison", "Monroe", "Adams", "Jackson"]

for num, name in enumerate(presidents, start=1):
    print("President {}: {}".format(num, name))
 ```
 - 5. loop over two lists simultaneously
   - `zip` with different size lists will stop after the shortest list runs out of items.
 ```
colors = ["red", "green", "blue", "purple"]
ratios = [0.2, 0.3, 0.1, 0.4]

for i, color in enumerate(colors):
    ratio = ratios[i]
    print("{}% {}".format(ratio * 100, color))
---------------------------------------------------------------------------
colors = ["red", "green", "blue", "purple"]
ratios = [0.2, 0.3, 0.1, 0.4]

for color, ratio in zip(colors, ratios):
    print("{}% {}".format(ratio * 100, color))
 ```
 
 
 
 
 
 
 

### Pandas & Numpy     
 - why Numpy?
   - it gives 'arrays' as a data structure. (multidimensional) 
   - it gives 'statistical func'     
 - why Pandas?
   - it gives 'dataframes' as a data structure
   - it gives '.read_csv()' method 

>Select from a dataframe 
 - Select data-point ? 
   - df`.loc['row_name'or row_index ,'col_name']`
   - df`.iloc[row_index, col_index]`
 - Selct **rows**
   - df`.ix[index_number]` or df`.ix[slicing]`
   - df`.loc[[list of 'row_name']]` or df`.iloc[[list of row_index]]`
 - Select **columns**
   - It's a Series ! you dummy !
 
 
### 1. np.Array
 - np.array(LIST) : **vector**
<img src="https://user-images.githubusercontent.com/31917400/35475085-11eefd52-0390-11e8-8b18-9e830eb31485.jpg" width="700" height="100" />

 - np.array([LIST, LIST]) : **matrix** 
<img src="https://user-images.githubusercontent.com/31917400/35475130-ea34ed7a-0390-11e8-92ca-d19ae94ce020.jpg" width="700" height="160" />

### 2. pd.Dataframe
 - pd.DataFrame([LIST, LIST], columns=LIST)
<img src="https://user-images.githubusercontent.com/31917400/35475176-a0710c4a-0391-11e8-9ab8-f76ba37f6179.jpg" width="700" height="300" />

 - pd.DataFrame(dictionary)
<img src="https://user-images.githubusercontent.com/31917400/35475250-0b6a157c-0393-11e8-8184-68c0469156e4.jpg" width="700" height="80" /> 

 - rename columns
<img src="https://user-images.githubusercontent.com/31917400/35475286-83b2a62a-0393-11e8-84a4-146e0b1525ab.jpg" width="700" height="240" /> 

### combining different datasets
https://pandas.pydata.org/pandas-docs/stable/merging.html

### replacing wrong values tip
<img src="https://user-images.githubusercontent.com/31917400/60037929-deea1400-96aa-11e9-8aef-333329c8b1aa.jpg" />    



------------------------------------------------------------------------------------------------------------
# Extra Tip_2: Trial & Error project collections

## Q1. Most frequent word in the string
Write a function that returns the most frequently occurring word in a given string. For example, if the input s is `s = 'I scream you scream we all scream for ice cream'`, the result should be `scream` as it is the most frequent word in this sentence. If there is a tie for the most common word, return only one result, the first (tied) word in alphabetical order. 
    # HINT: Use the built-in split() function to transform the string s into an array
    # HINT: Iterate through the array and count each occurance of every word using the .count() list method
    # HINT: Find the number of times the most common word appears using max()
    # HINT: Locate the index of the most frequently seen word
    # HINT: Return the most frequent word. Remember that if there is a tie, return the first (tied) word in alphabetical order.

```
def most_frequent(s):
    ar = s.split()
    pool = []
    for i in range(0,len(ar),1):
        cc = ar.count(ar[i])     ## it shows how many times the element appears in the str ##
        pool.append(cc)
    mx = max(pool)     ## it shows the biggest element. ##
    ind_loc = pool.index(mx)     ## it gives the location of the element. ##
    result = ar[ind_loc]
    return result

def test_run():
    print most_frequent("cat bat mat cat bat cat")     ## output: 'cat' ##
    print most_frequent("betty bought a bit of butter but the butter was bitter")      ## output: 'butter' ##
    print most_frequent("london bridge is falling down falling down falling down london bridge is falling down my fair lady")

if __name__ == '__main__':
    test_run()
```

## Q2. Date & Time
1. `datetime.datetime` is the combination of 'date'class and 'time'class.
 - my birthday?
```
import datetime
my_day = datetime.datetime(1981, 8, 10, 21, 30, 45); my_day
```
/// datetime.datetime(1981, 8, 10, 21, 30, 45) --- This is a 'datetime object!!!
```
print(my_day)
```
/// 1981-08-10 21:30:45
```
my_day.strftime('%Y-%m-%d')
```
/// '1981-08-10' --- I converted it to str!!!

 - today?
```
today = datetime.datetime.today() # or datetime.datetime.now()
print(today)
```
/// 2018-01-23 22:50:03.543023 --- This is a 'datetime object!!!

2. **define** date and time elements
```
year = datetime.datetime.today().year
month = datetime.datetime.today().month
day = datetime.datetime.today().day
hour = datetime.datetime.today().hour
minute = datetime.datetime.today().minute
second = datetime.datetime.today().second
```
3. `datetime.date()` process Year, Month, Day. First, we need to come up and offer... year, month, day then 'date()' processes them.
```
date_c = datetime.date(2016, 12, 24)   # introducing certain day #
date_d = datetime.date(year, month, day)   # today's date #
date_e = date_d - date_c   ### calculating days passed. ### 

print('First meetup : {}'.format(date_c))
print('Today is  : {}'.format(date_d))
print("It's been {}days".format(date_e.days))
```
<img src="https://user-images.githubusercontent.com/31917400/35305561-9d98e112-0091-11e8-871a-971a7e7866c2.jpg" />    

4. `datetime.time()` process Hour, Minute, Second with (Time zone)
```
time_a = datetime.time(21, 30, 24)
print('we meet at: {}'.format(time_a))
```
<img src="https://user-images.githubusercontent.com/31917400/35305674-1aec45be-0092-11e8-9101-c97ef07f989b.jpg" />    

5. manipulation
 - `strftime()` -str_Format_time- is the way to ask python about the string format we want. It works with`datetime.date()` as well.
```
today_2 = datetime.datetime.today().strftime('%Y + %m + %d %H peekaboo %M:%S')

print(today_2)
type(today_2)
```
<img src="https://user-images.githubusercontent.com/31917400/35305755-80a0e2a2-0092-11e8-99f4-3dc73e6dd916.jpg" />    

 - `strptime()` -str_Parse_time- is the way we teach python date&time. Need to introduce certain 'time str' and articulating the format one by one so that python understands. It works with`datetime.date()` as well ?
```
d1 = datetime.datetime.strptime('2017/12/21 14|00|38', '%Y/%m/%d %H|%M|%S')

d2 = d1.replace(year=9999, month=9, day=29, hour=11, minute=59, second=49)

print('Check-in :', end=' ')
print(d1)

print('New Ckeck-in :', end=' ')
print(d2)
```
<img src="https://user-images.githubusercontent.com/31917400/35305877-118971a8-0093-11e8-81a8-7234b401ae38.jpg" />    

 - timestamp: time (in sec) has passed since 1970/01/01. it returns a float ! It does not work with `datetime.date()`. 
```
date_a = "2016-07-17 12:23:45"
date_b = "Sun, 17 Jul 2016 12:34:56 GMT"

d3 = datetime.datetime.strptime(date_a, "%Y-%m-%d %H:%M:%S")
d4 = datetime.datetime.strptime(date_b, "%a, %d %b %Y %H:%M:%S GMT")

print(d3)
print(d4)
d3.timestamp(), d4.timestamp()
```
<img src="https://user-images.githubusercontent.com/31917400/35356079-3fc9b55a-0147-11e8-9e19-814763af6d3e.jpg" />    
       
   <img src="https://user-images.githubusercontent.com/31917400/35306223-86de549a-0094-11e8-8974-4e545792302a.jpg" width="360" height="450" />    

 - `fromtimestamp()` We can convert timestamp to the date in the format.
```
a = datetime.datetime.fromtimestamp(d3.timestamp())
print(a)
```
<img src="https://user-images.githubusercontent.com/31917400/35356886-a9e16d0a-0149-11e8-957b-4ac5f7732b1a.jpg" />    

 - `combine()` We can combine date and time.
```
b = datetime.datetime.combine(datetime.date.today(), datetime.time(22,22,22))
print(b)
```
<img src="https://user-images.githubusercontent.com/31917400/35356890-ac7bd4ec-0149-11e8-9862-4f58c799e5e7.jpg" />    

6. `datetime.timedelta()` it works with `datetime.date()` .... and `datetime.datetime()` as well
```
# 3 days later
print(datetime.date(2018,2,4) + datetime.timedelta(days=3))
print(datetime.datetime(2018,2,4,5,36,35) + datetime.timedelta(days=3))

# 7 hours later
print(datetime.datetime(2018,2,4,5,36,35) + datetime.timedelta(hours=7)) 

# etc
print(datetime.datetime(2018,2,4,5,36,35) + datetime.timedelta(weeks=2,days=3,hours=-3,minutes=30))
print(datetime.datetime(2018,2,4,5,36,35) + datetime.timedelta(minutes=3,milliseconds=-20,microseconds=400))
```
<img src="https://user-images.githubusercontent.com/31917400/35363531-4c377f78-0162-11e8-9d80-bd17fe3d214a.jpg" />    


> time module
1. it gives each individual element ? and has always sth to do with **EPOCH** ?
 - `gmtime()` gives tm_year, tm_mon, tm_mday, tm_hour, tm_min, tm_sec. 
 - Plus, 
   - **tm_wday:** 0 (Mon), 1 (Tue), ....
   - **tm_yday:** counting days from the begining of the year
   - **tm_isdst:**
```
import time
tt = time.gmtime()

print(t2.tm_year)
print(t2.tm_mon)
print(t2.tm_mday) ##
print(t2.tm_hour)
print(t2.tm_min)
print(t2.tm_sec)
print(t2.tm_wday) ##
print(t2.tm_yday) ##
print(t2.tm_isdst) ##?????
```
<img src="https://user-images.githubusercontent.com/31917400/35306605-83c2f692-0096-11e8-993f-1fe3bdce953f.jpg" />    

```
365 - tt.tm_yday
```
 - `ctime()` converts a time expressed in **seconds** since the epoch(1970/01/01) to a string representing local time. If secs is not provided or None, the 'current time' as returned by 'time()' is used.
```
timestr=time.ctime(1234567890)  #'Sat Feb 14 08:31:30 2009' is 1234567890 sec 

time.strptime(timestr, "%a %b %d %H:%M:%S %Y")
```
<img src="https://user-images.githubusercontent.com/31917400/35307250-d5859f68-0099-11e8-9e82-75c00f42b4a1.jpg" />    

 - When caculating, we convert all into 'sec'
```
#35 days in sec (day-hour-min-sec) = 3024000
35 * 24 * 60 * 60

#3 weeks in sec (week-day-hour-min-sec) = 1814400
3 * 7 * 24 * 60 * 60

#1 week in sec (week-day-hour-min-sec) = 604800
1 * 7 * 24 * 60 * 60
```

>Write a function that returns 'the day' that follows a specified time period after an initial date. Time periods can be specified in two different ways: as a number of days like "1 day" or "30 days", or as a number of weeks like "2 weeks" or "12 weeks". This function takes as **input** a string depicting a date in `YYYY/mm/dd` format and a string stating a time period in the form of "X day(s)" or "Y week(s)". **Output** should be a string in form `YYYY/mm/dd` with **the date that is X days or Y weeks after the initial date.**
```
ef which_date(start_date,t):

    import datetime
    initial = datetime.date(int(start_date.split('/')[0]), int(start_date.split('/')[1]), int(start_date.split('/')[2]))
    if 'day' in t:
        nex = datetime.timedelta(int(t.split()[0])) 
    elif 'week' in t:
        nex = datetime.timedelta(int(t.split()[0])*7)
    
    end_date = (initial + nex).strftime('%Y/%m/%d')
    
    return end_date
    
def test():
    assert which_date('2016/02/10','35 days') == '2016/03/16'
    assert which_date('2016/12/21','3 weeks') == '2017/01/11'
    assert which_date('2015/01/17','1 week') == '2015/01/24'
    print("All tests completed.")


if __name__ == "__main__":
    test()
```

# [NOTE]:`pd.to_datetime()`
(https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.to_datetime.html)

---------------------------------------------------------------------------------------------------
# Object Oriented Programming
<img src="https://user-images.githubusercontent.com/31917400/77896575-684cf900-7270-11ea-937d-37a234effeaa.png" /> 

## > Because...
1. Modularity
 - Each object is generated from the corresponding "blue-print" as a separate entity in the code. They work together to achieve a common goal.
2. Reusability
 - We are working on the "blue-print" representing the `Data`+`Actions` of the object. Each "blue-print" is a puzzle piece that comes together to create a certain functionality. 
 - We can create multiple objects from the "blue-print" we design and we can also use the same "blue-print" in several different projects.
3. Extensibility
 - It is easy to add new features or functionality by using the existing functionality to avoid the code repetition. You can extend the functionality of your program by adding new "blueprints" that use existing functionality from other "blueprints". 
4. Maintainability, Testing, Debugging 
 - We can work with different "blue-prints" that create different objects interacting each other in the code such that if we make a change to one of the "blue-prints", the other "blue-prints" should not be greatly affected by that chance, or we are able to know exactly where to look.   
  
 

### > Two Bld-Blocks
 - 1. Classes
 - 2. Instances

 - ### 1. Classes
   - class = `blue-print`
   - Each class is a **blue-print** describing the attributes and functionality of an **object** or **abstract concept** (For example, houses, bank accounts, employees, clients, cars, products...) 
   - Class names are nouns and they should start with an uppercase letter. If the name has more than one word, each word should be 
capitalized.
   - In short, a class contains the `data`, and the `action` of the objects that belong to a class. 
     - data = `attributes`
     - action = `methods`
   - __Main Elements__
     - Class Attributes 
     - Constructor `def __init__(?)`
     - Methods `def blah(?)`
     <img src="https://user-images.githubusercontent.com/31917400/77844542-7da62280-719f-11ea-9d5e-ae62202efce0.png" />
     
     ```
     class <ClassName>:
     
         # "Class" Attributes
         <class attribute> = <value>
         
         # "Constructor" and "Instance" Attributes
         def __init__(self, <parameters>):
             self.<instance attribute1> = <value1>
             self.<instance attribute2> = <value2>
             . . .
             
         # Methods
         def <method_name> (self, <parameters>):
             . . . 
     ```
 - ### 1-1. Class Attribute
   - Belonging to a class, it is shared by all the instances(its change affects all instances you create).
   - It is defined within the class.   
   - How to access? `<class_name>.<class_attribute>` or `<instance_name>.<class_attribute>`
   - How to modify? `<class_name>.<class_attirbute> = <value>`
     
 - ### 2. Instances
   The instance attribute is defined within the constructor in the class.
   - instance = `object` 
   - Instances are created from a class. They are concrete objects created based on the "blue-print"(class), and each of which is totally independent object. "class" is like a **catagory**. If "class" is an abstract representation of a certain object, while "instance" is a concrete example of a certain object develped from the "class".
   - All objects generated by the same class share the same instance attribute, but the values of the instance attributes for each object are independent! 
     <img src="https://user-images.githubusercontent.com/31917400/77850505-ef479600-71ca-11ea-934b-761b4af6fc3a.png" />
  
   - 1> Let's define the **instance attributes** in the class. First, think about what features are supposed to vary by each object(instance). If the category is about 'dog', then 'name' might vary! Ok! then build the **instance attribute** of 'name' inside of the "Constructor". The constructor initializes the **instance attributes**.   
     ```
     class Dog:
     
         def __init__(self, age_param, name_param, is_male_param, weight_param, ailment_param=None, num_baby_param=0):
             self.age = age_param
             self.name = name_param
             self.is_male = is_male_param    # Boolean: True is Male, False if Female.
             self.weight = weight_param
             self.ailment = ailment_param    # String
             self.num_baby = num_baby_param  # Integer
             self.owner = "Minkun~always"    # fixed attribute !!! Unnecessary to specify in the argument of the constructor
     ```
     - [Note]: what is "self"? It's referring to the instance! 
   - 2> Let's create the **instances**: `<ins_variable_name> = <class_name>(param, param,...)`
     ```        
     my_dog = Dog(5, "Selly", True, 15, ["cough", "insomnia"]) # this omitting default implies the dog doesn't have a baby 
     ```
   - 3> Let's access the **instance attributes**: `<ins_variable_name>.<instance_attribute>`
     ```
     my_dog.name
     ```
   - 4> Let's modify the **instance attributes**(like..updating the value): `<ins_variable_name>.<instance_attribute> = <new_value>`
     ```
     my_dog.is_male = False
     ```
### > Two Principles: Encapsulation & Abstraction
 - ### 1. Encapsulation
   : It refers to the bundling of `Data`(attribute) and `Actions`(method) into a class. It has a purpose of "information hiding" or "access restriction". 

 - ### 2. Abstraction(Hierarchical Generalization using Class)
   : The `interface` should be independent of the `implementation`. Let's say the classes should interact with each other as the program grows. We have to decide what part of our code(data? action?) is going to be public(accessible from anywhere) and which part (data? action?) is only accessible within a class. "Interface" as a USER'S VIEW is a part of the code that is publicly available for use, and "Implementation" as a DEVELOPER'S VIEW is a part of the code that relates "how the code is written to achieve the goal functionality"?   
     <img src="https://user-images.githubusercontent.com/31917400/78508933-66100080-7782-11ea-84c5-96cda6347039.png" />

 - Let's see how **attributes** works to achieve the principles of Encapsulation & Abstraction! Use **Privacy / Publicity** ?
   - No attribute is ever private in Python. They can still be accessed outside of the class, but according to the conventions, you shouldn't.
   - There is a convention of privacy such as `_` and `__`. 
   ```
   class Employee:
     
       def __init__(self, name_param, age_param, address_param, number_param, vehicle_param=None):
           self.name = name_param         
           self._age = age_param           # "_"<protection-01>: Not To Access this attribute from outside of the class...
           self._address = address_param   # "_"<protection-01>: Not To Access this attribute from outside of the class...
           self.__number = number_param    # "__"<protection-02>: Not To Access this attribute from outside of the class...
           self.__vehicle = vehicle_param  # "__"<protection-02>: Not To Access this attribute from outside of the class...
   
   employee01 = Employee("John", 56, "5th Ave", 34523, "Honda")
   employee01._age                # it works
   employee01.__number            # it won't work coz it's in a "name mangling" process.
   employee01._Employee.__number  # it works if it comes with its class name.
   ```
### > Getters & Setters, and Properties
Getters and Setters are `actions` as members of a class...so they are "Methods" for the instance that can call them. Their purpose is to "get" and "set" the value of an instance attribute. **They protect `data` by providing an indirect way to access**. 
 - __Getters__ helps access the attribute **indirectly**. 








### > Methods
### > OO-Analysis
### > Aliasing, Mutation, Cloning
### > Inheritance, Polymorphism
### > How to work with Multiple files?
### > How to document my code using Docstrings?
-----------------------------------------------------------------------------------------------------







































































