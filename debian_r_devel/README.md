Alternative track. Use this build command.

```sh
## ~/bin/build-R-devel
#!/bin/sh
cd ~/svn/R-devel-build
# R_PAPERSIZE=letter                \
# R_BATCHSAVE="--no-save --no-restore"         \
# R_BROWSER=xdg-open                \
# PAGER=/usr/bin/pager                \
# PERL=/usr/bin/perl                \
# R_UNZIPCMD=/usr/bin/unzip            \
# R_ZIPCMD=/usr/bin/zip                \
# R_PRINTCMD=/usr/bin/lpr                \
# LIBnn=lib                    \
# AWK=/usr/bin/awk                                \
# CC="ccache gcc"                    \
# CFLAGS="-ggdb -pipe -std=gnu99 -Wall -pedantic -DTESTING_WRITE_BARRIER" \
# CXX="ccache g++"                \
# CXXFLAGS="-ggdb -std=c++0x -pipe -Wall -pedantic" \
# FC="ccache gfortran"                \
# FCFLAGS="-ggdb -pipe -Wall -pedantic"        \
# F77="ccache gfortran"                \
# FFLAGS="-ggdb -pipe -Wall -pedantic"        \
# MAKE="make -j4"                    \
# ./configure                     \
#     --prefix=/usr/local/lib/R-devel         \
#     --enable-R-shlib                 \
#     --enable-strict-barrier             \
#     --with-blas                 \
#     --with-lapack                 \
#     --with-readline                 \
#     --without-recommended-packages
R_PAPERSIZE=letter                \
R_BATCHSAVE="--no-save --no-restore"         \
R_BROWSER=xdg-open                \
PAGER=/usr/bin/pager                \
PERL=/usr/bin/perl                \
R_UNZIPCMD=/usr/bin/unzip            \
R_ZIPCMD=/usr/bin/zip                \
R_PRINTCMD=/usr/bin/lpr                \
LIBnn=lib                    \
AWK=/usr/bin/awk                                \
CC="ccache gcc"                    \
CFLAGS="-ggdb -pipe -std=gnu99 -Wall -pedantic" \
CXX="ccache g++"                \
CXXFLAGS="-ggdb -pipe -Wall -pedantic"         \
FC="ccache gfortran"                   \
F77="ccache gfortran"                \
MAKE="make -j4"                    \
../r-devel/R/configure                     \
--prefix=/usr/local/lib/R-devel         \
--enable-R-shlib                 \
--with-blas                 \
--with-lapack                 \
--with-readline                 \
--without-recommended-packages
#CC="clang -O3"                                  \
#CXX="clang++ -03"                \
#make svnonly
make 
echo "*** Done -- now run 'make install'"
make install
echo "*** All Done -- start R-devel with 'bash R-devel'"
```

Use this shell script to run R-devel

```sh
## ~/bin/R-devel.sh
#!/bin/bash
export R_LIBS_SITE=${R_LIBS_SITE-'/usr/local/lib/R-devel/lib/R/library:~/R/x86_64-pc-linux-gnu-library/3.7'}
export PATH="/usr/local/lib/R-devel/bin:$PATH"
R "$@"
```

