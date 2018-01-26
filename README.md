# Study-R-Python-SQL
Don't forget

------------------------------------------------------------------------------------------------------------------------------------
### R
#### 1. vector
Vectors must contain the same type of data, that is the entries must all be of the **same type** such as: character, logical (TRUE or FALSE), or numeric. You can add values to a vector.
 - `c()` is a generic function that combines arguments to form a vector.
```
L <- c("Chris Saden", "Lauren Castellano","Sarah Spikes","Dean Eckles","Andy Brown", "Moira Burke","Kunal Chawla")
V <- c(100,200,300)
N <- c(1:10); N
N <- c(N, 11:20); N
```
 [1]  1  2  3  4  5  6  7  8  9 10
 
 [1]  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20
 
 - Give names to the vector data
```
names(V) <- c(‘human’, ‘animal’, ‘tree’)
```
 - A vector that contains the number of characters for each of the names in
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

 - 






























------------------------------------------------------------------------------------------------------------------------------------
### Python













------------------------------------------------------------------------------------------------------------------------------------
### SQL























































































