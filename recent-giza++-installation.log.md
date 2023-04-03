# GIZA++ Installation Log on Server

I installed this GIZA++ on CADT Server for alignment tutorial to my ITC students.  

## git clone

(base) rnd@gpu:~/tool$ git clone https://github.com/moses-smt/giza-pp
Cloning into 'giza-pp'...
remote: Enumerating objects: 328, done.
remote: Counting objects: 100% (27/27), done.
remote: Compressing objects: 100% (24/24), done.
remote: Total 328 (delta 5), reused 9 (delta 3), pack-reused 301
Receiving objects: 100% (328/328), 314.48 KiB | 498.00 KiB/s, done.
Resolving deltas: 100% (212/212), done.
(base) rnd@gpu:~/tool$ cd giza-pp/

## Check the folder

(base) rnd@gpu:~/tool/giza-pp$ ls
GIZA++-v2  Makefile  README  mkcls-v2

## run make

(base) rnd@gpu:~/tool/giza-pp$ time make | tee make.log
make -C GIZA++-v2
make[1]: Entering directory '/home/rnd/tool/giza-pp/GIZA++-v2'
mkdir optimized/
g++   -Wall -Wno-parentheses -O3 -funroll-loops -DNDEBUG -DWORDINDEX_WITH_4_BYTE -DBINARY_SEARCH_FOR_TTABLE  -c Parameter.cpp -o optimized/Parameter.o
Parameter.cpp: In function ‘bool writeParameters(std::ofstream&, const ParSet&, int)’:
Parameter.cpp:48:14: warning: ignoring return value of ‘char* getcwd(char*, size_t)’, declared with attribute warn_unused_result [-Wunused-result]
        getcwd(path,1024);
        ~~~~~~^~~~~~~~~~~
g++   -Wall -Wno-parentheses -O3 -funroll-loops -DNDEBUG -DWORDINDEX_WITH_4_BYTE -DBINARY_SEARCH_FOR_TTABLE  -c myassert.cpp -o optimized/myassert.o
...
...
...
g++ -Wall -W -DNDEBUG -O3 -funroll-loops -c KategProblemTest.cpp -o KategProblemTest.o
g++ -Wall -W -DNDEBUG -O3 -funroll-loops -c KategProblemKBC.cpp -o KategProblemKBC.o
g++ -Wall -W -DNDEBUG -O3 -funroll-loops -c KategProblemWBC.cpp -o KategProblemWBC.o
g++ -Wall -W -DNDEBUG -O3 -funroll-loops -c KategProblem.cpp -o KategProblem.o
g++ -Wall -W -DNDEBUG -O3 -funroll-loops -c StatVar.cpp -o StatVar.o
g++ -Wall -W -DNDEBUG -O3 -funroll-loops -c general.cpp -o general.o
g++ -Wall -W -DNDEBUG -O3 -funroll-loops -c mkcls.cpp -o mkcls.o
g++ -Wall -W -DNDEBUG -O3 -funroll-loops -o mkcls GDAOptimization.o HCOptimization.o Problem.o IterOptimization.o ProblemTest.o RRTOptimization.o MYOptimization.o SAOptimization.o TAOptimization.o Optimization.o KategProblemTest.o KategProblemKBC.o KategProblemWBC.o KategProblem.o StatVar.o general.o mkcls.o 
make[1]: Leaving directory '/home/rnd/tool/giza-pp/mkcls-v2'

real	0m47.004s
user	0m43.957s
sys	0m2.659s
