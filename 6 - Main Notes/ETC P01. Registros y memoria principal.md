2025-09-17 18:58

Status: #baby #lectures

Tags:

# ETC P01. Registros y memoria principal

Las instruccciones de lectura y escritura se escriben de la forma `op rt,desp(rs)`

```assembly
          .globl __start
          .text 0x00400000
__start:  li $t0, 25            # guardamos 25 en el registro t0
          li $t1, 30            # guardamos 30 en el registro t1
          add $s0, $t1, $t0     # guardamos la suma en s0
          add $s0, $s0, $s0     # s0 = s0 + s0 = 2 * (25 + 30)
```


## References

[[ETC Tema 1.3 El procesador]], [[ETC Concepts]]