# glpkAPI 包安装
* 环境准备

      #安装gmp
      yum install gmp-devel
      #安装GLPK
      tar -xzf glpk-4.65.tar.gz
      cd glpk-4.65
      mkdir Install
      ./configure --with-gmp --prefix=/biosoftware/GLPK/glpk-4.65/Install
      make
      make install


* 下载源码包

      glpkAPI_1.3.1.tar.gz

* 安装

      R3.6 CMD INSTALL --configure-args="--with-glpk-include=/biosoftware/GLPK/glpk-4.65/Install/include/ --with-glpk-lib=/biosoftware/GLPK/glpk-4.65/Install/lib/" glpkAPI_1.3.1.tar.gz

* 报错1

      Error: package or namespace load failed for ‘glpkAPI’ in dyn.load(file, DLLpath = DLLpath, ...):
       unable to load shared object '/opt/R-3.6.0/Install/lib64/R/library/00LOCK-glpkAPI/00new/glpkAPI/libs/glpkAPI.so':
        libglpk.so.40: cannot open shared object file: No such file or directory
      Error: loading failed
      Execution halted
      ERROR: loading failed
      * removing ‘/opt/R-3.6.0/Install/lib64/R/library/glpkAPI’
* 解决

      #下载libglpk40-4.65-47.1.x86_64.rpm
      ftp://ftp.pbone.net/mirror/ftp5.gwdg.de/pub/opensuse/repositories/devel:/languages:/R:/released/SLE_12/x86_64/libglpk40-4.65-47.1.x86_64.rpm
      #安装
      rpm -Uvh libglpk40-4.65-47.1.x86_64.rpm 
      #重装R包
      R3.6 CMD INSTALL --configure-args="--with-glpk-include=/biosoftware/GLPK/glpk-4.65/Install/include/ --with-glpk-lib=/biosoftware/GLPK/glpk-4.65/Install/lib/" glpkAPI_1.3.1.tar.gz


