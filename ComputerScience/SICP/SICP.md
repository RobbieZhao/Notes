Install sicp and simply-scheme in Dr. Racket

## [Course websites](https://inst.eecs.berkeley.edu//~cs61a/su10/index.html)

## Notes from [videos](https://www.youtube.com/playlist?list=PLhMnuBfGeCDNgVzLPxF9o5UNKG1b-LFY9)

### L01

 - Why do we need functional way to represent mathematical expressions?

   - Consistency. In math, you can have prefix, infix, suffix operators or operators that are positioned somewhere else. In functional way, it's always prefix.

 - How does Scheme evaluated things?

        (a b c d e)
 
   - First evaluate a b c d e. The value of a is a function, the rest are values. Then call the function with those values. 

 - A special case of the above evaluation process is `define`:

    
        (define (square x) ; x is the formal parameter
            (* x x))       ; (* x x) is the body
    
        (square (+ 2 3))   ; (+ 2 3) is the actual argument expression 
                           ; (5 is the actual argument value)
 - The other special case is `if`
		
		(if condition
		    expr1
		    expr2)
 - predicate function: returns true or false
 - Fix `plural` function:

		#lang simply-scheme
		
		(define (plural wd)
		  (if (and (ends-with-y? wd)
		           (consonant? (second-to-last wd)))
		      (word (bl wd) 'ies)
		      (word wd 's)))
		
		(define (ends-with-y? wd)
		  (equal? (last wd) 'y))
		
		(define (second-to-last wd)
		  (last (bl wd)))
		  
		(define (vowel? letter)
		  (member? letter '(a e i o u)))
		
		(define (consonant? letter)
		  (not (vowel? letter)))
		
		(plural 'book)
		(plural 'fly)
		(plural 'boy)

### L02

 - Don't use "go back" when thinking about recursion.
 - Abstraction
 - Functions don't care about other things. Given the same input, they always return the same output.
   - f(x) = 2x + 6 v.s. g(x) = 2(x + 3)
     - Same function: given same input, always return same outputs.
     - Different procedure: procedure is a sequence of steps for computing something.
   - `random` is not a function (because it might return different result)
 - cond `(cond clause clause clause ...)`
   - clause: `(test action)`
        
 - applicative order (which scheme uses) v.s. normal order
   - applicative order: first evaluate the subexpressions (actual argument expressions), get the actual argument value, then call the function, substitute the value into the body
   - normal order: first substitute the subexpressions into the body, and it doesn't evaluate anything until it obtained an expression involving only primitive procedure (like +, *) (the example in the book seems to contradict with the example [here](https://sookocheff.com/post/fp/evaluating-lambda-expressions/))

### L03

 - higher order procedures: either it takes a procedure as an argument or returns a procedure as a value
 - lambda is the only way to make a procedure

### L04

 - First class datatype can be:
   - the value of a variable
   - an argument to a procedure
   - the value returned by a procedure
   - am member of an aggregate
   - anonymous
 - Special form: let

		(let bindings body)
		
		bindings = (binding binding binding ...)
		
		binding = (name value-expr) 
   - let form is an abbreviation:

			(let ((d (+ 4 5)))
			  (* d d))
			
			is an abbreviation of
			
			((lambda (d) (* d d)) (+ 4 5))
		
 - bindings cannot refer to each other
 - in `let*`, bindings can refer to each other

		(let* ((a 3)
		       (b (+ a 5)))
		  (* a b))
		  
		will be translated to:
		
		(let ((a 3))
		  (let ((b (+ a 5)))
		    (* a b)))


## Notes from the textbook

### 1.1 

 - read-eval-print loop
   - reads an expression from the terminal
   - evaluates the expression
   - prints the result
 - substitution model: replace the formal argument with actual argument value
 - Special forms: define, cond, if, and, or
 - bound variable, free variable, scope
 - lexical scoping
  
## [Lecture notes](https://web.archive.org/web/20091127212630/http://inst.eecs.berkeley.edu/~cs61a/reader/notes.pdf)