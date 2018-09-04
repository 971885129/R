# R
cor 求列之间的相关性
<br>dist 按行聚类
<br>WGCNA 导入数据格式 行为样本 列为基因
<br>WGCNA 的导入数据一般只取一组?多组？ 
## pheatmap 更改源码包，增加导出聚类基因结果列表功能
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
解决：压缩应方式为tar 或 zip 

    file ‘R/pheatmap.r’ has the wrong MD5 checksum
原因：修改了源码，MD5发生改变  
解决：删掉MD5文件
