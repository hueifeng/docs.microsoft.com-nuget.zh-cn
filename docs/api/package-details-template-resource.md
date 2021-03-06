---
title: 包详细信息 URL 模板，NuGet API
description: "\"包详细信息 URL\" 模板允许客户端在其 UI 中显示指向更多包详细信息的 web 链接"
author: joelverhagen
ms.author: jver
ms.date: 3/1/2019
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 1b84c6e88a56216e5747d5bc602219af6695c305
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/29/2020
ms.locfileid: "76812930"
---
# <a name="package-details-url-template"></a>包详细信息 URL 模板

客户端可能会生成一个 URL，用户可以使用该 URL 在其 web 浏览器中查看更多包详细信息。 当包源要显示与 NuGet 客户端应用程序所显示的范围不匹配的包的其他信息时，这非常有用。

用于生成此 URL 的资源是在[服务索引](service-index.md)中找到的 `PackageDetailsUriTemplate` 资源。

## <a name="versioning"></a>版本管理

使用以下 `@type` 值：

@type 值                     | 注释
------------------------------- | -----
PackageDetailsUriTemplate/5.1.0 | 初始版本

## <a name="url-template"></a>URL 模板

以下 API 的 URL 是 `@id` 属性的值，该属性与前面提到的一个资源 `@type` 值相关联。

## <a name="http-methods"></a>HTTP 方法

尽管客户端不打算代表用户向包详细信息 URL 发出请求，但网页应支持 `GET` 方法，以便在 web 浏览器中轻松地打开已单击的 URL。

## <a name="construct-the-url"></a>构造 URL

给定已知的包 ID 和版本，客户端实现可以构造用于访问 web 界面的 URL。 客户端实现应向用户显示此构造的 URL （或可单击的链接），以允许用户通过 web 浏览器打开 URL 并了解有关包的详细信息。 包详细信息页的内容由服务器实现确定。

URL 必须是绝对 URL，方案（协议）必须为 HTTPS。

服务索引中 `@id` 的值是包含以下任何占位符标记的 URL 字符串：

### <a name="url-placeholders"></a>URL 占位符

Name        | 类型    | 必需 | 注释
----------- | ------- | -------- | -----
`{id}`      | string  | no       | 要获取其详细信息的包 ID
`{version}` | string  | no       | 要获取其详细信息的包版本

服务器应接受任意大小写形式的 `{id}` 和 `{version}` 值。 此外，服务器不应对版本是否[规范化](../concepts/package-versioning.md#normalized-version-numbers)敏感。 换句话说，服务器还应接受非标准化版本。

例如，nuget 的包详细信息模板如下所示：

    https://www.nuget.org/packages/{id}/{version}

如果客户端实现需要显示4.3.0 的包详细信息的链接，它将生成以下 URL，并将其提供给用户：

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0
