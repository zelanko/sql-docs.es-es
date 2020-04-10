---
title: Valores de columna de SQL XML
description: Muestra cómo recuperar datos XML recuperados de SQL Server y cómo trabajar con ellos.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: d97ce4da-f09c-4d1e-85b7-a0ccedd7246a
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: 2704ceae26c58edc85b0cbc1f0fbe6cc98f64311
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80902017"
---
# <a name="sql-xml-column-values"></a>Valores de columna de SQL XML

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

SQL Server admite el tipo de datos `xml` y los desarrolladores pueden recuperar conjuntos de resultados que incluyan este tipo mediante el comportamiento estándar de la clase <xref:Microsoft.Data.SqlClient.SqlCommand>. Una columna `xml` se puede recuperar tal como se recupera cualquier columna (en <xref:Microsoft.Data.SqlClient.SqlDataReader>, por ejemplo), pero si desea trabajar con el contenido de la columna como XML, debe usar <xref:System.Xml.XmlReader>.  
  
## <a name="example"></a>Ejemplo  
La siguiente aplicación de consola selecciona dos filas, cada una de las cuales contiene una columna `xml`, de la tabla **Sales.Store** de la base de datos **AdventureWorks** para una instancia <xref:Microsoft.Data.SqlClient.SqlDataReader>. Para cada fila, se lee el valor de la columna `xml` mediante el método <xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlXml%2A> de <xref:Microsoft.Data.SqlClient.SqlDataReader>. El valor se almacena en <xref:System.Xml.XmlReader>. Tenga en cuenta que debe usar <xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlXml%2A> en lugar del método <xref:System.Data.IDataRecord.GetValue%2A> si desea establecer el contenido en una variable <xref:System.Data.SqlTypes.SqlXml>; <xref:System.Data.IDataRecord.GetValue%2A> devuelve el valor de la columna `xml` como una cadena.  
  
> [!NOTE]
>  De forma predeterminada, la base de datos de ejemplo **AdventureWorks** no se instala al instalar SQL Server. Puede instalarlo mediante la ejecución del programa de instalación de SQL Server.  
  
[!code-csharp [SqlDataReader_GetSqlXml#1](~/../sqlclient/doc/samples/SqlDataReader_GetSqlXml.cs#1)]
  
## <a name="next-steps"></a>Pasos siguientes
- <xref:System.Data.SqlTypes.SqlXml>
- [Datos XML en SQL Server](xml-data-sql-server.md)
