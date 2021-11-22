# Introduction
**BRICK** is a bounded reachability checker for numericallyintensive C code, with special emphasis on handling nonlinear operations. It supports user-speciﬁed safety speciﬁcation checking as well as built-in assertion and domain error checking. 

Diﬀerent from the existing tools, **BRICK** supports the checking of codes with nonlinear operations. e.g. trigonometric functions, exponential functions by delta-decision SMT solver dReal. At the same time, **BRICK** supports inter-procedural analysis, and analysis of complex structures including arrays, structs, and pointer registers. **BRICK** has scaled well on realistic programs in evaluation, e.g. for debugging the GNU Scientiﬁc Library (GSL).

The functionalities of **BRICK** are shown from the following command in the standard unix command-line style:     
`BRICK < filename > -f < func > -b < bound > -p < precision > [-options]`.

**BRICK** returns the error type and line number if a error would ocurr. It also shows the inputs that trigger it.

# Experiment
We evaluate **BRICK** on functions of specfunc in the GNU scientiﬁc library ([GSL](http://www.gnu.org/software/gsl/gsl.html)), which is a mature and widely-used numerically-intensive scientiﬁc library. Furthermore, we locate one similar projects Numerical Algorithms in ALGOL ([NUMAL](https://github.com/JeffBezanson/numal)) library in C in github.

## Benchmark
* [GSL](https://github.com/BRICK-tool/Experiment/tree/master/GSL-benchmark) 
* [NUMAL](https://github.com/BRICK-tool/Experiment/tree/master/NUMAL-benchmark)    
After downloading the benchmark, move binary to the benchmark directory and run the bash file.     

## Results
The output and statics of experiment:
* [GSL](https://github.com/BRICK-tool/Experiment/tree/master/GSL)
* [NUMAL](https://github.com/BRICK-tool/Experiment/tree/master/numal)

# How to Build
## Source Code and Build Instructions
You can download and build the source code of BRICK according to the following instructions:     
###Install g++-4.9
```
sudo add-apt-repository ppa:ubuntu-toolchain-r/test -y    
sudo add-apt-repository ppa:dns/gnu -y     
sudo update-alternatives --remove-all gcc    
sudo update-alternatives --remove-all g++    
sudo apt-get update    
sudo apt-get install -qq g++-4.9     
sudo apt-get upgrade    
sudo apt-get dist-upgrade -y    
```
### Download LLVM and Clang
Go to the [release page](http://releases.llvm.org/) of llvm                
Download LLVM-3.5.0
### Build and Install LLVM and Clang
```
cd llvm    
./configuration     
make     
sudo make install    
```
### Build and Install Minisat
```
git clone https://github.com/niklasso/minisat.git
cd minisat  
make
sudo make install     
```
### Build and Install Z3
```
git clone https://github.com/Z3Prover/z3.git
cd z3
python scripts/mk_make.py
cd build
make
sudo make install
```
### Build and Install dReal
```
git clone https://github.com/dreal/dreal3.git dreal
cd dreal
mkdir -p build/release
cd build/release
cmake -DCMAKE_BUILD_TYPE=RELEASE -DCMAKE_CXX_COMPILER=g++-4.9 -DCMAKE_C_COMPILER=gcc-4.9 -DBUILD_SHARED_LIB=ON ../../src
make
sudo make install
```
### Download and build BRICK
```
cd llvm/lib/Transforms    
git clone https://github.com/BRICK-tool/BRICK-tool.git    
cd BRICK-tool    
./Build_BRICK.sh    
```
The binary is in Directory Bin.     
Our tool is now mainly based on LLVM3.5. If there is any problem with other versions, please contact us.


