---
title: 包内容，NuGet API
description: 包基址是一个简单的接口，用于提取包本身。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 7aea28d6224a89149aa33be035c82a45db3058f0
ms.sourcegitcommit: 1eda83ab537c86cc27316e7bc67f95a358766e63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/18/2019
ms.locfileid: "71094124"
---
# <a name="package-content"></a>包内容

可以使用 V3 API 生成 URL 来提取任意包的内容（nupkg 文件）。 用于提取包内容的资源是在`PackageBaseAddress` [服务索引](service-index.md)中找到的资源。 此资源还允许发现包的所有版本、列出或未列出。

此资源通常称为 "包基址" 或 "平面容器"。

## <a name="versioning"></a>版本管理

使用以下`@type`值：

@type 值              | 说明
------------------------ | -----
PackageBaseAddress/3.0.0 | 初始版本

## <a name="base-url"></a>基 URL

以下 api 的基 URL 是与上述资源`@id` `@type`值关联的属性的值。 在下面的文档中，将使用占位符`{@id}`基 URL。

## <a name="http-methods"></a>HTTP 方法

注册资源中找到的所有 url 都支持 HTTP 方法`GET`和`HEAD`。

## <a name="enumerate-package-versions"></a>枚举包版本

如果客户端知道包 ID 并想要发现包源有哪些包版本可用，则客户端可以构造可预测的 URL 来枚举所有包版本。 此列表应为下述包内容 API 的 "目录列表"。

> [!Note]
> 此列表包含列出和未列出的包版本。

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a>请求参数

name     | 内     | 类型    | 必填 | 说明
-------- | ------ | ------- | -------- | -----
LOWER_ID | URL    | string  | 是      | 包 ID lowercased

`LOWER_ID`值是所需的包 ID lowercased，它使用由实现的规则。NET 的[`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)方法。

### <a name="response"></a>响应

如果包源没有提供的包 ID 版本，则返回404状态代码。

如果包源有一个或多个版本，则返回200状态代码。 响应正文是包含以下属性的 JSON 对象：

name     | 类型             | 必填 | 说明
-------- | ---------------- | -------- | -----
版本 | 字符串数组 | 是      | 可用版本

`versions`数组中的字符串是所有 lowercased 的[规范化 NuGet 版本字符串](../concepts/package-versioning.md#normalized-version-numbers)。 版本字符串不包含任何 SemVer 2.0.0 生成元数据。

目的在于，在此数组中找到的版本字符串可以逐字`LOWER_VERSION`用于以下终结点中的标记。

### <a name="sample-request"></a>示例请求

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a>示例响应

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a>下载包内容（. nupkg）

如果客户端知道包 ID 和版本并想要下载包内容，则它们只需构造以下 URL：

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a>请求参数

name          | 内     | 类型   | 必填 | 说明
------------- | ------ | ------ | -------- | -----
LOWER_ID      | URL    | string | 是      | 包 ID，小写
LOWER_VERSION | URL    | string | 是      | 包版本（正常化和 lowercased）

`LOWER_ID` 和`LOWER_VERSION`都是使用实现的规则 lowercased 的。网络[`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)
方法。

是使用 NuGet 的版本[规范化规则](../concepts/package-versioning.md#normalized-version-numbers)规范化的所需包版本。 `LOWER_VERSION` 这意味着，在这种情况下必须排除 SemVer 2.0.0 规范允许的生成元数据。

### <a name="response-body"></a>响应正文

如果包源上存在包，则返回200状态代码。 响应正文将是包内容本身。

如果包源中不存在包，则返回404状态代码。

### <a name="sample-request"></a>示例请求

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a>示例响应

Newtonsoft.json 的 nupkg 的二进制流。

## <a name="download-package-manifest-nuspec"></a>下载包清单（. nuspec）

如果客户端知道包 ID 和版本并想要下载包清单，则它们只需构造以下 URL：

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a>请求参数

name          | 内     | 类型   | 必需 | 说明
------------- | ------ | ------ | -------- | -----
LOWER_ID      | URL    | string | 是      | 包 ID，小写
LOWER_VERSION | URL    | string | 是      | 包版本（正常化和 lowercased）

`LOWER_ID` 和`LOWER_VERSION`都是使用实现的规则 lowercased 的。NET 的[`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)方法。

是使用 NuGet 的版本[规范化规则](../concepts/package-versioning.md#normalized-version-numbers)规范化的所需包版本。 `LOWER_VERSION` 这意味着，在这种情况下必须排除 SemVer 2.0.0 规范允许的生成元数据。

### <a name="response-body"></a>响应正文

如果包源上存在包，则返回200状态代码。 响应正文将为包清单，即 nuspec 中包含的 nupkg。 Nuspec 是一个 XML 文档。

如果包源中不存在包，则返回404状态代码。

### <a name="sample-request"></a>示例请求

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a>示例响应

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
