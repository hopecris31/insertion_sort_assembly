# Insertion Sort Lab 6
# Hope Crisafi

PR_STR = 4
PR_INT = 1

        .data
before_sort_message:	.asciiz "Before Sorting: "
after_sort_message: 	.asciiz	"After Sorting: "
space: 	.asciiz " "

array:  .word -9, 4, -2, 8, 7, 9, 5
endarr:
        .text
        .align 2

main:
    la $a0, array        # a0 arr address pointer
    la $a1, endarr       # a1 points end of arr
    sub $t4, $a1, $a0    # array len
    srl $t5, $t4  2      # a2 = ASIZE = (endarr - array)/4
    move $a1, $t5
    move $s0, $a0
    move $s1, $a1
    la $a0, before_sort_message
    li $v0, 4
    syscall
    
    addi $sp, $sp, -4    # push
    sw $ra, 0($sp)       # ret addr on stack
    jal print_array
    lw $ra, 0($sp)       # pop
    addi $sp, $sp, 4     # ret addr
    
    move $a0, $s0
    move $a1, $s1
    
    addi $sp, $sp, -4    # push
    sw $ra, 0($sp)       # ret addr on stack
    jal iSort            #call insertion sort
    lw $ra, 0($sp)       # pop
    addi $sp, $sp, 4     # ret addr
    
    move $s0, $a0
    move $s1, $a1
    la $a0, after_sort_message
    li $v0, 4
    syscall
    
    addi $sp, $sp, -4
    sw $ra, 0($sp)
    jal print_array
    lw $ra, 0($sp)
    addi $sp, $sp, 4

    jr $ra


iSort:
    li $t2, 0    # initialize j
    li $t4, 0    # initialize tmp
    li $t3, 1    # int i = 1
    
forLoop:
    move $t2, $t3        # j = i
    sll $t7, $t3, 2
    add $t7, $t7, $a0    # address a[i]
    lw $t4, 0($t7)        # tmp = a[i]
    j while

whileBody:
    sw $t1, 0($t0)        # a[j] = a[j-1]
    addi $t2, $t2, -1    # j--

while:
    bge $0, $t2, forLoopCondition    # first while condition
    sll $t6, $t2, 2            # shifting j to add to base address
    add $t0, $a0, $t6        # address of j added to base
    lw $t1, -4($t0)            # a[j-1]
    bge $t4, $t1, forLoopCondition    # second while condition (modified)

    sw $t1, 0($t0)            # a[j] = a[j-1]
    addi $t2, $t2, -1        # j--
    j while
    
forLoopCondition:
    sll $t1, $t2, 2
    add $t1, $t1, $a0
    sw $t4, 0($t1)            # a[j] = tmp
    addi $t3, $t3, 1        # i++
    bge $t3, $t5, end        # for loop condition
    j forLoop

end: jr $ra

print_array:
    addi $sp, $sp, -4   # push
    sw $ra, 0($sp)      # ret addr on stack
    la $t0, array       # t0 points to array
    la $t1, endarr      # t1 points to array end
    la $t3, space       # t3 points to space string
print_loop:
    lw $t2, 0($t0)      # get array element
    addi $t0, $t0, 4    # point to next
    addi $a2, $a2, -4   # decrement array size
    add $a0, $0, $t2    # copy array element into $a0
    addi $v0, $0, PR_INT    # print $v0
    syscall

    bne $t0, $t1, print_space # jump to print space if not last element
    lw $ra, 0($sp)      # pop
    addi $sp, $sp, 4    # ret addr
    jr $ra

print_space:
    addi $v0, $0, PR_STR     # print space
    la $a0, space
    syscall
    j print_loop

