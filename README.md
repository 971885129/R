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
		
## 3.t.test
* 计算两组差异时，若两组数据完全一样，曾报错
## 4.apply内函数导入多参数

	fxn <- function(var1,var2){
		}
	apply(dataframe,1,fxn,var2=2)

## 5.Affy芯片数据处理
* annotate包可识别芯片所需注释包

		annPkgName(DATA@annotation,type="db")
* affycoretools包可利用annotate识别出的注释包对芯片进行注释（需确定注释包名称是否有差别）

		eset <- annotateEset(DATA.rma,hgu133plus2.db)
		annotation <- pData(featureData(eset))
* oligo包质控步骤

		待完善
* olig包标准化

		背景校正
		oligo::backgroundCorrectionMethods()#展示有哪些校正方法
		[1] "rma"  "mas"  "LESN"
		bgdata <- backgroundCorrect(DATA,method = 'mas')
		组间标准化
		normalizationMethods()#展示有哪些标准化方法
		[1] "quantile"           "quantile.robust"    "quantile.in.blocks" "qspline"            "loess"              "invariantset"      
		[7] "constant"  
		normData <- normalize(bgdata)#默认为quantile normalization
		未知
		summarizationMethods()
		summarize()
oligo::rma(),背景校正方法为rma,组间标准化方法为quantile normalization，同时可将读取数据得到的GeneFeatureSet数据格式转化为ExpressionSet，从而可提取表达量
<br>若想选择其他标准化方法，可通过上面的拆分步骤进行，但GeneFeatureSet格式和ExpressionFeatureSet格式无法summarize，故目前无法分步骤进行标准化
<br>可通过用oligo::rma(normData,normalize=F,background=F)方法转换为ExpressionSet，但经测试affy芯片用mas方法会报错，故需确认？
<br>ExpressionFeatureSet格式的数据可以通过backgroundCorrect + normalize + summarize进行处理，但不清楚如何获取该数据格式？

	发现在部分芯片中，读取原始数据是ExpressionFeatureSet格式，还有有的芯片是GeneFeatureSet格式，而且这两种芯片数据可能来自同一种平台
	关于GeneFeatureSet格式，chrome收藏书签“the oligo package”有介绍
<br>注意： mas LESN可能只能适用于双通道芯片？affy为单通道芯片？故只能用rma？可用Affy包验证

## apply传递多参数

	apply(exp,1,FC,s1=sam1,s2=sam2)











