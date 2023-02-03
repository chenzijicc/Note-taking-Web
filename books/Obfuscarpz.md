#### Obfuscar配置
Visual Studio 2019
1.解决方案资源管理器，找到依赖项，右键打开NuGet包管理
2.点击浏览，搜索Obfuscar安装
3.项目根目录新建obfuscar.xml
4.修改配置为：
```xml
<?xml version="1.0" encoding="utf-8" ?>
		<Obfuscator>
		<!--输入路径-->
		<Var name="InPath" value="." />
		<!--输出路径:加密混淆过的路径-->
		<Var name="OutPath" value=".\Obfuscator_Output" />
		<!--混淆代码的参数-->
		<Var name="KeepPublicApi" value="true" />
		<Var name="HidePrivateApi" value="true" />
		<Var name="HideStrings" value="false" />
		<Var name="UseUnicodeNames" value="true" />
		<Var name="ReuseNames" value="true" />
		<Var name="RenameFields" value="true" />
		<Var name="RegenerateDebugInfo" value="true" />
		<!--要混淆的模块文件 编辑器默认会复制到输出目录-->
		<Module file="$(InPath)\fileencryption.dll" />
		</Obfuscator>
```
6.项目右键属性，打开生成事件->在生成后事件命令行中填入
```shell
set "str=$(ConfigurationName)" if "%str%"=="Release" (CD $(TargetDir)"$(Obfuscar)" obfuscar.xmlxcopy Obfuscator_Output\*.dll   /y /e /i /qxcopy Obfuscator_Output\*.exe   /y /e /i /q)
```
7.右键项目点击生成，编译项目
8.找到依赖项-->包-->Obfuscar右键在文件管理器中打开
9.复制Obfuscar.Console.exe 到程序打包输出目录
10.在cmd中运行Obfuscar.Console.exe obfuscar.xml
11.将生成的加密文件整合到软件一起