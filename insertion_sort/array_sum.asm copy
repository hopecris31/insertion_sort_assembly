## Sum an array with a subroutine.
## Hope Crisafi
PR_INT = 1                   # (example of defining a constant)
        .data
array:  .word -123, 548, 923, 431, 560, -348, 961
endarr:
message:    .asciiz "The array sum is: "   # print message
        .text
        .align 2

main:  
        la $a0, array          # a0 points into array
        la $a1, endarr         # a1 points to array end
        sub $t0, $a1, $a0      # t0 = endarr - array
        srl $a2, $t0, 2        # a2 = size = (endarr - array)/4
        addi $sp, $sp, -4      # push 
        sw $ra, 0($sp)         # ret addr on stack
        jal arrsum
        lw $ra, 0($sp)         # pop
        addi $sp, $sp, 4       # ret addr
        add $a0, $0, $v0       # copy sum into $a0
        addi $v0, $0, PR_INT   # print $v0
        syscall
        jr $ra                

arrsum:
    move $v0, $0   
    j loop
done:
    jr $ra                

loop:
    lw $t1, 0($a0)         # get next arr element
    add $v0, $v0, $t1      # add to sum
    addi $a0, $a0, 4       # point to next word
    addi $a2, $a2, -1      # decrement array size
    bgtz $a2, loop         # repeat while size > 0
    j done
