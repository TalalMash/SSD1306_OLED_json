# 目录
编辑中...

---
# 简介
嵌入式linux驱动SSD1306芯片的OLED，采用json文件配置显示内容

---
# 配置文件
配置文件采用json格式，使用cJSON解析，语法遵循json语法

## 开始运行
**方法1：**
将config.json和二进制ssd放入同一目录，终端进入该目录执行
```
./ssd
```
**方法2**：
将config.json放入`/xxx`目录，终端进入`ssd`所在目录执行
```
./ssd -c /xxx/config.json
```

## json简介
* JSON(JavaScript Object Notation, JS 对象简谱) 是一种轻量级的数据交换格式
* 其主要元素为`健`、`值`、`符号`
* 基本语法规则:
1. 数据在`健/值`对中
2. 数据由`逗号`分隔
3. `大括号`保存`对象`
4. `中括号`保存`数组`
* `健`必须是`字符串`，且用`""`引起来
* `值`可以是
1. `数字`（整数或浮点数）
3. `字符串`（在双引号中）
4. `逻辑值`（true 或 false）
5. `数组`（在中括号中）
6. `对象`（在大括号中）
7. `null`  
注：在本程序配置文件中只采用了`数字`、`字符串`、`数组`、`对象` 

## 整体说明
本程序使用分页的方式显示各种内容，json表现为多个页面数据在同一级。 
配置文件整体结构如下：
```
{
	"seting":{
	},
	"test1":{
	},
	"test2":{
	}
}
```
键`"seting"`为[软硬件设置](#软硬件设置)，其值为`对象`，包含了分辨率、地址以及驱动文件等信息 
键`"text1"`、`"text2"`为[页面数据](#显示数据)，值为`对象`,包含了页面相关数据，名称可以自定义。 

## 软硬件设置
```
"seting":{
	"pixel":12864,
	"dev":"/dev/i2c-0",
	"addr":60
}
```
`"pixel"`:分辨率，值为`数字`，可选`12864`、`12832`，默认`12864`  
`"dev"`:i2c驱动路径，值为`字符串`,默认`"/dev/i2c-0"`  
`"addr"`:OLED在i2c总线的地址，值为`数字`，默`60`，即十六进制`0x3c`（json不支持十六进制表示）  
注：在配置文件中，可以省略`"seting":{}`  

## 页面数据
```
"test1":{
	"seting":{
	},
	"display":[
	]
}
```
`"seting"`为[页面设置](#页面设置)，其值为`对象`，包含了刷新周期、显示总时长等信息，每个页面的`"seting"`不可省略！  
`"display"`为[显示数据](#显示数据)，其值为`数组`，包含了频幕上的显示元素，数组为`对象`的数组，每一个`对象`都是页面上显示的一个元素。`"display"`可省略，省略后OLED显示空白页面(什么都不显示)

### 页面设置

### 显示数据

# 引用
---
 * json解析库cJSON:[DaveGamble/cJSON](https://github.com/DaveGamble/cJSON)
 * SSD1306驱动库:[deeplyembeddedWP/SSD1306-OLED-display-driver-for-BeagleBone](https://github.com/deeplyembeddedWP/SSD1306-OLED-display-driver-for-BeagleBone)
