#boost_1_75_0 C++ Library Installation Notes

Link: [https://www.boost.org/](https://www.boost.org/)  

## Download and Extract

```
ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool$ mv ~/Downloads/boost_1_75_0.tar.gz .
ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool$ tar -xzvf ./boost_1_75_0.tar.gz 
```

## Installation 

Run bootstrap.sh  
```
ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/boost_1_75_0$ ./bootstrap.sh 
```

Run ./b2  
```
ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/boost_1_75_0$ sudo ./b2 install
```

## Testing with example.cpp

```
ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/boost_1_75_0$ vi ./example.cpp
ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/boost_1_75_0$ cat ./example.cpp
#include <boost/lambda/lambda.hpp>
#include <iostream>
#include <iterator>
#include <algorithm>

int main()
{
    using namespace boost::lambda;
    typedef std::istream_iterator<int> in;

    std::for_each(
        in(std::cin), in(), std::cout << (_1 * 3) << " " );
}
ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/boost_1_75_0$
```

Compile and test ...  
```
ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/boost_1_75_0$ g++ -I /home/ye/tool/boost_1_75_0/ ./example.cpp -o example
ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/boost_1_75_0$ echo 1 2 3 | ./example 
3 6 9 
```
