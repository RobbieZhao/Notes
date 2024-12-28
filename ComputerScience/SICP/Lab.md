## Week 1A part 1

### Q1

	#lang simply-scheme
	
	(define (abs n)
	  (cond ((> n 0) n)
	        (else (- n))))
	
	(abs -1)
	(abs 0)
	(abs 5)
	
### Q2

	#lang simply-scheme
	
	(define (address area-code)
	  (if (= area-code 415)
	      (word 'san 'francisco)
	      (if (= area-code 510)
	          'berkeley
	          'where-you-from)))
	
	(address 415)
	(address 510)
	(address 102)

 - 3
 - 4
 - 3

### Q3

 - `#t`
 - keep calling `foo`
 - return `#f`

## Week 1A part 2

### Q1

	#lang simply-scheme
	
	(define (expt base power)
	  (if (= power 0)
	      base
	      (* base (expt base (- power 1)))))
	
	(expt 3 2)
	(expt 2 3)

### Q2

	#lang simply-scheme
	
	(define (count-stair-ways n)
	  (cond ((= n 1) 1)
	        ((= n 2) 2)
	        (else (+ (count-stair-ways (- n 1))
	                 (count-stair-ways (- n 2))))))
	
	(count-stair-ways 1)
	(count-stair-ways 2)
	(count-stair-ways 3)

### Q3

	#lang simply-scheme
		
	(define (subsent st i)
	  (cond ((empty? st) '())
	        ((= i 0) st)
	        (else (subsent (bf st) (- i 1)))))
		
	(subsent '(6 4 2 7 5 8) 3)
	
### Q4

	#lang simply-scheme
	
	(define (count-ways x y)
	  (cond ((= x 0) 1)
	        ((= y 0) 1)
	        (else (+ (count-ways x (- y 1))
	                 (count-ways (- x 1) y)))))
	
	(count-ways 3 3)

### Q5

	#lang simply-scheme
	
	(define (sum-of-sents st1 st2)
	  (cond ((empty? st1) st2)
	        ((empty? st2) st1)
	        (else (se (+ (first st1) (first st2))
	                  (sum-of-sents (bf st1) (bf st2))))))
	
	(sum-of-sents '(1 2 3) '(6 3 9))
	(sum-of-sents '(1 2 3 4 5) '(8 9))

### Lab 1B

	#lang simply-scheme
	
	(define (substitute st old-wd new-wd)
	  (cond ((empty? st) '())
	        ((equal? (first st) old-wd) (sentence new-wd (substitute (bf st) old-wd new-wd)))
	        (else (sentence (first st) (substitute (bf st) old-wd new-wd)))))
	
	(substitute '(she loves you yeah yeah yeah) 'yeah 'maybe)