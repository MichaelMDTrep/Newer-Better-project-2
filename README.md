# Newer-Better-project-2
makeCacheMatrix <- function(x = matrix()) {
## This sets up a square invertible matrix
## It then will return a list that will contain functions to set up the matrix, get the matrix and set the inverse.
     
 inv = NULL
 set = function(y) {

     
 
x <<- y
 inv <<- NULL
## Using ‘<<-‘to assign a value to an object in an environment
## This will make it different from the current environment

 }
 get = function() x
 setinv = function(inverse) inv <<- inverse 
 getinv = function() inv
 list(set=set, get=get, setinv=setinv, getinv=getinv)
 }
 
 cacheSolve <- function(x, ...) {
     
 inv = x$getinv()
##The INV function is being set equal to x.
 if (!is.null(inv)){
## What this basically means is that “if it is not equal to INV, there is no value to INV.” 
## It will get it from the cache and skip the computation
 message("getting cached data")
 return(inv)
 }
 
 mat.data = x$get()
 inv = solve(mat.data, ...)
 ##INV is equal to the data.
## It will set the value of ther inverse in the cache meaning, the setinv function.
 x$setinv(inv)

 return(inv)
 }
 test = function(mat){
## The function test basically takes in any invertible matrix, and will basically calculate the function twice using the functions above. It will print out the times for the runs. For instance the first run will take longer then the second.
 temp = makeCacheMatrix(mat){
##Mat is an invertible matrix.
 
 start.time = Sys.time()
 cacheSolve(temp)
 dur = Sys.time() - start.time
 print(dur)
 
 start.time = Sys.time()
 cacheSolve(temp)
 dur = Sys.time() - start.time
 print(dur)
 }
 set.seed(1110201)
 r = rnorm(1000000)
 mat1 = matrix(r, nrow=1000, ncol=1000)
 test(mat1)
 r = rnorm(1000000)
mat1 = matrix(r, nrow=1000, ncol=1000)
 test(mat1)
save.image("~/R Test 3/Working R function.RData")


 

## This basically sets the matrix with  a 1000 rows and 1000 columns filled with normal random numbers.
## It will set the time difference of 1.946601 seconds. 
## The second run then becomes 0.005 seconds. Which then makes it so it is a 99.8% decrease. 
