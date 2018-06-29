# IPEIT.TemplateResolver

This is a tiny library for getting full path to the directory containing template files.

## Install

If you have only one project in your solution:
```
PM> Install-Package IPEIT.TemplateResolver.Start
```

Otherwise, install the *Start* package in the project where your template files will be stored.
And in the other projects where you need access to the template files install the following package:
```
PM> Install-Package IPEIT.TemplateResolver
```


## Configure
If your project contains the *(App.config)* cofiguration file, then after installation of the 
*Start package* the following line have to appear in the `appSettings` section:
```
<add key="WebFramework.TemplatesPath" value="..\..\TemplateFiles" />
```
If not, add it manually.

The *value* of this configuration is pointing to the directory of your template files. 
This path is relative to the binary files of your program.
Usualy it's *bin* folder in ASP.NET or *bin/Debug* in colnsole apps.
Change this value as you like or leave it as is.

Then, you should create that folder and place files you need.

At this point cofiguration of library is over.

## Usage

Let's assume that you placed *readme.txt* file in the template files directory.
Then, you can get full path to that file using the following line of code:

```C#
var path = TemplateResolver.ResolveFilePath("readme.txt");
Console.WriteLine(path);
```

or you can do it even simpler:

```C#
var path = TemplateResolver.ResolveFilePath("readme");
Console.WriteLine(path);
```

All methods you need are placed in `TemplateResolver` (static) class.
Don't forget to add namespaces:
```C#
using IPEIT.TemplateResolver;
```

You can skip writing extensions of files when pointing to the file you want to get full path of.
In the current version, you can miss the following file extensions:
```
txt|pdf|rtf|ppt|pptx|xls|xlsx|doc|docx
```

Feel free to create subdirectories in the directory where you store your template files. 
You can access file's path in subdirectories with the following code:

```C#
var path = TemplateResolver.ResolveFilePath("subdirectory\\readme");
Console.WriteLine(path);
```

You can get path to the root directory with templates using `TemplateResolver.GetTemplatesDir()` method.
