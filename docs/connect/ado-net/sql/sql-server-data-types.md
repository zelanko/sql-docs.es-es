---
title: Tipos de datos de SQL Server en ADO.NET
description: Describe cómo trabajar con tipos de datos de SQL Server y cómo interactúan con los tipos de datos de .NET.
ms.date: 08/15/2019
ms.assetid: 81b43550-23e8-43bb-b460-7eb8ac825c33
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: 57e0cec178c407cda530e6699e51743094c57dca
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725596"
---
# <a name="sql-server-data-types-and-adonet"></a>Tipos de datos de SQL Server en ADO.NET

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

SQL Server y .NET se basan en sistemas de tipos diferentes, lo que puede dar lugar a una posible pérdida de datos. Para conservar la integridad de los datos, el proveedor de datos SqlClient de Microsoft para SQL Server (<xref:Microsoft.Data.SqlClient>) proporciona métodos de descriptor de acceso con tipo para trabajar con datos de SQL Server. Puede usar las enumeraciones de las clases <xref:System.Data.SqlDbType> para especificar tipos de datos <xref:Microsoft.Data.SqlClient.SqlParameter>.  
  
SQL Server 2008 introduce nuevos tipos de datos que están diseñados para satisfacer las necesidades empresariales de trabajar con datos de fecha y hora, estructurados, semiestructurados y no estructurados. Están documentados en los Libros en pantalla de SQL Server 2008.  
  
Los tipos de datos de SQL Server que están disponibles para su uso en la aplicación dependen de la versión de SQL Server que esté usando. Para obtener más información, vea [Tipo de datos (motor de base de datos) ](/previous-versions/sql/sql-server-2008-r2/ms187594(v=sql.105)) en los Libros en pantalla de SQL Server.
  
## <a name="in-this-section"></a>En esta sección  
[SqlTypes y DataSet](sqltypes-dataset.md)  
Describe la compatibilidad de tipos con `SqlTypes` en `DataSet`.  
  
[Tratamiento de valores NULL](handle-null-values.md)  
Demuestra cómo trabajar con valores NULL y la lógica de tres valores.  
  
[Comparación de valores GUID y uniqueidentifier](compare-guid-uniqueidentifier-values.md)  
Muestra cómo trabajar con valores GUID y de identificador único en SQL Server y .NET.  
  
[Datos de fecha y hora](date-time-data.md)  
Describe cómo usar los nuevos tipos de datos de hora y fecha incorporados en SQL Server 2008.  
  
[UDT grandes](large-udts.md)  
Muestra cómo recuperar datos de UDT de valores grandes introducidos en SQL Server 2008.  
  
[Datos XML en SQL Server](xml-data-sql-server.md)  
Muestra cómo recuperar datos XML recuperados de SQL Server y cómo trabajar con ellos.  
  
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