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

### 1.29

	#lang simply-scheme
	
	(define (sum term a next b)
	  (if (> a b)
	      0
	      (+ (term a)
	         (sum term (next a) next b))))
		
	(define (integral a b f n)
	  (define (coef i)
	    (cond ((or (= i 0)
	               (= i n)) 1)
	          ((even? i) 2)
	          (else 4)))
	  (define h (/ (- b a) n))
	  (define (add1 x) (+ x 1))
	  (define (yk k) (* (coef k)
	                    (f (+ a (* k h)))))
	  (* (/ h 3)
	     (sum yk 0 add1 n)))
	  
	  
	(define (cube n) (* n n n))
	
	(integral 0 1 cube 100) 
	(integral 0 1 cube 1000)
	
### 1.31

	#lang simply-scheme
	
	(define (product a b f next)
	  (if (> a b)
	      1
	      (* (f a)
	         (product (next a) b f next))))
	
	(define (addn n)
	  (lambda (x) (+ x n)))
	
	(define (factorial n)
	  (define (identity x) x)
	  (product 1 n identity (addn 1)))
	
	(factorial 5)
	
	(define (square x) (* x x))
	
	(/ (* 2.0 (product 4 100 square (addn 2)))
	   (* 101 (product 3 99 square (addn 2))))

### 1.32

	#lang simply-scheme
	
	(define (accumulate combiner null-value term a next b)
	  (if (> a b)
	      null-value
	      (combiner (term a)
	                (accumulate combiner null-value term (next a) next b))))
	
	(define (product term a next b)
	  (accumulate * 1 term a next b))
	
	(define (sum term a next b)
	  (accumulate + 0 term a next b))
	  
### 1.33 (*)

	#lang simply-scheme
	
	(define (filtered-accumulate combiner null-value term a next b filter)
	  (cond ((> a b) null-value)
	        ((filter a) (combiner (term a)
	                              (accumulate combiner null-value term (next a) next b)))
	        (else (accumulate combiner null-value term (next a) next b))))
	
	(define (add1 n) (+ n 1))
	
	(define (square n) (* n n))
	
	(filtered-accumulate + 0 square a add1 b prime?)
	
	(define (relative-prime? n i)
	  (define (relative-prime? n i num)
	    (cond ((< i num) #t)
	          ((and (= (remainder n num) 0)
	                (= (remainder i num) 0)) #f)
	          (else (relative-primer? n i (+ num 1)))))
	  (relative-prime? n i 2))
	
	(define (relative-prime-to-n? i)
	  (relative-prime? n i))
	
	(define (identity x) x)
	
	(filtered-accumulate * 1 identity 1 add1 (- n 1) relative-prime-to-n?)
	

answer for b should be (key is the gcd algorithm)

	(define (gcd m n)
	  (cond ((> n m) (gcd n m))
	        ((= n 0) m)
	        (else (gcd n (remainder m n)))))
	
	(define (relative-prime? m n)
	  (= (gcd m n) 1))
	
	(define (prod-rela-prime n)
	  (define (filter x)
	    (relative-prime? x n))
	  (filtered-accumulate * 1 identity 0 add1 n filter))

### 1.34

2 is not a procedure

### 1.35

	#lang simply-scheme
	
	(define (fixed-point f tolerance first-guess)
	  (define (close-enough? a b)
	    (< (abs (- a b)) tolerance))
	  (define (fixed-point guess)
	    (let ((next (f guess)))
	      (cond ((close-enough? guess next) next)
	            (else (fixed-point next)))))
	  (fixed-point first-guess))
	
	(define (f x)
	  (+ 1 (/ 1 x)))
	
	(define golden-ratio (fixed-point f 0.0001 1.0)) 
	
### 1.36

Without damping, it takes more number of steps to converge than with damping.

	#lang simply-scheme


	(define (fixed-point f tolerance first-guess)
	  (define (close-enough? a b)
	    (< (abs (- a b)) tolerance))
	  (define (fixed-point guess)
	    (display guess)
	    (newline)
	    (let ((next (f guess)))
	      (cond ((close-enough? guess next) next)
	            (else (fixed-point next)))))
	  (fixed-point first-guess))
	
	(display 'with-damping)
	(newline)
	
	(define solution-with-damping
	  (fixed-point (lambda (x) (/ (+ x (/ (log 1000)
	                                      (log x))) 2))
	               0.0001 2))
	
	(newline)
	(display 'without-damping)
	(newline)
	
	(define solution-without-damping
	  (fixed-point (lambda (x) (/ (log 1000)
	                              (log x)))
	               0.0001 2)) 

### 1.37

	#lang simply-scheme
	
	(define (cont-frac n d k)
	  (define (cont-frac n d k i)
	    (if (= i k)
	        (/ (n k) (d k))
	        (/ (n i) (+ (d i)
	                    (cont-frac n d k (+ i 1))))))
	  (cont-frac n d k 1))
	
	(cont-frac (lambda (i) 1.0)
	           (lambda (i) 1.0)
	           10)
	0.6180339887498948

### 1.38

	#lang simply-scheme
	
	(define (cont-frac n d k)
	  (define (cont-frac n d k i)
	    (if (= i k)
	        (/ (n k) (d k))
	        (/ (n i) (+ (d i)
	                    (cont-frac n d k (+ i 1))))))
	  (cont-frac n d k 1))
	
	(define (d i)
	  (if (or (= (remainder i 3) 0)
	          (= (remainder i 3) 1))
	      1
	      (* (+ (/ (- i 2) 3) 1) 2)))
	
	(+ (cont-frac (lambda (i) 1.0)
	              d
	              10)
	   2)

### 1.39

	#lang simply-scheme
	
	(define (square x) (* x x))
	
	(define (tan-cf x k)
	  (define (tan-cf x k i)
	    (cond ((= i k) (/ (square x) (- (* 2 k) 1)))
	          ((= i 1) (/ x (- 1 (tan-cf x k (+ i 1)))))
	          (else (/ (square x) (- (* 2 i) 1 (tan-cf x k (+ i 1)))))))
	  (tan-cf x k 1))
	  
### 1.40

	(define (cube x) (* x x x))
	
	(define (square x) (* x x))
	
	(define (cubic a b c)
	  (lambda (x)
	    (+ (cube x)
	       (* a (square x))
	       (* b x)
	       c)))

### 1.41 (*)

	(define (double f)
	  (lambda (x) (f (f x))))

Result will be 21

### 1.42

	#lang simply-scheme
	
	(define (compose f g)
	  (lambda (x) (f (g x))))
	
	(define (square x) (* x x))
	
	(define (inc x) (+ x 1))
	
	((compose square inc) 6)

### 1.43

	#lang simply-scheme
	
	(define (compose f g)
	  (lambda (x) (f (g x))))
	
	(define (repeated f n)
	  (define (repeated f i)
	    (if (= i n)
	        f
	        (compose f (repeated f (+ i 1)))))
	  (repeated f 1))
	
	(define (square x) (* x x))
	
	((repeated square 2) 5)

### 1.44

	(define (smooth f)
	  (lambda (x) (/ (+ (f (- x dx))
	                    (f x)
	                    (f (+ x dx)))
	                 3)))
	
	(define (smooth-repeated n)
	  (lambda (f) ((repeated smooth n) f)))

### 1.45

	#lang simply-scheme
	
	(define (compose f g)
	  (lambda (x) (f (g x))))
	
	(define (repeated f n)
	  (define (repeated f i)
	    (if (= i n)
	        f
	        (compose f (repeated f (+ i 1)))))
	  (repeated f 1))
	
	(define tolerance 0.00001)
	
	(define (fixed-point f first-guess)
	  (define (close-enough? v1 v2)
	    (< (abs (- v1 v2)) tolerance))
	  (define (try guess)
	    (let ((next (f guess)))
	      (if (close-enough? guess next)
	          next
	          (try next))))
	  (try first-guess))
	
	(define (average-damp f)
	  (lambda (x) (average x (f x))))
	
	(define (average x y)
	  (/ (+ x y) 2))
	
	(define (square x) (* x x))
	
	(define (power x n)
	  (if (= n 0)
	      1
	      (* x (power x (- n 1)))))
	
	(define (nth-root n x)
	  (fixed-point ((repeated average-damp (damp-times n)) (lambda (y) (/ x (power y (- n 1)))))
	               1.0))
	
	(define (damp-times n)
	  (define (search i)
	    (if (and (or (= n (power 2 i))
	                 (> n (power 2 i)))
	             (< n (power 2 (+ i 1))))
	        i
	        (search (+ i 1))))
	  (search 1))
	
	(nth-root 8 16)

### 1.46

	#lang simply-scheme
	
	(define (interative-improve good-enough? next)
	  (define (search guess)
	    (if (good-enough? guess)
	        guess
	        (search (next guess))))
	  (lambda (guess)
	    (search guess)))
	
	(define (square x) (* x x))
	
	(define (average x y) (/ (+ x y) 2))
	
	(define (sqrt x)
	  ((interative-improve (lambda (y) (< (abs (- (square y) x)) 0.001))
	                       (lambda (y) (average y (/ x y))))
	   1.0))
	
	(sqrt 4)
	
	(define (fixed-point f first-guess)
	  ((interative-improve (lambda (x) (< (abs (- (f x) x)) 0.00001))
	                       f)
	   first-guess))
	
	(fixed-point cos 1.0)


