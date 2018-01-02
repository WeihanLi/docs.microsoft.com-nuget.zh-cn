---
title: "NuGet CLI 安装命令 |Microsoft 文档"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 59ac622f-837c-4545-bc93-a56330e02d71
description: "Nuget.exe 安装命令的引用"
keywords: "nuget 安装引用，安装包命令"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 88c123a7f2a3d628713cefcc4b110fb0205093b4
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2017
---
# <a name="install-command-nuget-cli"></a>安装命令 (NuGet CLI)

**适用于：**打包消耗&bullet;**受支持的版本：**所有

下载并安装到项目中，默认设置为当前文件夹中，使用指定的包源的包。

> [!Tip]
> 若要下载的项目上下文之外直接程序包，请访问包的页面上[nuget.org](https://www.nuget.org)和选择**下载**链接。 

如果未不指定任何源，这些文件中列出全局配置， `%APPDATA%\NuGet\NuGet.Config`，使用。 请参阅[配置 NuGet 行为](../consume-packages/configuring-nuget-behavior.md)有关其他详细信息。

如果未不指定任何特定的包，`install`安装在项目中列出的所有包`packages.config`文件，使它类似于[ `restore` ](#restore)。 (`install`命令不适用于`project.json`。)

`install`命令不会修改项目文件或`packages.config`; 在这种方式很类似于`restore`，因为它只将包添加到磁盘，但不会更改项目的依赖关系。

若要添加依赖关系，请在 Visual Studio 中，添加通过程序包管理器 UI 或控制台项目，或者修改`packages.config`，然后运行或者`install`或`restore`。 对于项目使用`project.json`，你可以修改该文件，然后运行`restore`。

## <a name="usage"></a>用法

```
nuget install <packageID | configFilePath> [options]
```

其中`<packageID>`命名要安装 （使用最新版本） 的包或`<configFilePath>`标识`packages.config`列出要安装的包文件。 你可以指示特定版本与`-Version`选项。

## <a name="options"></a>选项

| 选项 | 描述 |
| --- | --- |
| ConfigFile | *（2.5 +)* NuGet 要应用的配置文件。 如果未指定， *%AppData%\NuGet\NuGet.Config*使用。 |
| DisableParallelProcessing | 禁用并行安装多个包。 |
| ExcludeVersion | 将包安装到名为仅的包名称和不的版本号的文件夹。 |
| FallbackSource | *（3.2 +)*要用作回退机制，以防主键中找不到包的包源的列表或默认源。 |
| ForceEnglishOutput | *（3.5 +)*强制 nuget.exe 运行使用固定的、 基于英语的区域性。 |
| 框架 | *（4.4 +)*用于选择依赖关系的目标框架。 默认值为任何如果未指定。 |
| 帮助 | 显示的帮助命令的信息。 |
| NoCache | 防止 NuGet 使用从本地计算机缓存的包。 |
| 非交互式 | 取消显示提示用户输入或确认。 |
| 输出目录 | 指定在其中安装包的文件夹。 如果未不指定任何文件夹，则使用当前文件夹。 |
| PackageSaveMode | 指定要保存包安装完成后的文件类型： 之一`nuspec`， `nupkg`，或`nuspec;nupkg`。 |
| 预发行版 | 允许要安装预发行程序包。 还原的包时，此标志不是必需`packages.config`。 |
| RequireConsent | 验证还原程序包启用了之前下载和安装包。 有关详细信息，请参阅[程序包还原](../consume-packages/package-restore.md)。 |
| SolutionDirectory | 指定为其还原包解决方案的根文件夹。 |
| 源 | 指定包源的列表 （作为 Url) 使用。 如果省略，则该命令使用在配置文件中提供的源，请参阅[配置 NuGet 行为](../Consume-Packages/Configuring-NuGet-Behavior.md)。 |
| 详细级别 | 指定的输出中显示的详细信息量：*正常*， *quiet*，*详细 （2.5 +）*。 |
| 版本 | 指定要安装的包的版本。 |

另请参阅[环境变量](cli-ref-environment-variables.md)

## <a name="examples"></a>示例

```
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```