---
ms.openlocfilehash: ef54f102352a3d088181ad6f7c356b8c7eeac166
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/07/2020
ms.locfileid: "74825166"
---
使用 [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) 命令还原项目文件中列出的包（请参阅 [PackageReference](../../consume-packages/package-references-in-project-files.md)）。 使用 .NET Core 2.0 和更高版本，通过 `dotnet build` 和 `dotnet run` 自动完成还原。 从 NuGet 4.0 开始，它运行与 `nuget restore` 相同的代码。

与其他 `dotnet` CLI 命令一样，先打开命令行并切换到包含项目文件的目录。

要使用 `dotnet restore` 还原包：

```dotnetcli
dotnet restore 
```