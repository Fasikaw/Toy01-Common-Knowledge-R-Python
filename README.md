# Study-R-Python-SQL
Don't forget

------------------------------------------------------------------------------------------------------------------------------------
# *R*
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

 - Counting the frequency
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

 - random reproduction
```
A <- rep(c(1:3), each = 3)
A1 <- rep(c(1:3), 3)
df <- data.frame(A,A1); df

x <- runif(10); x #random uniform
y <- letters[5:14]; y #WTF!!! is letter[ ] is a function??
z <- sample(c(rep('T',5), rep('F',5))); z #random T/F
yxz <- data.frame(y,x,z); yxz
```
<img src="https://user-images.githubusercontent.com/31917400/35456712-66d1cc5e-02ce-11e8-8f9d-a5480d50e2e8.jpg" />






































------------------------------------------------------------------------------------------------------------------------------------
### Python













------------------------------------------------------------------------------------------------------------------------------------
### SQL























































































