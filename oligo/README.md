# oligo

# 报错
## 加载包报错

    Loading required package: oligoClasses
    Error: package or namespace load failed for ‘oligoClasses’:
     objects ‘open.ff’, ‘close.ff’ are not exported by 'namespace:ff'
    Error: package ‘oligoClasses’ could not be loaded
* ff包版本问题，安装旧版版本解决

        install.packages('https://cran.r-project.org/src/contrib/Archive/ff/ff_2.2-14.tar.gz',repos=NULL)
        安装完成后重启R
## rma报错

    > DATA.rma <- oligo::rma(rawdata)
    Background correcting
    Error in basicRMA(pms, pnVec, normalize, background) : 
      ERROR; return code from pthread_create() is 22
* 可能为openblas版本问题

        I solved this problem downgrading the version of openblas to 0.3.3

