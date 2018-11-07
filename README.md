# R
cor 求列之间的相关性
<br>dist 按行聚类
<br>WGCNA 导入数据格式 行为样本 列为基因
<br>WGCNA 的导入数据一般只取一组?多组？ 
## 1.pheatmap 更改源码包，增加导出聚类基因结果列表功能
* 下载源码包
* 增加新函数

      write_matrix=function(mat,out_file){
	      write.table(as.data.frame(mat),sep='\t',quote=F,file=out_file)
      }
* pheatmap画图函数增加新参数out_file=NA（默认）
* pheatmap画图函数内增加新的过程

      if( !is.na(out_file) ){
		    write_matrix( mat, out_file )
	    }

* Rstudio安装该包
### 报错

    Error in install.packages : type == "both" cannot be used with 'repos = NULL'
原因：压缩包为.rar格式
<br>解决：压缩格式应为tar.gz 或者zip

    file ‘R/pheatmap.r’ has the wrong MD5 checksum
原因：修改了源码，MD5发生改变
<br>解决：不影响，类似warning

	'C:/install/R-3.4.1/library/pheatmap/DESCRIPTION': No such file or directory
原因：压缩文件命名问题
<br>解决：更改压缩文件名为下载原始压缩文件名称
### 使用方法
pheatmap(out_file='文件名')，即可生成聚类后的结果

## 2.affy芯片自定义CDF环境方法
### 方法1 
获取目前芯片所需的GDF环境名称

	file<-list.files(path="data/",pattern=".CEL.gz",ignore.case=TRUE,full.names=TRUE)
	#获取CDF name
	cleancdfname(whatcdf(file[1]))
	[1] "glycov3mmcdf"
创建CDF环境，环境赋值给变量，变量名为上一步获取的CDF环境名称

	glycov3mmcdf <- make.cdf.env('data/GPL11096_GLYCOv3_Mm.CDF.gz',compress = T)

### 方法2
详见makecdfenv包使用说明

## R报错 maximal number of DLLs reached
* 环境变量增加

		export R_MAX_NUM_DLLS=300:$R_MAX_NUM_DLLS
		数值超过500会报错
		R_MAX_NUM_DLLS bigger than 614 may exhaust open files limit
		R3.5可能已修复该问题
		






