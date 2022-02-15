# Rakudo Installation and Testing

Raku language (i.e. perl 6) ကို compile လုပ်ပေးတာက Rakudo ပါ။  
Raku language နဲ့ Rakudo ကို program တစ်ပုဒ် စမ်းရေးဖို့အတွက် လေ့လာခဲ့စဉ်က မှတ်သားခဲ့တဲ့ note ဖိုင်ပါ။  

y  
14 Feb 2022   

## Installation

```
(base) ye@:/media/ye/project2/exp$ sudo apt install rakudo
[sudo] password for ye: 
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following packages were automatically installed and are no longer required:
  apturl-common gir1.2-goa-1.0 ibverbs-providers libboost-atomic-dev libboost-atomic1.71-dev libboost-atomic1.71.0 libboost-chrono-dev
  libboost-chrono1.71-dev libboost-chrono1.71.0 libboost-container-dev libboost-container1.71-dev libboost-container1.71.0 libboost-context-dev
  libboost-context1.71-dev libboost-context1.71.0 libboost-coroutine-dev libboost-coroutine1.71-dev libboost-coroutine1.71.0 libboost-date-time-dev
  libboost-date-time1.71-dev libboost-dev libboost-exception-dev libboost-exception1.71-dev libboost-fiber-dev libboost-fiber1.71-dev
  libboost-fiber1.71.0 libboost-filesystem-dev libboost-filesystem1.71-dev libboost-graph-parallel-dev libboost-graph-parallel1.71-dev
  libboost-graph-parallel1.71.0 libboost-graph1.71.0 libboost-locale-dev libboost-locale1.71-dev libboost-log1.71.0 libboost-math-dev
  libboost-math1.71-dev libboost-math1.71.0 libboost-mpi-dev libboost-mpi-python-dev libboost-mpi-python1.71-dev libboost-mpi-python1.71.0
  libboost-mpi1.71-dev libboost-mpi1.71.0 libboost-numpy-dev libboost-numpy1.71-dev libboost-numpy1.71.0 libboost-program-options-dev
  libboost-program-options1.71-dev libboost-program-options1.71.0 libboost-python-dev libboost-python1.71-dev libboost-python1.71.0
  libboost-random-dev libboost-random1.71-dev libboost-random1.71.0 libboost-regex1.71.0 libboost-serialization-dev libboost-serialization1.71-dev
  libboost-serialization1.71.0 libboost-stacktrace-dev libboost-stacktrace1.71-dev libboost-stacktrace1.71.0 libboost-system-dev
  libboost-system1.71-dev libboost-system1.71.0 libboost-test-dev libboost-test1.71-dev libboost-test1.71.0 libboost-thread-dev
  libboost-thread1.71-dev libboost-timer-dev libboost-timer1.71-dev libboost-timer1.71.0 libboost-tools-dev libboost-type-erasure-dev
  libboost-type-erasure1.71-dev libboost-type-erasure1.71.0 libboost-wave-dev libboost-wave1.71-dev libboost-wave1.71.0 libboost1.71-dev
  libboost1.71-tools-dev libcaf-openmpi-3 libcoarrays-openmpi-dev libevent-core-2.1-7 libevent-dev libevent-extra-2.1-7 libevent-openssl-2.1-7
  libevent-pthreads-2.1-7 libfabric1 libhwloc-dev libhwloc-plugins libhwloc15 libibverbs-dev libibverbs1 libnl-3-dev libnl-route-3-dev libnuma-dev
  libopenmpi-dev libopenmpi3 libpmix2 libpsm-infinipath1 libpsm2-2 librdmacm1 mpi-default-bin mpi-default-dev openmpi-bin openmpi-common python3-click
  python3-colorama python3-software-properties software-properties-common unattended-upgrades
Use 'sudo apt autoremove' to remove them.
The following additional packages will be installed:
  fonts-glyphicons-halflings libffi7 libgraph-perl libjs-angularjs libjs-bootstrap libpath-tiny-perl libtommath1 libunicode-utf8-perl moarvm nqp
Suggested packages:
  valgrind
The following NEW packages will be installed:
  fonts-glyphicons-halflings libffi7 libgraph-perl libjs-angularjs libjs-bootstrap libpath-tiny-perl libtommath1 libunicode-utf8-perl moarvm nqp
  rakudo
0 upgraded, 11 newly installed, 0 to remove and 103 not upgraded.
Need to get 6,602 kB of archives.
After this operation, 47.4 MB of additional disk space will be used.
Do you want to continue? [Y/n] Y
Get:1 http://archive.ubuntu.com/ubuntu focal/main amd64 libffi7 amd64 3.3-4 [19.7 kB]
Get:2 http://archive.ubuntu.com/ubuntu focal/universe amd64 fonts-glyphicons-halflings all 1.009~3.4.1+dfsg-1 [117 kB]
Get:3 http://archive.ubuntu.com/ubuntu focal/universe amd64 libgraph-perl all 1:0.9704-1 [109 kB]
Get:4 http://archive.ubuntu.com/ubuntu focal/universe amd64 libjs-angularjs all 1.7.9-1 [551 kB]
Get:5 http://archive.ubuntu.com/ubuntu focal/universe amd64 libjs-bootstrap all 3.4.1+dfsg-1 [124 kB]
Get:6 http://archive.ubuntu.com/ubuntu focal/main amd64 libpath-tiny-perl all 0.108-1 [42.6 kB]
Get:7 http://archive.ubuntu.com/ubuntu focal/main amd64 libtommath1 amd64 1.2.0-3 [53.0 kB]
Get:8 http://archive.ubuntu.com/ubuntu focal/main amd64 libunicode-utf8-perl amd64 0.62-1build1 [18.1 kB]
Get:9 http://archive.ubuntu.com/ubuntu focal/universe amd64 moarvm amd64 2019.11+dfsg-2build2 [1,225 kB]
Get:10 http://archive.ubuntu.com/ubuntu focal/universe amd64 nqp amd64 2019.11+dfsg-2 [584 kB]
Get:11 http://archive.ubuntu.com/ubuntu focal/universe amd64 rakudo amd64 2019.11-4 [3,759 kB]
Fetched 6,602 kB in 2s (2,646 kB/s)
Selecting previously unselected package libffi7:amd64.
(Reading database ... 665642 files and directories currently installed.)
Preparing to unpack .../00-libffi7_3.3-4_amd64.deb ...
Unpacking libffi7:amd64 (3.3-4) ...
Selecting previously unselected package fonts-glyphicons-halflings.
Preparing to unpack .../01-fonts-glyphicons-halflings_1.009~3.4.1+dfsg-1_all.deb ...
Unpacking fonts-glyphicons-halflings (1.009~3.4.1+dfsg-1) ...
Selecting previously unselected package libgraph-perl.
Preparing to unpack .../02-libgraph-perl_1%3a0.9704-1_all.deb ...
Unpacking libgraph-perl (1:0.9704-1) ...
Selecting previously unselected package libjs-angularjs.
Preparing to unpack .../03-libjs-angularjs_1.7.9-1_all.deb ...
Unpacking libjs-angularjs (1.7.9-1) ...
Selecting previously unselected package libjs-bootstrap.
Preparing to unpack .../04-libjs-bootstrap_3.4.1+dfsg-1_all.deb ...
Unpacking libjs-bootstrap (3.4.1+dfsg-1) ...
Selecting previously unselected package libpath-tiny-perl.
Preparing to unpack .../05-libpath-tiny-perl_0.108-1_all.deb ...
Unpacking libpath-tiny-perl (0.108-1) ...
Selecting previously unselected package libtommath1:amd64.
Preparing to unpack .../06-libtommath1_1.2.0-3_amd64.deb ...
Unpacking libtommath1:amd64 (1.2.0-3) ...
Selecting previously unselected package libunicode-utf8-perl.
Preparing to unpack .../07-libunicode-utf8-perl_0.62-1build1_amd64.deb ...
Unpacking libunicode-utf8-perl (0.62-1build1) ...
Selecting previously unselected package moarvm.
Preparing to unpack .../08-moarvm_2019.11+dfsg-2build2_amd64.deb ...
Unpacking moarvm (2019.11+dfsg-2build2) ...
Selecting previously unselected package nqp.
Preparing to unpack .../09-nqp_2019.11+dfsg-2_amd64.deb ...
Unpacking nqp (2019.11+dfsg-2) ...
Selecting previously unselected package rakudo.
Preparing to unpack .../10-rakudo_2019.11-4_amd64.deb ...
Unpacking rakudo (2019.11-4) ...
Setting up libunicode-utf8-perl (0.62-1build1) ...
Setting up libtommath1:amd64 (1.2.0-3) ...
Setting up fonts-glyphicons-halflings (1.009~3.4.1+dfsg-1) ...
Setting up libffi7:amd64 (3.3-4) ...
Setting up libgraph-perl (1:0.9704-1) ...
Setting up libjs-angularjs (1.7.9-1) ...
Setting up libpath-tiny-perl (0.108-1) ...
Setting up moarvm (2019.11+dfsg-2build2) ...
Setting up libjs-bootstrap (3.4.1+dfsg-1) ...
Setting up nqp (2019.11+dfsg-2) ...
Setting up rakudo (2019.11-4) ...
  rakudo-helper.pl: Reinstalling all perl6 modules ...
Processing triggers for fontconfig (2.13.1-2ubuntu3) ...
Processing triggers for libc-bin (2.32-0ubuntu3) ...
/sbin/ldconfig.real: /usr/local/lib/libnatools.so.0 is not a symbolic link

/sbin/ldconfig.real: /usr/local/lib/liblouis.so.20 is not a symbolic link

/sbin/ldconfig.real: /usr/local/lib/libsqlite3.so.0 is not a symbolic link

Processing triggers for man-db (2.9.3-2) ...
(base) ye@:/media/ye/project2/exp$ rakudo --version
This is Rakudo version 2019.11 built on MoarVM version 2019.11
implementing Perl 6.d.
(base) ye@:/media/ye/project2/exp$
```

## Testing Rakudo

```
(base) ye@:/media/ye/project2/exp/brain-fuck/rakudo$ cat ./brainfuck.p6 
use v6;

use MONKEY-SEE-NO-EVAL;  # we need to parse user input

my $hello-bf = "
++++++++++    initializes cell zero to 10
[
   >+++++++>++++++++++>+++>+<<<<-
]             loop sets the next four cells to 70/100/30/10
>++.          print   'H'
>+.           print   'e'
+++++++.              'l'
.                     'l'
+++.                  'o'
>++.                  space
<<+++++++++++++++.    'W'
>.                    'o'
+++.                  'r'
------.               'l'
--------.             'd'
>+.                   '!'
>.                    newline
";

sub MAIN($input = "") {
    # Read the program.
    my $program = $input eq "" ?? $hello-bf !! $input.IO.slurp;

    # Compile to Perl 6.
    $program .= subst(/ <-[+\-<>,.\[\]]> /, '', :g);
    $program .= subst(/(\++)/, { 'P += ' ~ $0.chars ~ ";" }, :g);
    $program .= subst(/(\-+)/, { 'P -= ' ~ $0.chars ~ ";" }, :g);
    $program .= subst(/(\>+)/, { '$ptr += ' ~ $0.chars ~ ";" }, :g);
    $program .= subst(/(\<+)/, { '$ptr -= ' ~ $0.chars ~ ";" }, :g);
    $program .= subst(/\./, "print chr P;", :g);
    $program .= subst(/\,/, "P = ord getc;", :g);
    $program .= subst(/\[/, 'while (P) {', :g);
    $program .= subst(/\]/, '};', :g);
    $program .= subst(/P/, '@P[$ptr]', :g);
    $program  = 'my @P = (); my $ptr = 0;' ~ $program;

    # Run
    EVAL $program;
}
(base) ye@:/media/ye/project2/exp/brain-fuck/rakudo$
```

```
(base) ye@:/media/ye/project2/exp/brain-fuck/rakudo$ rakudo ./brainfuck.p6 ./ykt.bf 
ykt(base) ye@:/media/ye/project2/exp/brain-fuck/rakudo$
```

```
(base) ye@:/media/ye/project2/exp/brain-fuck/rakudo$ cat ilovelang.p6 
grammar Parser {
    rule  TOP  { I <love> <lang> }
    token love { '♥' | love }
    token lang { < Raku Perl Rust Go Python Ruby > }
}

say Parser.parse: 'I ♥ Raku';
# OUTPUT: ｢I ♥ Raku｣ love => ｢♥｣ lang => ｢Raku｣

say Parser.parse: 'I love Perl';
# OUTPUT: ｢I love Perl｣ love => ｢love｣ lang => ｢Perl｣
(base) ye@:/media/ye/project2/exp/brain-fuck/rakudo$
```

```
(base) ye@:/media/ye/project2/exp/brain-fuck/rakudo$ rakudo ./ilovelang.p6 
｢I ♥ Raku｣
 love => ｢♥｣
 lang => ｢Raku｣
｢I love Perl｣
 love => ｢love｣
 lang => ｢Perl｣
(base) ye@:/media/ye/project2/exp/brain-fuck/rakudo$ 
```

### Separating as Class 

```
(base) ye@:/media/ye/project2/exp/brain-fuck/rakudo$ cat ./demo-class.p6 

# no separation for lexer and paser in perl6, write both in a single grammar

my $prog = "var x = 20; print x;
var y = 42; print y;";
my %var;

grammar G {
	rule TOP {
		<statement>* %% ';'
	}
	
	rule statement {
		| <variable-declaration>
		| <function-call>
	}
	
	rule variable-declaration {
		'var' <variable-name> '=' <number> 
	}
	
	token variable-name {
		\w+
	}
	
	token number {
		\d+
	}
	
	rule function-call {
		'print' <variable-name> 
	}
}	
	class A {
		method variable-declaration($/) {
			%var{$<variable-name>} = +$<number>;
		}
		method function-call($/) {
			say %var{$<variable-name>};
		}
	}



say G.parse($prog, :actions(A));
dd %var;
(base) ye@:/media/ye/project2/exp/brain-fuck/rakudo$ 
```

running ...  

```
(base) ye@:/media/ye/project2/exp/brain-fuck/rakudo$ rakudo  ./demo-class.p6 
20
42
｢var x = 20; print x;
var y = 42; print y;｣
 statement => ｢var x = 20｣
  variable-declaration => ｢var x = 20｣
   variable-name => ｢x｣
   number => ｢20｣
 statement => ｢print x｣
  function-call => ｢print x｣
   variable-name => ｢x｣
 statement => ｢var y = 42｣
  variable-declaration => ｢var y = 42｣
   variable-name => ｢y｣
   number => ｢42｣
 statement => ｢print y｣
  function-call => ｢print y｣
   variable-name => ｢y｣
Hash %var = {:x(20), :y(42)}
(base) ye@:/media/ye/project2/exp/brain-fuck/rakudo$
```


## Writing a Small Compiler

Ref:https://www.youtube.com/watch?v=lwIXF25KJCo  

```
(base) ye@:/media/ye/project2/exp/brain-fuck/rakudo$ cat ./demo.p6 

# no separation for lexer and paser in perl6, write both in a single grammar

my $prog = "var x = 20; print x;
var y = 42; print y;";
my %var;

grammar G {
	rule TOP {
		<statement>* %% ';'
	}
	
	rule statement {
		| <variable-declaration>
		| <function-call>
	}
	
	rule variable-declaration {
		'var' <variable-name> '=' <number> {
			%var{$<variable-name>} = +$<number>;
		}
	}
	
	token variable-name {
		\w+
	}
	
	token number {
		\d+
	}
	
	rule function-call {
		'print' <variable-name> {
			say %var{$<variable-name>};
		}
	}
}


say G.parse($prog);
dd %var;
```

```
(base) ye@:/media/ye/project2/exp/brain-fuck/rakudo$ rakudo  ./demo.p6
20
42
｢var x = 20; print x;
var y = 42; print y;｣
 statement => ｢var x = 20｣
  variable-declaration => ｢var x = 20｣
   variable-name => ｢x｣
   number => ｢20｣
 statement => ｢print x｣
  function-call => ｢print x｣
   variable-name => ｢x｣
 statement => ｢var y = 42｣
  variable-declaration => ｢var y = 42｣
   variable-name => ｢y｣
   number => ｢42｣
 statement => ｢print y｣
  function-call => ｢print y｣
   variable-name => ｢y｣
Hash %var = {:x(20), :y(42)}
(base) ye@:/media/ye/project2/exp/brain-fuck/rakudo$
```

## Notes

```
use Grammar::Common;
# / ^ <number> \s+ <number> \s+ ... /;
my rule line { <number> <number> ... };
```

```
grammar MLCad does Grammar::Common {
	rule TOP { <x=number> <y=number> }
}

MLCad.parse('10 20');
say $/<x>;
10
```

```
class Interpreter does
 Grammar::Common::Interpreter {
 	method expression( $/ ) {
 		make $/<expression>.ast;
 	}
 }
 MLCad.parse('10 20 (2*7)+1 "Red"',
 	:actions(Interpreter.new));
 	say $/{'z'};
 	10.428571
```

```
infix: A + B
prefix: -A
postfix: A++
circumfix: [A]
post-circumfix: A[B]
Unary operators take 1 argument
Binary operators take 2 argument
Infix operators also have a noun form, &[+]

say &[+]{1,2}

Subs that take two args can be used as infix binary operators

sub plus-twice($a,$b) { $a + 2 * $b }
say 1 {&plus-twice} 2

----------
sub infix:<plus>($x,$y) {
	$x + $y
}
say 1 plus 2;
-----------

sub prefix:<@@>($x) { $x * 2 }
sub postfix:<+++>($y is rw) { $y+=3 }

my $z = @@10;
$z+++;
say $z;

အထက်ပါ လိုမျိုးအပြင် unicode math symbol တွေကိုပါ သုံးလို့ ရတယ်။ custom operator တွေ လုပ်ပြီး သုံးလို့ ရတယ်။ 

# dot product
sub infix:<.>(@a,@b) {
	return [+] @a z* @b
}
say (1,2) . (3,4)
```


```
sub infix:<plus>($x, $y) {
	$x + $y
}
sub infix:<times>($x,$y) {
	$x + $y
}
say 1 plus 2 times 3;

လိုချင်တဲ့ အဖြေမရဘူး။
---------

အမြှောက် ဖြစ်တဲ့ times ကို tight လုပ်ပေးလိုက်တာ
is tighter controls precedence
အရမ်းအဆင်ပြေပါတယ်
sub infix:<plus>($x, $y) {
	$x + $y
}
sub infix:<times>($x,$y) is tighter (&infix:<plus>){
	$x + $y
}
say 1 plus 2 times 3;

Also is looser, "is equiv "
အထက်မှာ plus က looser အနေနဲ့ ထားထားတာပေါ့

question တက်လာတယ်။ non-transitive precedence နဲ့ ပတ်သက်ပြီးတော့... 

------------
```

```
chaining operators
sub infix:<to-the-power>($x, $y) {
	$x ** $y
}
say 2 to-the-poser 3 to-the-power 2
အဖြေ 64 ရမယ်။
လွဲနေတယ် အဲဒါကြောင့် အောက်ပါအတိုင်း ပြောင်းရေးရတယ်

associativity
we can fix this. is assoc!
sub infix:<to-the-power>($x,$y) is assoc<right> {
	$x ** $y
}
say 2 to-the-power 3 to-the-power 2
အဖြေက 512 ရပြီ

associativity အမျိုးအစားတွေ အမျိုးမျိုး ရှိတယ်
Associativity types:
right, left, non, chain (1 < 2 < 3)
list(1, 2 X 3, 4 X 5, 6)
```

```
argument types

define subtraction between strings

sub infix:<->($x,$y) {
	$x.subst($y, "", :g);
}
say "house" - "u";
အဖြေက "hose" ဆိုပြီး ရမယ်။

But 
say 32-2
3 ဆိုရင်တော့ မဟုတ်သေးဘူးလေ...  
```

```
multiple dispatch

We can fix this, too.

multi infix:<->(Str $x, Str $y) {
	$x.subst($y, "", :g);
}
say "house" - "u";
say 32 - 3;

အဖြေက hose နဲ့ 29

```

```
multiple dispatch

Also works for strings, ints, constants, or any class.

multi sub infix:<->(Str $x, Str $y) {
	$x.subst($y, "", :g);
}
multi sub infix:<->(Str $x, Int $y) {
	"stairs"
}
say "catamaran" - "a";
say "catamaran" - 6;
say "escalator" - "electricity";
say 10 - 5;

အဖြေက အောက်ပါအတိုင်းရမယ်။
ctmrn
cat
staris
5
```

```
example

emulate python % operator

multi sub infix:<%>(Str $f, Numeric $n) {
	return sprintf($f,$n)
}
multi sub infix:<%>(Str $f,List $1) {
	return sprintf($f,$1.flat)
}
say 'This is %d.' % 40;
say 'Pi is about %0.2f and e is about %0.2f' % (π, e);

```

```
DBIx::Class, Rose::DB::Object, SQL::Abstract
SQLAlchemy, Squeel
Typical techniques:
- method chaining
- operator overloading
- data structure abuse

perl 6 operators add new techniques:
SELECT id
FROM user INNER JOIN address ON address.user=user.id
WHERE name = 'ed' and fullname='Ed Jones'

(User + Address)[ name == 'ed' and fullname == 'Ed Jones' ]

- native operators and, == can be defined for columns
- post-circumfix [ ] can be used to filter

အောက်ပါလိုမျိုး လုပ်လို့ ရတယ်

class Table { ... }
multi sub infix:<+>(Table $a, Table $b) {
...
}

```

အလားတူပါပဲ...  
```
class Filter { ... }
class Column { ... }
multi sub infix:<==>(column  $1, $b) {
	...
	return Filter.{ ... }
}
multi sub infix:<and>(Filter $a, Filter $b) {
	...
	return Filter.new( ... )
}
	
```

## External IDSLs or Grammars

```
parsing Slim
- a grammar is a collection of regexes (like a class + method)
- a token is a regex with no backtracking
a rule is a regex with significant whitespace


grammar slim{
	rule TOP < <line>+ %% <eol>}
	token line { <indentation} <tag> [ ' ' <text> ]? }
	token indentation { <indent>* }
	token indent { '	' }
	token tag { \w+ }
	token text { \v+ }
	token eol { \n+ }
}
say slim.parse(q:to/DONE/);
html
	head
		title Slim Examples
	body
		h1 Markup Examples
DONE

ဒီနေရာမှာ X %% Y means [ X ][ Y X ]*
```

Slangs ဆိုတာက structure way to modify the grammar ...  

The language braid

- Immutable versions are stored in $~MAIN, $~Quote, etc
- Available even at run time

```
for $-MAIN, $-Quote, $-P5Regex, $-Regex {
	say .grammar.^name;
	say .actions.^name;
}
```

to see examples, use --target=parse:
```
perl6 --target=parse -e "say 'hello, world'"
```

ကိုယ့်စက်ထဲမှာ လုပ်ကြည့်ခဲ့...  

```
(base) ye@:/media/ye/project2/exp/brain-fuck/rakudo$ perl6 --target=parse -e "say 'hello, world'"
- statementlist: say 'hello, world'
  - statement: 1 matches
    - EXPR: say 'hello, world'
      - longname: say
        - colonpair:  isa NQPArray
        - name: say
          - morename:  isa NQPArray
          - identifier: say
      - args:  'hello, world'
        - arglist: 'hello, world'
          - EXPR: 'hello, world'
            - value: 'hello, world'
              - quote: 'hello, world'
                - nibble: hello, world
- lang-version: 
(base) ye@:/media/ye/project2/exp/brain-fuck/rakudo$
```

စမ်းထားတဲ့ demo program က  

```
(base) ye@:/media/ye/project2/exp/brain-fuck/rakudo$ cat ./demo-class.p6

# no separation for lexer and paser in perl6, write both in a single grammar

my $prog = "var x = 20; print x;
var y = 42; print y;";
my %var;

grammar G {
	rule TOP {
		<statement>* %% ';'
	}
	
	rule statement {
		| <variable-declaration>
		| <function-call>
	}
	
	rule variable-declaration {
		'var' <variable-name> '=' <number> 
	}
	
	token variable-name {
		\w+
	}
	
	token number {
		\d+
	}
	
	rule function-call {
		'print' <variable-name> 
	}
}	
	class A {
		method variable-declaration($/) {
			%var{$<variable-name>} = +$<number>;
		}
		method function-call($/) {
			say %var{$<variable-name>};
		}
	}



say G.parse($prog, :actions(A));
dd %var;
(base) ye@:/media/ye/project2/exp/brain-fuck/rakudo$
```

tree ထုတ်ကြည့်ရင် အရှည့်ကြီးရလိမ့်မယ်။ အောက်ပါအတိုင်း....  

```
(base) ye@:/media/ye/project2/exp/brain-fuck/rakudo$ rakudo --target=parse ./demo-class.p6 
- statementlist: my $prog = "var x = 20; print x;
var y = 42; print y;";
my %var;

grammar G {
	rule TOP {
		<statement>* %% ';'
	}
	
	rule statement {
		| <variable-declaration>
		| <function-call>
	}
	
	rule variable-declaration {
		'var' <variable-name> '=' <number> 
	}
	
	token variable-name {
		\w+
	}
	
	token number {
		\d+
	}
	
	rule function-call {
		'print' <variable-name> 
	}
}	
	class A {
		method variable-declaration($/) {
			%var{$<variable-name>} = +$<number>;
		}
		method function-call($/) {
			say %var{$<variable-name>};
		}
	}



say G.parse($prog, :actions(A));
dd %var;

  - statement: 6 matches
    - EXPR: my $prog = "var x = 20; print x;
var y = 42; print y;"
      - scope_declarator: my $prog = "var x = 20; print x;
var y = 42; print y;"
        - scoped:  $prog = "var x = 20; print x;
var y = 42; print y;"
          - declarator: $prog = "var x = 20; print x;
var y = 42; print y;"
            - trait:  isa NQPArray
            - initializer: = "var x = 20; print x;
var y = 42; print y;"
              - sym: =
              - EXPR: "var x = 20; print x;
var y = 42; print y;"
                - value: "var x = 20; print x;
var y = 42; print y;"
                  - quote: "var x = 20; print x;
var y = 42; print y;"
                    - nibble: var x = 20; print x;
var y = 42; print y;
            - variable_declarator: $prog
              - signature:  isa NQPArray
              - post_constraint:  isa NQPArray
              - variable: $prog
                - desigilname: prog
                  - longname: prog
                    - colonpair:  isa NQPArray
                    - name: prog
                      - identifier: prog
                      - morename:  isa NQPArray
                - sigil: $
              - semilist:  isa NQPArray
              - postcircumfix:  isa NQPArray
              - trait:  isa NQPArray
          - DECL: $prog = "var x = 20; print x;
var y = 42; print y;"
            - trait:  isa NQPArray
            - initializer: = "var x = 20; print x;
var y = 42; print y;"
              - sym: =
              - EXPR: "var x = 20; print x;
var y = 42; print y;"
                - value: "var x = 20; print x;
var y = 42; print y;"
                  - quote: "var x = 20; print x;
var y = 42; print y;"
                    - nibble: var x = 20; print x;
var y = 42; print y;
            - variable_declarator: $prog
              - signature:  isa NQPArray
              - post_constraint:  isa NQPArray
              - variable: $prog
                - desigilname: prog
                  - longname: prog
                    - colonpair:  isa NQPArray
                    - name: prog
                      - identifier: prog
                      - morename:  isa NQPArray
                - sigil: $
              - semilist:  isa NQPArray
              - postcircumfix:  isa NQPArray
              - trait:  isa NQPArray
          - typename:  isa NQPArray
        - sym: my
    - EXPR: my %var
      - scope_declarator: my %var
        - scoped:  %var
          - typename:  isa NQPArray
          - DECL: %var
            - trait:  isa NQPArray
            - variable_declarator: %var
              - postcircumfix:  isa NQPArray
              - trait:  isa NQPArray
              - post_constraint:  isa NQPArray
              - signature:  isa NQPArray
              - semilist:  isa NQPArray
              - variable: %var
                - sigil: %
                - desigilname: var
                  - longname: var
                    - colonpair:  isa NQPArray
                    - name: var
                      - identifier: var
                      - morename:  isa NQPArray
          - declarator: %var
            - trait:  isa NQPArray
            - variable_declarator: %var
              - postcircumfix:  isa NQPArray
              - trait:  isa NQPArray
              - post_constraint:  isa NQPArray
              - signature:  isa NQPArray
              - semilist:  isa NQPArray
              - variable: %var
                - sigil: %
                - desigilname: var
                  - longname: var
                    - colonpair:  isa NQPArray
                    - name: var
                      - identifier: var
                      - morename:  isa NQPArray
        - sym: my
    - EXPR: grammar G {
	rule TOP {
		<statement>* %% ';'
	}
	
	rule statement {
		| <variable-declaration>
		| <function-call>
	}
	
	rule variable-declaration {
		'var' <variable-name> '=' <number> 
	}
	
	token variable-name {
		\w+
	}
	
	token number {
		\d+
	}
	
	rule function-call {
		'print' <variable-name> 
	}
}	
	
      - package_declarator: grammar G {
	rule TOP {
		<statement>* %% ';'
	}
	
	rule statement {
		| <variable-declaration>
		| <function-call>
	}
	
	rule variable-declaration {
		'var' <variable-name> '=' <number> 
	}
	
	token variable-name {
		\w+
	}
	
	token number {
		\d+
	}
	
	rule function-call {
		'print' <variable-name> 
	}
}
        - sym: grammar
        - package_def: G {
	rule TOP {
		<statement>* %% ';'
	}
	
	rule statement {
		| <variable-declaration>
		| <function-call>
	}
	
	rule variable-declaration {
		'var' <variable-name> '=' <number> 
	}
	
	token variable-name {
		\w+
	}
	
	token number {
		\d+
	}
	
	rule function-call {
		'print' <variable-name> 
	}
}
          - longname: G
            - colonpair:  isa NQPArray
            - name: G
              - morename:  isa NQPArray
              - identifier: G
          - blockoid: {
	rule TOP {
		<statement>* %% ';'
	}
	
	rule statement {
		| <variable-declaration>
		| <function-call>
	}
	
	rule variable-declaration {
		'var' <variable-name> '=' <number> 
	}
	
	token variable-name {
		\w+
	}
	
	token number {
		\d+
	}
	
	rule function-call {
		'print' <variable-name> 
	}
}
            - statementlist: 
	rule TOP {
		<statement>* %% ';'
	}
	
	rule statement {
		| <variable-declaration>
		| <function-call>
	}
	
	rule variable-declaration {
		'var' <variable-name> '=' <number> 
	}
	
	token variable-name {
		\w+
	}
	
	token number {
		\d+
	}
	
	rule function-call {
		'print' <variable-name> 
	}

              - statement: 6 matches
                - EXPR: rule TOP {
		<statement>* %% ';'
	}
	
	
                  - regex_declarator: rule TOP {
		<statement>* %% ';'
	}
	
	
                    - regex_def: TOP {
		<statement>* %% ';'
	}
	
	
                      - trait:  isa NQPArray
                      - signature:  isa NQPArray
                      - deflongname: TOP
                        - colonpair:  isa NQPArray
                        - name: TOP
                          - morename:  isa NQPArray
                          - identifier: TOP
                      - nibble: <statement>* %% ';'
	
                        - termseq: <statement>* %% ';'
	
                          - termaltseq: <statement>* %% ';'
	
                            - termconjseq: 1 matches
                              - termalt: 1 matches
                                - termconj: 1 matches
                                  - termish: 1 matches
                                    - noun: 1 matches
                                      - atom: <statement>
                                        - metachar: <statement>
                                          - assertion: statement
                                            - longname: statement
                                              - name: statement
                                                - morename:  isa NQPArray
                                                - identifier: statement
                                              - colonpair:  isa NQPArray
                                      - separator: %% ';'
	
                                        - septype: %%
                                        - quantified_atom: ';'
	
                                          - sigfinal: 
	
                                            - normspace: 
	
                                          - atom: ';'
                                            - metachar: ';'
                                              - quote: ';'
                                                - nibble: ;
                                      - sigfinal:  
                                        - normspace:  
                                      - quantifier: *
                                        - backmod: 
                                        - sym: *
                    - sym: rule
                - EXPR: rule statement {
		| <variable-declaration>
		| <function-call>
	}
	
	
                  - regex_declarator: rule statement {
		| <variable-declaration>
		| <function-call>
	}
	
	
                    - regex_def: statement {
		| <variable-declaration>
		| <function-call>
	}
	
	
                      - trait:  isa NQPArray
                      - nibble: | <variable-declaration>
		| <function-call>
	
                        - termseq: | <variable-declaration>
		| <function-call>
	
                          - termaltseq: | <variable-declaration>
		| <function-call>
	
                            - termconjseq: 1 matches
                              - termalt: 1 matches
                                - termconj: 2 matches
                                  - termish: 1 matches
                                    - noun: 1 matches
                                      - sigfinal: 
		
                                        - normspace: 
		
                                      - atom: <variable-declaration>
                                        - metachar: <variable-declaration>
                                          - assertion: variable-declaration
                                            - longname: variable-declaration
                                              - name: variable-declaration
                                                - morename:  isa NQPArray
                                                - identifier: variable-declaration
                                              - colonpair:  isa NQPArray
                                  - termish: 1 matches
                                    - noun: 1 matches
                                      - atom: <function-call>
                                        - metachar: <function-call>
                                          - assertion: function-call
                                            - longname: function-call
                                              - colonpair:  isa NQPArray
                                              - name: function-call
                                                - morename:  isa NQPArray
                                                - identifier: function-call
                                      - sigfinal: 
	
                                        - normspace: 
	
                      - deflongname: statement
                        - name: statement
                          - morename:  isa NQPArray
                          - identifier: statement
                        - colonpair:  isa NQPArray
                      - signature:  isa NQPArray
                    - sym: rule
                - EXPR: rule variable-declaration {
		'var' <variable-name> '=' <number> 
	}
	
	
                  - regex_declarator: rule variable-declaration {
		'var' <variable-name> '=' <number> 
	}
	
	
                    - regex_def: variable-declaration {
		'var' <variable-name> '=' <number> 
	}
	
	
                      - trait:  isa NQPArray
                      - signature:  isa NQPArray
                      - deflongname: variable-declaration
                        - colonpair:  isa NQPArray
                        - name: variable-declaration
                          - identifier: variable-declaration
                          - morename:  isa NQPArray
                      - nibble: 'var' <variable-name> '=' <number> 
	
                        - termseq: 'var' <variable-name> '=' <number> 
	
                          - termaltseq: 'var' <variable-name> '=' <number> 
	
                            - termconjseq: 1 matches
                              - termalt: 1 matches
                                - termconj: 1 matches
                                  - termish: 1 matches
                                    - noun: 4 matches
                                      - atom: 'var'
                                        - metachar: 'var'
                                          - quote: 'var'
                                            - nibble: var
                                      - sigfinal:  
                                        - normspace:  
                                      - sigfinal:  
                                        - normspace:  
                                      - atom: <variable-name>
                                        - metachar: <variable-name>
                                          - assertion: variable-name
                                            - longname: variable-name
                                              - colonpair:  isa NQPArray
                                              - name: variable-name
                                                - morename:  isa NQPArray
                                                - identifier: variable-name
                                      - atom: '='
                                        - metachar: '='
                                          - quote: '='
                                            - nibble: =
                                      - sigfinal:  
                                        - normspace:  
                                      - sigfinal:  
	
                                        - normspace:  
	
                                      - atom: <number>
                                        - metachar: <number>
                                          - assertion: number
                                            - longname: number
                                              - colonpair:  isa NQPArray
                                              - name: number
                                                - morename:  isa NQPArray
                                                - identifier: number
                    - sym: rule
                - EXPR: token variable-name {
		\w+
	}
	
	
                  - regex_declarator: token variable-name {
		\w+
	}
	
	
                    - sym: token
                    - regex_def: variable-name {
		\w+
	}
	
	
                      - deflongname: variable-name
                        - name: variable-name
                          - identifier: variable-name
                          - morename:  isa NQPArray
                        - colonpair:  isa NQPArray
                      - nibble: \w+
	
                        - termseq: \w+
	
                          - termaltseq: \w+
	
                            - termconjseq: 1 matches
                              - termalt: 1 matches
                                - termconj: 1 matches
                                  - termish: 1 matches
                                    - noun: 1 matches
                                      - quantifier: +
                                        - backmod: 
                                        - sym: +
                                      - atom: \w
                                        - metachar: \w
                                          - backslash: w
                                            - sym: w
                                      - sigfinal: 
	
                                        - normspace: 
	
                      - signature:  isa NQPArray
                      - trait:  isa NQPArray
                - EXPR: token number {
		\d+
	}
	
	
                  - regex_declarator: token number {
		\d+
	}
	
	
                    - regex_def: number {
		\d+
	}
	
	
                      - nibble: \d+
	
                        - termseq: \d+
	
                          - termaltseq: \d+
	
                            - termconjseq: 1 matches
                              - termalt: 1 matches
                                - termconj: 1 matches
                                  - termish: 1 matches
                                    - noun: 1 matches
                                      - atom: \d
                                        - metachar: \d
                                          - backslash: d
                                            - sym: d
                                      - sigfinal: 
	
                                        - normspace: 
	
                                      - quantifier: +
                                        - backmod: 
                                        - sym: +
                      - deflongname: number
                        - name: number
                          - morename:  isa NQPArray
                          - identifier: number
                        - colonpair:  isa NQPArray
                      - signature:  isa NQPArray
                      - trait:  isa NQPArray
                    - sym: token
                - EXPR: rule function-call {
		'print' <variable-name> 
	}

                  - regex_declarator: rule function-call {
		'print' <variable-name> 
	}

                    - regex_def: function-call {
		'print' <variable-name> 
	}

                      - trait:  isa NQPArray
                      - signature:  isa NQPArray
                      - deflongname: function-call
                        - colonpair:  isa NQPArray
                        - name: function-call
                          - morename:  isa NQPArray
                          - identifier: function-call
                      - nibble: 'print' <variable-name> 
	
                        - termseq: 'print' <variable-name> 
	
                          - termaltseq: 'print' <variable-name> 
	
                            - termconjseq: 1 matches
                              - termalt: 1 matches
                                - termconj: 1 matches
                                  - termish: 1 matches
                                    - noun: 2 matches
                                      - atom: 'print'
                                        - metachar: 'print'
                                          - quote: 'print'
                                            - nibble: print
                                      - sigfinal:  
                                        - normspace:  
                                      - sigfinal:  
	
                                        - normspace:  
	
                                      - atom: <variable-name>
                                        - metachar: <variable-name>
                                          - assertion: variable-name
                                            - longname: variable-name
                                              - name: variable-name
                                                - identifier: variable-name
                                                - morename:  isa NQPArray
                                              - colonpair:  isa NQPArray
                    - sym: rule
          - trait:  isa NQPArray
    - EXPR: class A {
		method variable-declaration($/) {
			%var{$<variable-name>} = +$<number>;
		}
		method function-call($/) {
			say %var{$<variable-name>};
		}
	}




      - package_declarator: class A {
		method variable-declaration($/) {
			%var{$<variable-name>} = +$<number>;
		}
		method function-call($/) {
			say %var{$<variable-name>};
		}
	}
        - sym: class
        - package_def: A {
		method variable-declaration($/) {
			%var{$<variable-name>} = +$<number>;
		}
		method function-call($/) {
			say %var{$<variable-name>};
		}
	}
          - longname: A
            - colonpair:  isa NQPArray
            - name: A
              - morename:  isa NQPArray
              - identifier: A
          - blockoid: {
		method variable-declaration($/) {
			%var{$<variable-name>} = +$<number>;
		}
		method function-call($/) {
			say %var{$<variable-name>};
		}
	}
            - statementlist: 
		method variable-declaration($/) {
			%var{$<variable-name>} = +$<number>;
		}
		method function-call($/) {
			say %var{$<variable-name>};
		}
	
              - statement: 2 matches
                - EXPR: method variable-declaration($/) {
			%var{$<variable-name>} = +$<number>;
		}
		
                  - routine_declarator: method variable-declaration($/) {
			%var{$<variable-name>} = +$<number>;
		}
		
                    - sym: method
                    - method_def:  variable-declaration($/) {
			%var{$<variable-name>} = +$<number>;
		}
		
                      - trait:  isa NQPArray
                      - specials: 
                      - longname: variable-declaration
                        - colonpair:  isa NQPArray
                        - name: variable-declaration
                          - morename:  isa NQPArray
                          - identifier: variable-declaration
                      - multisig: $/
                        - signature: $/
                          - parameter: 1 matches
                            - modifier:  isa NQPArray
                            - default_value:  isa NQPArray
                            - param_var: $/
                              - name: /
                              - sigil: $
                            - trait:  isa NQPArray
                            - quant: 
                            - type_constraint:  isa NQPArray
                            - post_constraint:  isa NQPArray
                          - param_sep:  isa NQPArray
                      - blockoid: {
			%var{$<variable-name>} = +$<number>;
		}
                        - statementlist: 
			%var{$<variable-name>} = +$<number>;
		
                          - statement: 1 matches
                            - EXPR: = +$<number>
                              - 0: {$<variable-name>}
                                - 0: %var
                                  - variable: %var
                                    - desigilname: var
                                      - longname: var
                                        - colonpair:  isa NQPArray
                                        - name: var
                                          - identifier: var
                                          - morename:  isa NQPArray
                                    - sigil: %
                                - postcircumfix: {$<variable-name>}
                                  - O: 
                                  - semilist: $<variable-name>
                                    - statement: 1 matches
                                      - EXPR: $<variable-name>
                                        - variable: $<variable-name>
                                          - sigil: $
                                          - postcircumfix: <variable-name>
                                            - nibble: variable-name
                                            - O: 
                                - OPER: {$<variable-name>}
                                  - O: 
                                  - semilist: $<variable-name>
                                    - statement: 1 matches
                                      - EXPR: $<variable-name>
                                        - variable: $<variable-name>
                                          - sigil: $
                                          - postcircumfix: <variable-name>
                                            - nibble: variable-name
                                            - O: 
                                - postfix_prefix_meta_operator:  isa NQPArray
                              - 1: +
                                - 0: $<number>
                                  - variable: $<number>
                                    - postcircumfix: <number>
                                      - nibble: number
                                      - O: 
                                    - sigil: $
                                - OPER: +
                                  - O: 
                                  - sym: +
                                - prefix: +
                                  - O: 
                                  - sym: +
                                - prefix_postfix_meta_operator:  isa NQPArray
                              - OPER: =
                                - O: 
                                - sym: =
                              - infix: =
                                - O: 
                                - sym: =
                - EXPR: method function-call($/) {
			say %var{$<variable-name>};
		}
	
                  - routine_declarator: method function-call($/) {
			say %var{$<variable-name>};
		}
	
                    - method_def:  function-call($/) {
			say %var{$<variable-name>};
		}
	
                      - specials: 
                      - trait:  isa NQPArray
                      - blockoid: {
			say %var{$<variable-name>};
		}
                        - statementlist: 
			say %var{$<variable-name>};
		
                          - statement: 1 matches
                            - EXPR: say %var{$<variable-name>}
                              - longname: say
                                - colonpair:  isa NQPArray
                                - name: say
                                  - morename:  isa NQPArray
                                  - identifier: say
                              - args:  %var{$<variable-name>}
                                - arglist: %var{$<variable-name>}
                                  - EXPR: {$<variable-name>}
                                    - 0: %var
                                      - variable: %var
                                        - desigilname: var
                                          - longname: var
                                            - colonpair:  isa NQPArray
                                            - name: var
                                              - morename:  isa NQPArray
                                              - identifier: var
                                        - sigil: %
                                    - postcircumfix: {$<variable-name>}
                                      - semilist: $<variable-name>
                                        - statement: 1 matches
                                          - EXPR: $<variable-name>
                                            - variable: $<variable-name>
                                              - postcircumfix: <variable-name>
                                                - nibble: variable-name
                                                - O: 
                                              - sigil: $
                                      - O: 
                                    - OPER: {$<variable-name>}
                                      - semilist: $<variable-name>
                                        - statement: 1 matches
                                          - EXPR: $<variable-name>
                                            - variable: $<variable-name>
                                              - postcircumfix: <variable-name>
                                                - nibble: variable-name
                                                - O: 
                                              - sigil: $
                                      - O: 
                                    - postfix_prefix_meta_operator:  isa NQPArray
                      - longname: function-call
                        - colonpair:  isa NQPArray
                        - name: function-call
                          - identifier: function-call
                          - morename:  isa NQPArray
                      - multisig: $/
                        - signature: $/
                          - parameter: 1 matches
                            - type_constraint:  isa NQPArray
                            - post_constraint:  isa NQPArray
                            - modifier:  isa NQPArray
                            - default_value:  isa NQPArray
                            - param_var: $/
                              - sigil: $
                              - name: /
                            - quant: 
                            - trait:  isa NQPArray
                          - param_sep:  isa NQPArray
                    - sym: method
          - trait:  isa NQPArray
    - EXPR: say G.parse($prog, :actions(A))
      - longname: say
        - colonpair:  isa NQPArray
        - name: say
          - morename:  isa NQPArray
          - identifier: say
      - args:  G.parse($prog, :actions(A))
        - arglist: G.parse($prog, :actions(A))
          - EXPR: .parse($prog, :actions(A))
            - 0: G
              - longname: G
                - colonpair:  isa NQPArray
                - name: G
                  - morename:  isa NQPArray
                  - identifier: G
            - dotty: .parse($prog, :actions(A))
              - dottyop: parse($prog, :actions(A))
                - methodop: parse($prog, :actions(A))
                  - longname: parse
                    - name: parse
                      - morename:  isa NQPArray
                      - identifier: parse
                    - colonpair:  isa NQPArray
                  - args: ($prog, :actions(A))
                    - semiarglist: $prog, :actions(A)
                      - arglist: 1 matches
                        - EXPR: , :actions(A)
                          - 0: $prog
                            - variable: $prog
                              - sigil: $
                              - desigilname: prog
                                - longname: prog
                                  - name: prog
                                    - morename:  isa NQPArray
                                    - identifier: prog
                                  - colonpair:  isa NQPArray
                          - 1: :actions(A)
                            - colonpair: :actions(A)
                              - identifier: actions
                              - coloncircumfix: (A)
                                - circumfix: (A)
                                  - semilist: A
                                    - statement: 1 matches
                                      - EXPR: A
                                        - longname: A
                                          - name: A
                                            - morename:  isa NQPArray
                                            - identifier: A
                                          - colonpair:  isa NQPArray
                          - infix: ,
                            - O: 
                            - sym: ,
                          - OPER: ,
                            - O: 
                            - sym: ,
              - sym: .
              - O: 
            - OPER: .parse($prog, :actions(A))
              - dottyop: parse($prog, :actions(A))
                - methodop: parse($prog, :actions(A))
                  - longname: parse
                    - name: parse
                      - morename:  isa NQPArray
                      - identifier: parse
                    - colonpair:  isa NQPArray
                  - args: ($prog, :actions(A))
                    - semiarglist: $prog, :actions(A)
                      - arglist: 1 matches
                        - EXPR: , :actions(A)
                          - 0: $prog
                            - variable: $prog
                              - sigil: $
                              - desigilname: prog
                                - longname: prog
                                  - name: prog
                                    - morename:  isa NQPArray
                                    - identifier: prog
                                  - colonpair:  isa NQPArray
                          - 1: :actions(A)
                            - colonpair: :actions(A)
                              - identifier: actions
                              - coloncircumfix: (A)
                                - circumfix: (A)
                                  - semilist: A
                                    - statement: 1 matches
                                      - EXPR: A
                                        - longname: A
                                          - name: A
                                            - morename:  isa NQPArray
                                            - identifier: A
                                          - colonpair:  isa NQPArray
                          - infix: ,
                            - O: 
                            - sym: ,
                          - OPER: ,
                            - O: 
                            - sym: ,
              - sym: .
              - O: 
            - postfix_prefix_meta_operator:  isa NQPArray
    - EXPR: dd %var
      - longname: dd
        - colonpair:  isa NQPArray
        - name: dd
          - morename:  isa NQPArray
          - identifier: dd
      - args:  %var
        - arglist: %var
          - EXPR: %var
            - variable: %var
              - desigilname: var
                - longname: var
                  - name: var
                    - identifier: var
                    - morename:  isa NQPArray
                  - colonpair:  isa NQPArray
              - sigil: %
- lang-version: 
# no separation for lexer and paser in perl6, write both in a single grammar


(base) ye@:/media/ye/project2/exp/brain-fuck/rakudo$
```

Class မှာလိုပဲ grammar တွေကိုလည်း overwrite လုပ်လို့ ရတယ်။

If you put your slang in a module:

```
# lambda.pm
sub EXPORT {
	%*LANG<MAIN> := $-MAIN but role { ... }
}

Using it is lexically scoped:   

{
	use lambda;
	lambda hello { say 'hi' }
}
## lambda bye { say 'bye' } # illegal!
sub bye { say 'bye' } # ok
```

```
Conclusion

- Making informal DSLs may involve  
-- creative use of syntax (internal)  
-- parsing (external)  
-- modifying an existing language (variant)  
- Perl 6 offers new and exiciting techniques for each of these.  
```



## Reference

- https://examples.p6c.dev/categories/interpreters/brainfuck.html  
- https://github.com/raku-community-modules/Inline-Brainfuck  

- Andrew Shitov. Perl 6 grammars for simple compilers (lightning talk):  
https://www.youtube.com/watch?v=rxaB6m_sQKk  

- https://www.youtube.com/watch?v=lwIXF25KJCo  
- https://github.com/ash/lingua  

- https://edu.anarcho-copy.org/Programming%20Languages/Perl/perl-6-deep-dive.pdf  
- https://github.com/drforr/perl6-Grammar-Common  

- Perl6, https://perl6.org
- Regexes, https://docs.perl6.org/language/regexes
- MLCad, http://mlcad.lm-software.com/
- https://www.youtube.com/watch?v=yMybtZV_Uy4
- https://www.newthinktank.com/2019/01/perl-6-tutorial/
- https://perl6advent.wordpress.com/2015/12/07/day-7-unicode-perl-6-and-you/




