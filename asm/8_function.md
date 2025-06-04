### Code has all the concepts

```arm
	// Idea is to mimic the working of a function
	// using lr register and bx
	// also "return val"; 
	// Concepts: 
		// Resuse registers used in caller function
		// Work in current pushed function
		// Once done come back to next instruction of the function
		// Restore previous values of register [present in stack area]
		// Resume working from there


.global _start
_start:
	mov r0, #1
	mov r1, #6
	
	// add these by a function
	// store the values in stack section
	push {r0, r1}
	bl add2 // bl vs bal: bal: anyway always go to this branch, but bl stores the addr of the next instruction
	// which comes in handy when the called fn is popped and we come back to the caller function
	pop {r0, r1}
	// also for retuned value we ask r2 as we did that in add2
	
	b exit
	
add2:
	// here wer can resuse the register values
	add r2, r0, r1
	// return r0
	bx lr // asl lr
	
exit:


```


#### Concepts used
- `Resuse` registers used in `caller` function
    - Assume, push {r0, r1} => bl add2 => `undo` pop {r0, r1}
    - Becoz we can restore the previous values, using the above idea 
- Work in current pushed function
    - Can reuse r0, r1
- Once done come back to next instruction of the function
    - This is achieved by:-
        - `caller` has `bl add2` => Stores the addr of next of instruction in `lr`
        - From `function that is called` => ask linker register i.e `bx lr` 
- Restore previous values of register [present in stack area]
    - pop {r0, r1}
- Return value:-
    - In `fn that is called`
        - add r2, r0, r1
    - After coming back to `caller` i.e after `bx lr`
        - We can use value inside `r2`
