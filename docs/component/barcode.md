## Barcode 组件（component）

### 属性说明
设置Barcode扫码控件的属性，如扫码框、扫码条的颜色等。

属性|类型 |默认值|必填|说明
:--|:--|:--|:--|:--|
background|string| |否|条码识别控件背景颜色,颜色值支持(参考CSS颜色规范)：颜色名称(参考CSS Color Names)/十六进制值/rgb值，默认值为黑色。
frameColor |string| |否|扫码框颜色,颜色值支持(参考CSS颜色规范)：颜色名称(参考CSS Color Names)/十六进制值/rgb值/rgba值，默认值为红色。
scanbarColor|string||否|扫码条颜色,颜色值支持(参考CSS颜色规范)：颜色名称(参考CSS Color Names)/十六进制值/rgb值/rgba值，默认值为红色。
filters|Array[Number] |[0,1,2]|否|条码类型过滤器，条码类型常量数组，默认情况支持QR、EAN13、EAN8类型。 通过此参数可设置扫码识别支持的条码类型（注意：设置支持的条码类型越多，扫描识别速度可能将会降低）。

#### 常量：
- QR: QR二维码，数值为0
- EAN13: EAN条形码标准版，数值为1
- EAN8: ENA条形码简版，数值为2
- AZTEC: Aztec二维码，数值为3
- DATAMATRIX: Data Matrix二维码，数值为4
- UPCA: UPC条形码标准版，数值为5
- UPCE: UPC条形码缩短版，数值为6
- CODABAR: Codabar条形码，数值为7
- CODE39: Code39条形码，数值为8
- CODE93: Code93条形码，数值为9
- CODE128: Code128条形码，数值为10
- ITF: ITF条形码，数值为11
- MAXICODE: MaxiCode二维码，数值为12
- PDF417: PDF 417二维条码，数值为13
- RSS14: RSS 14条形组合码，数值为14
- RSSEXPANDED: 扩展式RSS条形组合码，数值为15

### API
#### start(object)
> 开始扫码识别

##### Object object
属性|说明|类型|必填|备注
:--|:--|:--|:--|:--|
conserve|是否保存扫码成功时的截图|Boolean|否|如果设置为true则在扫码成功时将图片保存，并通过onmarked回调函数的file参数返回保存文件的路径。 默认值为false，不保存截图。
filename|保存扫码成功时图片保存路径|String|否|可通过此参数设置保存截图的路径和名称，如果设置图片文件名称则必须指定文件的后缀名（必须是.png），否则认为是指定目录，文件名称则自动生成。
vibrate|扫码成功时是否需要震动提醒|Boolean|否|如果设置为true则在扫码成功时震动设备，false则不震动。 默认值为true。
sound|扫码成功时播放的提示音|String|否|可取值： "none" - 不播放提示音； "default" - 播放默认提示音（5+引擎内置）。 默认值为"default"。


#### cancel()
> 取消扫码识别

参数|类型 |必填|说明
:--|:--|:--|:--|
无|无| 无| 结束对摄像头获取图片数据进行条码识别操作，同时关闭摄像头的视频捕获。 结束后可调用start方法重新开始识别。

#### setFlash(object)
> 操作闪光灯

##### Object object
类型 |必填|说明|备注
:--|:--|:--|:--|
Boolean| 是| 是否开启闪光灯|可取值true或false，true表示打开闪光灯，false表示关闭闪光灯。

<br>
## barcodeScan 模块 (module)

#### scan(object,callback,object)
> 扫码识别图片中的条码

##### object
类型 |默认值|必填|说明
:--|:--|:--|:--|
String| |是|要扫码的图片路径,必须是本地文件路径，如URLType类型（如以"_www"、"_doc"、"_documents"、"_downloads"开头的相对URL路径）或者系统绝对路径。
Array| |否|条码类型过滤器，条码类型常量数组，默认情况支持QR、EAN13、EAN8类型。 通过此参数可设置扫码识别支持的条码类型（注意：设置支持的条码类型越多，扫描识别速度可能将会降低）。

##### callback 返回 Object 参数说明
##### 成功时
属性|类型 |说明
:--|:--|:--|
type|string|"success" 表示成功
message|string|识别到的条码数据，扫码识别出的数据内容，字符串类型，采用UTF8编码格式。
code|Number|识别到的条码类型，与Barcode组件的条码类型常量一致。
file|string|扫码成功的截图文件路径，扫码识别到的截图，png格式文件，如果设置为不保存截图，则返回undefined。
##### 失败时
属性|类型 |说明
:--|:--|:--|
type|string|"fail" 表示失败
code|number| 相应 code 码
message|string|失败描述

### 事件

#### marked
> 条码识别成功事件

#####  返回参数说明
参数|类型 |说明
:--|:--|:--|
type|string|"success" 表示成功
message|string|识别到的条码数据，扫码识别出的数据内容，字符串类型，采用UTF8编码格式。
code|Number|识别到的条码类型，与Barcode组件的条码类型常量一致。
file|string|扫码成功的截图文件路径，扫码识别到的截图，png格式文件，如果设置为不保存截图，则返回undefined。


#### error
> 条码识别错误事件

#####  返回参数说明
参数|类型 |说明
:--|:--|:--|
type|string|"fail" 表示失败
code|number| 相应 code 码
message|string|失败描述
