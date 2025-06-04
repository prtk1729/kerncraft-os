### Code

```arm
.global _start
.equ endloop, 0xaaaaaaaa // same as #pragma  , remember .equ is "," separated

// looping: for loop or whikle loop
// ow to write terminating condition?
// When to stop?
// How to increment?


_start:
	ldr r0, =list // ro = list[] or base address of list
	mov r1, r0 // r1 is temp pointer
	
	ldr r2, =endloop // r2 = 0xaaaaaaaa, so that we can use this as tc
	
	// accumulator
	ldr r3, [r0] // r3 = *r0 i.e init to 1
	mov r4, #0

loop:
	// r3 ?= *(r1++)
	ldr r4, [r1, #4]!  // r4 = *(r1++), r4 = 2
	cmp r4, r2 
	beq exit // tc
	
	// passed tc => r4 contains list-val
	add r3, r3, r4
	bal loop
	
	
.data
list:
	.word 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 0xaaaaaaaa
	
exit:
```


#### The above code uses multiple concepts to execute `looping`

- Observations:-
    - We can use a sentinel (an `end-of-data` marker )
        - We use `0xaaaaaaaa` as we are assuminhg here that this is unlikely to appear in data
        - `.equ endloop, 0xaaaaaaaa // same as #pragma  , remember .equ is "," separated`
    - ```arm
        .data
        list:
            .word 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 0xaaaaaaaa
      ``` 
      - Here, `.data`, tells the assembler to switch from `code/text area` to `data` area
      - The `code/text` area is where the assembler is vcurrently in as it is executing this current code. It contains `executables`, object files, `high-level program or code`
      - Once, it swtches to `data` area, it is no more using registers i.e as regiusters are in CPU
    - `list:` This label is base-addr of `list`
    - We define the following data that are laid out are in `word type` i.e given by `.word`
    - So, 1, 2, 3..., 0xaaaaaaa are stored in 4B (`if word-size is 4B i.e 32 bit processor`)