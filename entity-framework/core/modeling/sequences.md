---
title: 序列-EF Core
author: roji
ms.date: 12/18/2019
ms.assetid: 94f81a92-3c72-4e14-912a-f99310374e42
uid: core/modeling/sequences
ms.openlocfilehash: 6343e58dd79837cc69308a070c9814030505d7dd
ms.sourcegitcommit: 32c51c22988c6f83ed4f8e50a1d01be3f4114e81
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/27/2019
ms.locfileid: "75502437"
---
# <a name="sequences"></a>序列

> [!NOTE]  
> 序列是通常仅由关系数据库支持的功能。 如果使用的是非关系数据库（如 Cosmos），请查看数据库文档以生成唯一值。

序列将在数据库中生成唯一的顺序数值。 序列不与特定表相关联，并且可以将多个表设置为从同一序列中绘制值。

## <a name="basic-usage"></a>基本用法

您可以在模型中设置一个序列，然后使用它来生成属性值：

[!code-csharp[Main](../../../samples/core/Modeling/FluentAPI/Sequence.cs?name=Sequence&highlight=3,7)]

请注意，用于从序列生成值的特定 SQL 是特定于数据库的;上面的示例可在 SQL Server 上运行，但在其他数据库中将失败。 有关详细信息，请参阅特定数据库的文档。

## <a name="configuring-sequence-settings"></a>配置序列设置

你还可以配置序列的其他方面，例如其架构、起始值、增量等：

[!code-csharp[Main](../../../samples/core/Modeling/FluentAPI/SequenceConfiguration.cs?name=SequenceConfiguration&highlight=3-5)]
