---
title: SqlTypes y DataSet
description: Describe la compatibilidad de tipos para SqlTypes en el conjunto de DataSet.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 9172c20a-9876-4b3b-9c97-1963c02b1993
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 70efb8615a70677c709abd6d9129c63de9420ffc
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/16/2019
ms.locfileid: "72451985"
---
# <a name="sqltypes-and-the-dataset"></a>SqlTypes y DataSet

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Descargar ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

ADO.NET 2,0 presentó compatibilidad con tipos mejorados para el `DataSet` a través del espacio de nombres <xref:System.Data.SqlTypes>. Los tipos de <xref:System.Data.SqlTypes> están diseñados para proporcionar tipos de datos con la misma semántica y precisión que los tipos de datos de una base de datos de SQL Server. Cada tipo de datos de <xref:System.Data.SqlTypes> tiene un tipo de datos equivalente en SQL Server, con la misma representación de datos subyacente.  
  
El uso de <xref:System.Data.SqlTypes> directamente en una <xref:System.Data.DataSet> confiere varias ventajas cuando se trabaja con tipos de datos de SQL Server. <xref:System.Data.SqlTypes> admite la misma semántica que SQL Server tipos de datos nativos. Si se especifica uno de los <xref:System.Data.SqlTypes> en la definición de un <xref:System.Data.DataColumn>, se elimina la pérdida de precisión que se puede producir al convertir tipos de datos decimales o numéricos a uno de los tipos de datos de Common Language Runtime (CLR).  

En el siguiente ejemplo se crea un objeto <xref:System.Data.DataTable> que define explícitamente los tipos de datos <xref:System.Data.DataColumn> mediante <xref:System.Data.SqlTypes> en lugar de tipos CLR. El código rellena <xref:System.Data.DataTable> con los datos de la tabla Sales.SalesOrderDetail de la base de datos AdventureWorks de SQL Server. La salida mostrada en la ventana de la consola muestra el tipo de datos de cada columna y los valores recuperados de SQL Server.  
  
[!code-csharp[DataWorks DataColumn_DataType#1](~/../sqlclient/doc/samples/DataColumn_DataType.cs#1)]
