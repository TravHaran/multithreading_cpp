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

### NULL
- has the value 0
- its type is implementation defined
    ```
    //Two functions which are overloaded
    void func(int);
    void func(int*);

    func(NULL);         //Calls func(int*) with clang
                        //Calls func(int) with VC++
                        //Does not compile with gcc
    ``` 

### std::chrono Durations
- types which represent time intervals
    - defined in <chrono>
    - in the std::chrono namespace
        ```
        //Namespace alias to simplify the code
        namespace sc = std::chrono;

        sc::seconds         //1 second
        sc::milliseconds    //1/1000 second
        sc::microseconds    //1/1000,000 second

        sc::seconds(2);         //2 second interval
        sc::milliseconds(20);   //20 millisecond interval
        sc::microseconds(50);   //50 microsecond interval
        ```

### The auto Type Specifier
- the compiler deduces the type from the initializer
    ```
    auto x = 6;         //Equivalent to int x = 6;
    auto x{6};          //Equivalent to int x{6};
    ```
- this is very useful with complicated types
    ```
    std::vector<std::string> vec;

    //Equivalent to std::vector<std::string>::iterator it = vec.begin();
    auto it = vec.begin();
    ```
- in modern C++, there are some cases where the type cannot be known by the programmer

### auto Specifier and Qualifiers
- auto will only give the underlying type
    ```
    auto x = 6;             // x deduced as non-const
    ```
- const, reference, etc are ignored
    ```
    const std::string& str = "Hello";       //Reference to const
    ...
    auto hello = str;                   //hello has type std::string
                                        //it is a mutable copy of str
    ```
- if we need them we must add them ourselves
    ```
    const auto& str = hello;            //hello is a const reference to std::string
    ```

### auto Specifier and for Loops
- we can use auto to simplify loops
    ```
    std::vector<int> vec;
    ...
    for(auto it = vec.begin(); it != vec.end(); ++it)
        std::cout<<*it<<",";        //Prints out each element of v
    
    for(auto it = vec.begin(); it != vec.end(); ++it)
        *it += 2;           // Add 2 to each element of v
    ```

### Range for loops
- special syntax for iterating over containers
    ```
    for(auto i : vec)
        std::cout<<i<<",";          //Prints out each element of v
    
    //We need to use a reference to modify the elements
    for(auto& i : vec)
        i += 2;                     // Add 2 to each element of v
    ```
- to visit each element once, in order, without adding or removing elements
- otherwise use a traditional loop



