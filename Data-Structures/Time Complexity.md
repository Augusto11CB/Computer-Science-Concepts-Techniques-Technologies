# Time Complexity
Time complexity helps describing a way of showing how the runtime of a function increases as the size of the input increases.
 
Time Complexity and Big O Notation try to answer the following question:
> How does the runtime of this function grow as the size of the input grows.
 
## How to Determine Time Complexity ?
**STEPS**
- Find the fastest growing term
- Take out the coefficient

Exemple: T = an+b = O(n)
				 T = cn² + dn + e = O(n²)

### Formal, Mathematical Definition of Big-O:

> O(g(n))  is a set of functions. Any other function  f(n)  is in the set  O(g(n))  if the ratio between  f  and  g,  f(n)/g(n)​,  eventually goes and stays at or below some constant  C  as n  gets very large.

[TODO](#Big-O-Mathematical-Exemple.png)

### Analysis of Loops
- **O(n^someValue)**: Time complexity of nested loops is equal to the number of times the innermost statement is executed. For example the following sample loops have O(n2) time complexity
```
   for (int i = 1; i <=n; i++) {
       for (int j = 1; j <=n;  i++) {
          // some O(1) expressions
       }
   }
```

- **O(Logn)** Time Complexity of a loop is considered as O(Logn) if the loop **variables is divided / multiplied by a constant** amount.
```
//Case 1
for (int i = 1; i <=n; i *= c) {
       // some O(1) expressions
}
//for (int i = n; i > 0; i /= c) {
       // some O(1) expressions
}
```

	- Case 1, `i` takes values `1, c, c2, c3, ..., clogc(n)`, so there are in total `log(n)` many iterations, and for each iteration there is a constant amount of work to be done (i.e. `O(1)` amount of work), so the total amount of work done is `log(n) * O(1) = O(log(n))`.
	- Case 2, `i` takes values `n, n / c, n / c2, n / c3, ..., , n / clogc(n)`, so there are in total `log(n)` many iterations and each iteration takes constant amount of time, so the total time complexity is `O(log(n))`.

- **O(LogLogn)** Time Complexity of a loop is considered as O(LogLogn) if the loop variables is reduced / increased exponentially by a constant amount.
```
   // Here c is a constant greater than 1   
   for (int i = 2; i <=n; i = pow(i, c)) { 
       // some O(1) expressions
   }
   //Here fun is sqrt or cuberoot or any other constant root
   for (int i = n; i > 1; i = fun(i)) { 
       // some O(1) expressions
   }
```

**How to combine time complexities of consecutive loops?**
```
 for (int i = 1; i <=m; i += c) {  
        // some O(1) expressions
   }
   for (int i = 1; i <=n; i += c) {
        // some O(1) expressions
   }
```
Time complexity of above code is O(m) + O(n) which is O(m+n)
If m == n,  the time complexity becomes O(2n) which is O(n).

**How to calculate time complexity of recursive functions?**

### Find the complexity - Exercises
**Problem 1**
```
void function(int n) 
{ 
	int count = 0; 
	for (int i=n/2; i<=n; i++) 
		for (int j=1; j<=n; j = 2 * j) 
			for (int k=1; k<=n; k = k * 2) 
				count++; 
} 
```

**Solution 1**
```
void function(int n) 
{ 
    int count = 0; 
    for (int i=n/2; i<=n; i++) 
  
        // Executes O(Log n) times 
        for (int j=1; j<=n; j = 2 * j) 
  
            // Executes O(Log n) times 
            for (int k=1; k<=n; k = k * 2) 
                count++; 
} 
```
**Problem 2**
```
void function(int n) 
{ 
	int count = 0; 
	for (int i=0; i<n; i++) 
		for (int j=i; j< i*i; j++) 
			if (j%i == 0) 
			{ 
				for (int k=0; k<j; k++) 
					printf("*"); 
			} 
} 

```
**Solution 2**
```
void function(int n) 
{ 
	int count = 0; 

	// executes n times 
	for (int i=0; i<n; i++) 

		// executes O(n*n) times. 
		for (int j=i; j< i*i; j++) 
			if (j%i == 0) 
			{ 
				// executes j times = O(n*n) times 
				for (int k=0; k<j; k++) 
					printf("*"); 
			} 
} 

```

## Asymptotic Notion
**Asymptotic Notations** are the expressions that are used to represent the complexity of an algorithm.

## Scenarios - Type of Analysis
- **Best Case** (Omega Notation (Ω)): In which is analysed the performance of an algorithm for the input, for which the algorithm takes less time or space.
- **Worst Case** (Big-O Notation (Ο)): In which  the performance of an algorithm for the input, for which the algorithm takes long time or space.
- **Average Case** Theta Notation (θ): In which is analysed the performance of an algorithm for the input, for which the algorithm takes time or space that lies between best and worst case.


# 
## References
[https://beginnersbook.com/2018/10/ds-asymptotic-notation/](https://beginnersbook.com/2018/10/ds-asymptotic-notation/)

[https://www.geeksforgeeks.org/analysis-of-algorithms-set-3asymptotic-notations/?ref=rp](https://www.geeksforgeeks.org/analysis-of-algorithms-set-3asymptotic-notations/?ref=rp)

[https://www.geeksforgeeks.org/analysis-of-algorithms-set-4-analysis-of-loops/?ref=rp](https://www.geeksforgeeks.org/analysis-of-algorithms-set-4-analysis-of-loops/?ref=rp)

[https://www.geeksforgeeks.org/analysis-algorithms-set-5-practice-problems/?ref=rp](https://www.geeksforgeeks.org/analysis-algorithms-set-5-practice-problems/?ref=rp)


