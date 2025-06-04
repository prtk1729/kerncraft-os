#### Previous vs New Knowledge

##### Add to `r2 += 10` only if (`r0 < r1`)
- Previous Knowledge of `cmp and branching`
    - ```arm
      ```
- New knowledge of `simple [opcode]le, [opcode]ge, [opcode]lt, [opcode]gt`
    - ```arm
            .global _start
        _start:
            mov r0, #3
            mov r1, #5
            
            // r2 += 10 if r0 < r1
            cmp r0, r1 // checks cpsr flag
            
            blt branch
            bal exit
            
        branch:
            mov r2, #0
            add r2, r2, #10
            
        exit:
      ```

- Same objective can be achived by lesser code.
    ``arm
    .global _start
    _start:
        mov r0, #3
        mov r1, #5
        mov r2, #0 // reset
        
        // r2 += 10 if r0 < r1
        cmp r0, r1 // checks cpsr flag
        addlt r2, r2, #10

    ````