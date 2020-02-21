---
title: SqlTypes y DataSet
description: Describe la compatibilidad de tipos para SqlTypes en el conjunto de datos.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 9172c20a-9876-4b3b-9c97-1963c02b1993
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: a7ef43ca6afa243e313e8e38bdd05d929161e71f
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "75233790"
---
# <a name="sqltypes-and-the-dataset"></a>SqlTypes y DataSet

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Descargar ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

ADO.NET 2.0 introdujo la compatibilidad de tipos mejorada con `DataSet` mediante el espacio de nombres <xref:System.Data.SqlTypes>. Los tipos en <xref:System.Data.SqlTypes> se han diseñado para proporcionar tipos de datos con la misma semántica y precisión que los de una base de datos SQL Server. Cada tipo de datos de <xref:System.Data.SqlTypes> tiene un tipo de datos equivalente en SQL Server, con la misma representación de datos subyacente.  
  
El uso de <xref:System.Data.SqlTypes> directamente en <xref:System.Data.DataSet> confiere varias ventajas cuando se trabaja con tipos de datos de SQL Server. <xref:System.Data.SqlTypes> admite la misma semántica que los tipos de datos nativos de SQL Server. Si se especifica uno de los tipos <xref:System.Data.SqlTypes> en la definición de <xref:System.Data.DataColumn>, se elimina la pérdida de precisión que se puede producir al convertir tipos de datos decimales o numéricos a uno de los tipos de datos de Common Language Runtime (CLR).  

En el siguiente ejemplo se crea un objeto <xref:System.Data.DataTable> que define explícitamente los tipos de datos <xref:System.Data.DataColumn> mediante <xref:System.Data.SqlTypes> en lugar de tipos CLR. El código rellena <xref:System.Data.DataTable> con los datos de la tabla Sales.SalesOrderDetail de la base de datos AdventureWorks de SQL Server. La salida mostrada en la ventana de la consola muestra el tipo de datos de cada columna y los valores recuperados de SQL Server.  
  
[!code-csharp[DataWorks DataColumn_DataType#1](~/../sqlclient/doc/samples/DataColumn_DataType.cs#1)]
