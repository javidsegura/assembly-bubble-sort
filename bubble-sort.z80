ORG 0x0000


START_OF_MEMORY  EQU 0x1000
NUMBER_OF_ELEMENTS EQU 5
CURRENT_ITERATION EQU 0

;--------------------------------------------------
; Bubble Sort Routine
;--------------------------------------------------
BUBBLE_SORT:
OUTER_LOOP:
        LD C, 0                   ; Clear swap flag (using register C)
        LD B, NUMBER_OF_ELEMENTS - 1  ; Set inner loop counter (for adjacent pairs)
        LD A, B
        SUB H
        LD B, A
        LD IX, START_OF_MEMORY    ; Reset pointer to start of array

INNER_LOOP:
        LD A, (IX)                ; Load first element into A
        LD D, (IX+1)              ; Load adjacent element into D
        CP D                      ; Compare A with D
        JP C, NO_SWAP            ; If A <= D (NC set), skip swapping

        CALL SWAP_SUBROUTINE

NO_SWAP:
        INC IX                   ; Move pointer to next element (now second becomes first for next pair)
        DEC B
        JP NZ, INNER_LOOP          ; Decrement inner counter (B) and loop if not zero

        ; If any swap occurred during this pass, repeat the outer loop.
        LD A, C                  ; Transfer swap flag into A
        OR A                     ; Set flags based on A (Z flag will be reset if A ≠ 0)
        JP NZ, CONTINUE_OUTER_LOOP        ; If a swap occurred, run another pass

        JP HALT_PROGRAM          ; Otherwise, sorting is complete

CONTINUE_OUTER_LOOP:
    INC H               ; Increment outer loop counter
    JP OUTER_LOOP       ; Repeat outer loop
    
SWAP_SUBROUTINE:
    LD (IX), D               ; Store D into the first element
    LD (IX+1), A             ; Store A into the second element
    LD C, 1 
    RET


;--------------------------------------------------
; Halt Program
;--------------------------------------------------
HALT_PROGRAM:
        HALT                     ; Stop execution

;--------------------------------------------------
; Data: Unsorted Array at 0x1000
;--------------------------------------------------
        ORG START_OF_MEMORY
        DB   1,60,30,10,99    ; Example unsorted numbers
