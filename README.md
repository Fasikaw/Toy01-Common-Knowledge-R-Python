# Study-R-Python-SQL
Don't forget

------------------------------------------------------------------------------------------------------------------------------------
# *R*
### 0. Basic
 - Check type : `class()`
 - 


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
 - Convert type: `int()`, `float()`, `str()`, `list()`
   - list('AB') --- ['A', 'B']
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



------------------------------------------------------------------------------------------------------------------------------------
# *SQL*

### 0. Basic
Thinking about how different pieces of data relate to each other is at the heart of relational databases
<img src="https://user-images.githubusercontent.com/31917400/35476981-b554aa66-03b1-11e8-8df6-679c7bb283f8.jpg" width="300" height="160" /> 
<img src="https://user-images.githubusercontent.com/31917400/35477036-d3ac95d6-03b2-11e8-99dc-f850dde7d5bf.jpg" width="300" height="160" /> 

>Data Type
<img src="https://user-images.githubusercontent.com/31917400/35476878-e4f73c9a-03af-11e8-9af6-272f78e9e99d.jpg" width="500" height="600" /> 

>Syntax
 - create statement: CREATE TABLE table (col_1 value_1, col_2 value_2,...)  
 - insert statement: INSERT table (col_1, col_2,...) VALUE (val_1, val_2,...)

(https://www.postgresql.org/docs/9.4/static/sql-createdatabase.html)

(https://www.postgresql.org/docs/9.4/static/sql-dropdatabase.html)

(https://www.postgresql.org/docs/9.4/static/sql-createtable.html)

(https://www.postgresql.org/docs/9.4/static/sql-droptable.html)

>Connect Python code into a SQL-database
<img src="https://user-images.githubusercontent.com/31917400/35477173-c561ca98-03b5-11e8-8ea8-2d16054f3513.jpg" />

```
import psycopg2 as sq

db = sq.connect('path')
cursor = db.cursor()
cursor.execute('query')

results = cursor.fetchall()
print(results)

conn.close()
```













































































