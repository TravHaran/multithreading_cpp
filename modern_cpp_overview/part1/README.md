## Modern C++ Overview Part One

### Universal Initialization
- initializer(s) within a pair of braces
- can be used with any type
    ```
    int x{7};           //Equivalent to int x = 7;
    std::string str{"Let us begin"};        //Equivalent to std::string str("Let us begin");
    ```
- narrowing conversions are not allowed
    ```
    int x = 7.7;        // Legal although compilers may warn
    int x{7.7};         // Illegal
    ```
- it can be used with compound types
    ```
    std::vector<int> vec{4, 2, 3, 5, 1};        //std::vector variable with elements 4, 2, 3, 5, 1
    ```

