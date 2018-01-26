# Study-R-Python-SQL
Don't forget

------------------------------------------------------------------------------------------------------------------------------------
# *R*
#### 1. vector
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
 human animal   tree 
   100    200    300 

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

#### 2. matrix
```
A <- matrix(c(1,2,3,4,5,6), 2,3); A
```
     [,1] [,2] [,3]
[1,]    1    3    5
[2,]    2    4    6

```
b_num <- 1:6
b_dim <- c(2,3)
B <- matrix(b_num, b_dim); B
```
     [,1] [,2] [,3]
[1,]    1    3    5
[2,]    2    4    6

```
C <- matrix(nrow=2,ncol=3); C
C[,1] <- c(1,2)
C[,2] <- c(3,4)
C[,3] <- c(5,6); C
```
     [,1] [,2] [,3]
[1,]    1    3    5
[2,]    2    4    6














#### 3. dataframe



 - typical starting **DataFrame** !
```
names(df)
dim(df)
str(df) 
```































------------------------------------------------------------------------------------------------------------------------------------
### Python













------------------------------------------------------------------------------------------------------------------------------------
### SQL























































































