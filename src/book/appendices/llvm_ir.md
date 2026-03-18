 A set of llvm's internals illustrating their usages and syntax.
 
 Categories
 - Attributes
 - linkages
 - Terminator instructions
 - Metadata
 - Debug Information
 
 
 ### Terminator instructions
 
 The terminator instructions are: ‘ret’, ‘br’, ‘switch’, ‘indirectbr’, ‘invoke’, ‘callbr’ ‘resume’, ‘catchswitch’, ‘catchret’, ‘cleanupret’, and ‘unreachable’.
 
  - `ret`
    return a value from a function.
    
    _syntax
    ```text
      ret <type> <value>
    ```
  
    _use-cases
    ```llvm-ir
      ret void
      ret i64 %_0
      ret i32 0
      ret { i32, i8 } { i32 4, i8 2 } ; a struct with fields of i32 and i8
    ```
    The return type must be of a first class type so basically it must be of the primitive types `i8`,`i32`,`i32`,`float` etc. If it is an aggregate type like a struct of some sort it must be delineated to illustrate the individual types within the aggregate type.
  - `br`
    branch conditionally or unconditionally from a block.
  
    _syntax
    ```text
      ;conditional branch
      br i1 <cond>, label <iftrue>, label <iffalse>
      
      ; unconditional branch
      br label %block
    ```
  
    _use-cases
    ```llvm-ir
      br label %bb14
      br i1 %_2, label %bb2, label %bb3
    ```
  - `switch`
    _syntax
    ```text
      switch <intty> <value>, label <defaultdest> [ <intty> <val>, label <dest> ... ]
    ```
  
    _use-cases
  ```llvm-ir
  switch i64 %_2, label %bb1 [
      i64 0, label %bb5
      i64 1, label %bb4
      i64 2, label %bb3
      i64 3, label %bb2
    ]
  ```
  From the langref :- "Depending on properties of the target machine and the particular switch instruction, this instruction may be code generated in different ways. For example, it could be generated as a series of chained conditional branches or with a lookup table."
  
  ### Linkages 
  
  These appear to be information being passed to the linker.
