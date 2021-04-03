### Exercise 1.1

 - 10
 - 12	
 - 8
 - 3
 - 6
 - None
 - None
 - 19
 - `#f`
 - 4
 - 16
 - 6
 - 16

### Exercise 1.2

	(/ (+ 5 4 (- 2 (- 3 (+ 6 (/ 4 5)))))
	   (* 3 (- 6 2) (- 2 7)))

### Exercise 1.3

	(define (square n)
	  (* n n))
	
	(define (sum-of-square a b)
	  (+ (square a) (square b)))
	
	(define (sum-square-larger a b c)
	  (if (> a b)
	      (if (> b c)
	          (sum-of-square a b)
	          (sum-of-square b c))
	      (if (> a c)
	          (sum-of-square a c)
	          (sum-of-square b c))))
	
	(sum-square-larger 1 2 3)
	(sum-square-larger 4 3 2)

### Exercise 1.4

 - Evaluate `(if (> b 0) + -)`, get its value, which is either the `+` or `-` operator.
 - Procedure call of the operator with a and b

### Exercise 1.5

 - applicative-order: stack overflow
 - normal-order: return 0

### Exercise 1.6 *

This will be running forever, since the new-if will always evaluate the predicate, then-clause, and the else-clause.

### Exercise 1.7 *

For small numbers, say 0.0001. a deviation of 0.001 would be ten times larger, causing the root to be very inaccurate.

	(define (good-enough? guess x)
	  (< (/ (abs (- (improve guess x) guess)) guess) 0.001))

	
### Exercise 1.8

	#lang simply-scheme
	
	(define (cbrt-iter guess x)
	  (if (good-enough? guess x)
	      guess
	      (cbrt-iter (improve guess x) x)))
	
	(define (improve guess x)
	  (/ (+ (/ x (square guess)) (* 2 guess))
	     3))
	
	(define (good-enough? guess x)
	  (< (abs (- (cube guess) x)) 0.001))
	
	(define (cbrt x)
	  (cbrt-iter 1.0 x))
	
	(define (cube x)
	  (* x x x))
	
	(define (square x)
	  (* x x))
	
	(cbrt 8)
	    


	   













