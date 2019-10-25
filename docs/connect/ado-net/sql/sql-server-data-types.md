---
title: Tipos de datos de SQL Server en ADO.NET
description: Describe cómo trabajar con tipos de datos de SQL Server y cómo interactúan con los tipos de datos de .NET.
ms.date: 08/15/2019
ms.assetid: 81b43550-23e8-43bb-b460-7eb8ac825c33
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 12ad13d6788ae2b8995289100883b06c5ab6d7c6
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452036"
---
# <a name="sql-server-data-types-and-adonet"></a>Tipos de datos de SQL Server en ADO.NET

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Descargar ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

SQL Server y .NET se basan en sistemas de tipos diferentes, lo que puede dar lugar a una posible pérdida de datos. Para conservar la integridad de los datos, el proveedor de datos SqlClient de Microsoft para SQL Server (<xref:Microsoft.Data.SqlClient>) proporciona métodos de descriptor de acceso con tipo para trabajar con datos de SQL Server. Puede usar las enumeraciones de las clases <xref:System.Data.SqlDbType> para especificar <xref:Microsoft.Data.SqlClient.SqlParameter> tipos de datos.  
  
SQL Server 2008 introduce nuevos tipos de datos que están diseñados para satisfacer las necesidades empresariales de trabajar con datos de fecha y hora, estructurados, semiestructurados y no estructurados. Están documentados en los Libros en pantalla de SQL Server 2008.  
  
Los tipos de datos de SQL Server que están disponibles para su uso en la aplicación dependen de la versión de SQL Server que esté usando. Para obtener más información, vea [tipos de datos (motor de base de datos)](https://go.microsoft.com/fwlink/?LinkID=107468) de libros en pantalla de SQL Server.
  
## <a name="in-this-section"></a>En esta sección  
[SqlTypes y DataSet](sqltypes-dataset.md)  
Describe la compatibilidad de tipos con `SqlTypes` en `DataSet`.  
  
[Tratamiento de valores NULL](handle-null-values.md)  
Muestra cómo trabajar con valores NULL y la lógica de tres valores.  
  
[Comparación de valores GUID y uniqueidentifier](compare-guid-uniqueidentifier-values.md)  
Muestra cómo trabajar con valores GUID y uniqueidentifier en SQL Server y .NET.  
  
[Datos de fecha y hora](date-time-data.md)  
Describe cómo usar los nuevos tipos de datos de fecha y hora introducidos en SQL Server 2008.  
  
[UDT grandes](large-udts.md)  
Muestra cómo recuperar datos de UDT de valor grande introducidos en SQL Server 2008.  
  
[Datos XML en SQL Server](xml-data-sql-server.md)  
Describe cómo trabajar con datos XML recuperados de SQL Server.  
  
## <a name="reference"></a>Referencia  
<xref:System.Data.DataSet>  
Describe la clase `DataSet` y todos sus miembros.  
  
<xref:System.Data.SqlTypes>  
Describe el espacio de nombres `SqlTypes` y todos sus miembros.  
  
<xref:System.Data.SqlDbType>  
Describe la enumeración `SqlDbType` y todos sus miembros.  
  
<xref:System.Data.DbType>  
Describe la enumeración `DbType` y todos sus miembros.  
  
## <a name="next-steps"></a>Pasos siguientes
- [Parámetros con valores de tabla](table-valued-parameters.md)
- [Datos binarios y datos de valores grandes de SQL Server](sql-server-binary-large-value-data.md)
