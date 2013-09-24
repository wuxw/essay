##前言##

数码照片和照片处理之间的内在关系非常复杂...其中有些术语，用在不同的对象和不同的场景下，又有不同的含义。在开始处理照片之前，还是要先了解一些基础知识，否则你最后只能知其一不知其二，单纯地使用处理工具却不理解他们的作用方式（正如我现在所处的局面，软件会用，但是完全不能理解工具处理的原理，当然，知其然正是我学习照片处理基础知识的动力）。

##图像文件##

###矢量图和点阵图###

+	矢量图

矢量图是根据几何特性来绘制图形，矢量可以是一个点或一条线，矢量图只能靠软件生成，文件占用内在空间较小，因为这种类型的图像文件包含独立的分离图像，可以自由无限制的重新组合。它的特点是放大后图像不会失真，和分辨率无关，适用于图形设计、文字设计和一些标志设计、版式设计等。

但是一张图片有无数微小的细节，要把每个细节都加以量化就太复杂了，而且技术上几乎不能实现。所以，数码照片的显示采用的其实是点阵图。

+	点阵图

也叫做位图[bitmap]，删格图像，像素图。简单的说，就是最小单位由像素构成的图，缩放会失真。构成位图的最小单位是像素，位图就是由像素阵列的排列来实现其显示效果的，每个像素有自己的颜色信息。

###像素###

“像素”（Pixel）是由Picture（图像）和Element（元素）这两个单词的字母所组成的，是用来计算数码影像的一种单位，在不同场合，像素含义并非总是相同的：

+	在相机中，像素指一个感光单位，这个单位在感光元件上占一小块地方，特定颜色的亮度能够在这个单位上得以确定。
+	一张数码照片的图像文件是由固定数量的排列在一个网格中的单个图像点组成的，这些图像点就是像素。每个像素都含有一个图像信息，但是没有物理的时机尺寸。所以，像素在图像文件中只是一个逻辑的信息单位，并且只有在**介质**上显示才会获得真实的尺寸。**这种尺寸取决于介质的分辨率。**

###色彩深度###

色彩深度计算机图形学领域表示在位图或者视频帧缓冲区中储存1像素的颜色所用的位数，它也称为位/像素（bpp）。色彩深度越高，可用的颜色就越多。

色彩深度是用“n位颜色”（n-bit colour）来说明的。若色彩深度是n位，即有2种颜色选择，而储存每像素所用的位数就是n。常见的有：

+	1位：2种颜色，单色光，黑白二色，用于compact Macintoshes。
+	2位：4种颜色，CGA，用于gray-scale早期的NeXTstation及color Macintoshes。
+	3位：8种颜色，用于大部分早期的电脑显示器。
+	4位：16种颜色，用于EGA及不常见及在更高的分辨率的VGA标准，color Macintoshes。
+	5位：32种颜色，用于Original Amiga chipset。
+	6位：64种颜色，用于Original Amiga chipset。
+	8位：

--256种颜色，用于最早期的彩色Unix工作站，低分辨率的VGA，Super VGA，AGA，color Macintoshes。
--灰阶，有256种灰色（包括黑白）。若以24位模式来表示，则RGB的数值均一样，例如(200,200,200)。

+	12位：4,096种颜色，用于部分硅谷图形系统，Neo Geo，彩色NeXTstation及Amiga系统于HAM mode。
+	16位：65,536种颜色，用于部分color Macintoshes。
+	24位：16,777,216种颜色，**真彩色**，能提供比肉眼能识别更多的颜色，用于拍摄照片。

另外有高动态范围影像(High Dynamic Range Image)，这种影像使用超过一般的256色阶来储存影像，通常来说每个像素会分配到32+32+32个bit来储存颜色资讯，也就是说对于每一个原色都使用一个32bit的浮点数来储存。

##EXIF、IPTC、XMP元数据##

###EXIF###

[EXIF](http://en.wikipedia.org/wiki/Exchangeable_image_file_format)是一种图象文件格式，它的数据存储与JPEG格式是完全相同的。实际上Exif格式就是在JPEG格式头部插入了数码照片的信息，包括拍摄时的光圈、快门、白平衡、ISO、焦距、日期时间等各种和拍摄条件以及相机品牌、型号、色彩编码、拍摄时录制的声音以及全球定位系统（GPS）、缩略图等。简单地说，Exif=JPEG+拍摄参数。

示例：

<table><tbody><tr><td><div class="para">项目</div>
</td><td><div class="para">资讯</div>
</td></tr><tr><td><div class="para">制造厂商</div>
</td><td><div class="para">Canon</div>
</td></tr><tr><td><div class="para">相机型号</div>
</td><td><div class="para">Canon EOS-1D Mark II</div>
</td></tr><tr><td><div class="para">影像方向</div>
</td><td><div class="para">正常（upper-left）</div>
</td></tr><tr><td><div class="para">影像分辨率 X</div>
</td><td><div class="para">72</div>
</td></tr><tr><td><div class="para">影像分辨率 Y</div>
</td><td><div class="para">72</div>
</td></tr><tr><td><div class="para">分辨率单位</div>
</td><td><div class="para">dpi</div>
</td></tr><tr><td><div class="para">Software</div>
</td><td><div class="para">Adobe Photoshop CS Macintosh</div>
</td></tr><tr><td><div class="para">最后异动时间</div>
</td><td><div class="para">2005:10:06 12:53:19</div>
</td></tr><tr><td><div class="para">YCbCrPositioning</div>
</td><td><div class="para">2</div>
</td></tr><tr><td><div class="para">曝光时间</div>
</td><td><div class="para">0.00800 (1/125) sec</div>
</td></tr><tr><td><div class="para">光圈值</div>
</td><td><div class="para">F1.6</div>
</td></tr><tr><td><div class="para">拍摄模式</div>
</td><td><div class="para">光圈优先</div>
</td></tr><tr><td><div class="para">ISO 感光值</div>
</td><td><div class="para">100</div>
</td></tr><tr><td><div class="para">EXIF 资讯版本</div>
</td><td><div class="para">30,32,32,31</div>
</td></tr><tr><td><div class="para">影像拍摄时间</div>
</td><td><div class="para">2005:09:25 15:00:18</div>
</td></tr><tr><td><div class="para">影像存入时间</div>
</td><td><div class="para">2005:09:25 15:00:18</div>
</td></tr><tr><td><div class="para">曝光补偿（EV+-）</div>
</td><td><div class="para">0</div>
</td></tr><tr><td><div class="para">测光模式</div>
</td><td><div class="para">点测光 (Spot)</div>
</td></tr><tr><td><div class="para">闪光灯</div>
</td><td><div class="para">关闭</div>
</td></tr><tr><td><div class="para">镜头实体焦长</div>
</td><td><div class="para">85 mm</div>
</td></tr><tr><td><div class="para">Flashpix 版本</div>
</td><td><div class="para">30,31,30,30</div>
</td></tr><tr><td><div class="para">影像色域空间</div>
</td><td><div class="para">sRGB</div>
</td></tr><tr><td><div class="para">影像尺寸 X</div>
</td><td><div class="para">800 pixel</div>
</td></tr><tr><td><div class="para">影像尺寸 Y</div>
</td><td><div class="para">533 pixel</div>
</td></tr></tbody></table>

###IPTC###

[IPTC](http://en.wikipedia.org/wiki/IPTC_Information_Interchange_Model)是国际出版电讯委员会(International Press Telecommunications Council)的缩写，IPTC元数据就是一种标准格式，可以将以下元数据加入照片信息中，如作者，作者联系方式，版权，字幕，细节描述等。

###XMP###

可延伸元数据平台（Extensible Metadata Platform，XMP），是一项由 Adobe Systems 所创建的 ISO 标准[（ISO 16684-1:2012）](http://www.iso.org/iso/home/news_index/news_archive/news.htm?refid=Ref1525)，其目的在于将数位影像资料的元数据标准化。

在我看过PhotoShop产生的XMP文档源代码之后，个人感觉XMP还是非常强大的。PS所有对图像的调整，都能实时记录在XMP文件下而不改变源图像文件，无损处理图片。XMP文件还可以直接使用文本编辑器修改。

既然我是搞技术的，那么我就附上一段XMP文档作为参考吧，请猛击**[这里](./IMG_5314.xmp)**。

##文件格式##

###RAW格式###

这个格式的特点是，感光原件上所有的信息都会被存储下来，无论是相机内置的处理器还是后期的处理操作都不能改变他的图像信息。RAW文件既不能改动，也不能直接处理。

RAW并不是独立并且标准化的，每个相机制造商，都有自己的RAW格式，甚至同一个品牌相机的RAW格式也有一定差异。常见的RAW文件有：

+	.3FR（ 哈苏 ）
+	.ARI（ARRIFLEX）
+	.ARW .SRF .SR2（ 索尼 ）
+	.bay（ 卡西欧 ）
+	.crw .cr2（ 佳能 ）
+	.cap .iiq .eip（Phase_One）
+	.dcs .dcr .drf .k25 .kdc（ 柯达 ）
+	.DNG（ 奥多比 ）
+	.ERF（ 爱普生 ）
+	.FFF（ 易迈康 ）
+	.MEF（ 玛米亚 ）
+	.MOS（ leaf ）
+	.MRW（ 美能达 ）
+	.NEF.NRW（ 尼康 ）
+	.ORF（ 奥林巴斯 ）
+	.PEF.PTX（ 宾得 ）
+	.PXN（ 罗技 ）
+	.R3D（ Red ）
+	.raf（ 富士 ）
+	.raw .rw2（ 松下 ）
+	.raw .rwl .dng（ 莱卡 ）
+	.rwz（Rawzor）
+	.srw（ 三星 ）
+	.X3F（西格玛）

###DNG格式###

全名是Digital negative——数字负片，是Adobe开发的一种用于数码相机生成的原始数据文件的公共存档格式。DNG 解决了不同型号相机的RAW原始数据文件之间缺乏开放式标准的问题，从而有助于确保摄影师们将来能够访问他们的文件。

主要优点：

+	消除了新型号相机采用该格式的潜在障碍，因为新型号相机的原始数据文件将很快获得 Photoshop 及其他应用程序的支持
+	使得商家不再需要开发新格式，且能简化相机测试过程，从而节省了研发费用
+	作为一种通用格式，DNG 使得第三方应用程序能够加强对转换质量的控制
+	该规范允许向 DNG 文件添加专用元数据，从而能实现文件的区分

###JPEG格式###

###TIFF格式###

标签图像文件格式（Tagged Image File Format，简写为TIFF），以**.tif**为扩展名。TIFF最初的设计目的是为了1980年代中期桌面扫描仪厂商达成一个公用的扫描图像文件格式，而不是每个厂商使用自己专有的格式。

这种格式的特点是能保证极高的图像质量，因此它也作为照片处理软件之间的交换格式而被应用于高质量的打印。

###PNG格式###

###PSD格式###

Photoshop Document（PSD），是著名的Adobe公司的图像处理软件Photoshop的专用格式。这种格式可以存储Photoshop中所有的图层，通道、参考线、注解和颜色模式等信息。

PSD格式的文件是一种图形文件格式，因此，使用看图软件如ACDSee 或图形处理软件如我形我速、PhotoShop等都可以打开的。

##图像大小和分辨率##

###图像大小###

这边要弄清楚两个概念，一个是图像大小，一个是图像文件大小。

**图像大小**涉及的是图像中，图像点的数量。以像素乘以像素来说明，其中第一个像素指的是水平方向的像素数量，第二个像素指的是垂直方向的像素数量。例如，一个图片大小可以是4368 x 2912像素，总共12719616像素或者取整为120万像素。

**图像文件大小**和它存储空间有关，以字节为单位。

**图像大小**只是一个虚拟的值，单独这个值既不能以厘米计算，也不能说明显示器上的图像的大小。为了对图像进行确切的描述，还需要**分辨率**这个值。只有通过介质的显示，数字的像素信息才能有一个实际的载体。

###分辨率###

单位长度内包含的像素点的数量，它的单位通常为像素/英寸（ppi）。分辨率也被用于其他的场景下，但是不同场景下，其含义有所不同：

+	镜头分辨率，英文是Resolution，不过在这边其实叫解像力应该更合适。解像力是用来描述缩微摄影系统再现被摄原件细微部分能力的物理量，是影像量评价的重要指标。在物体反差无限大的时候（就是所有物象在纯白和纯黑下）镜头记录物体细节的能力，国际标准单位是 线对/毫米（lp/mm）。当镜头在一毫米的范围内，可以分辩出60根平行线组成的图案，这时我们说这支镜头的光学分辨率为60lp/mm。理论上说分辨率越高的镜头，它成像也越清晰。

+	显示器分辨率是指单位面积显示像素的数量。

一张照片的分辨率其实并没有说明这个图像文件中真正的像素数量。因为在**一个特定介质上**，一张大图和一张小图的**分辨率是一样的**。

**同样的一张图片，分辨率越小，图片显示出来的尺寸就越大。反之，分辨率越高，图片显示出来的尺寸就越小。**

##色调##

色调不是指颜色的性质，是对一幅绘画作品的**整体评价**。一幅绘画作品虽然用了多种颜色，但总体有一种色调，是偏藍或偏红，是偏暖或偏冷等等。

##对比度##

对比度是最白与最黑**亮度单位**的**相除值**。对比度对视觉效果的影响非常关键，一般来说对比度越大，图像越清晰醒目，色彩也越鲜明艳丽；而对比度小，则会让整个画面都灰蒙蒙的。高对比度对于图像的清晰度、细节表现、灰度层次表现都有很大帮助。

##颜色##

##参考文档##

1.	[初略谈谈镜头的分辨率、明锐度和反差](http://club.pchome.net/thread_2_5_266373__.html)