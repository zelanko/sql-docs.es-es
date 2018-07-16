---
title: Quitar índices XML | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- removing indexes
- dropping indexes
- XML indexes [SQL Server], dropping
ms.assetid: 7591ebea-34af-4925-8553-b2adb5b487c2
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2a6021971575b0a17821e415aaf738ff651e9ec5
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37323975"
---
# <a name="drop-xml-indexes"></a>Quitar índices XML
  La instrucción [DROP INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-index-transact-sql)[!INCLUDE[tsql](../../includes/tsql-md.md)] se puede usar para quitar índices XML y no XML principales y secundarios existentes. No obstante, ninguna opción de DROP INDEX se aplica a los índices XML. Si se quita el índice XML principal, también se eliminarán todos los índices secundarios existentes.  
  
 La sintaxis de DROP con *TableName.IndexName* está desapareciendo y no es compatible con los índices XML.  
  
## <a name="example-creating-and-dropping-a-primary-xml-index"></a>Ejemplo: crear y quitar un índice XML principal  
 En el ejemplo siguiente, se crea un índice XML en un `xml` columna de tipo.  
  
```  
DROP TABLE T  
GO  
CREATE TABLE T (Col1 INT PRIMARY KEY, XmlCol XML)  
GO  
-- Create Primary XML index   
CREATE PRIMARY XML INDEX PIdx_T_XmlCol   
ON T(XmlCol)  
GO  
-- Verify the index creation.   
-- Note index type is 3 for xml indexes.  
-- Note the type 3 is index on XML type.  
SELECT *  
FROM sys.xml_indexes  
WHERE object_id = object_id('T')  
AND name='PIdx_T_XmlCol'   
-- Drop the index.  
DROP INDEX PIdx_T_XmlCol ON T  
```  
  
 Al quitar una tabla, se quitan automáticamente todos los índices XML que contiene. No obstante, una columna XML no puede quitarse desde una tabla si existe un índice XML en la columna.  
  
 En el ejemplo siguiente, se crea un índice XML en un `xml` columna de tipo. Para obtener más información, vea [Comparar XML con tipo y XML sin tipo](../xml/compare-typed-xml-to-untyped-xml.md).  
  
```  
CREATE TABLE TestTable(  
 Col1 int primary key,   
 Col2 xml (Production.ProductDescriptionSchemaCollection))   
GO  
```  
  
 En este momento, puede crear un índice XML principal en `Co12`.  
  
```  
CREATE PRIMARY XML INDEX PIdx_TestTable_Col2   
ON TestTable(Col2)  
GO  
```  
  
## <a name="example-creating-an-xml-index-by-using-the-dropexisting-index-option"></a>Ejemplo: crear un índice XML utilizando la opción de índice DROP_EXISTING  
 El ejemplo siguiente muestra cómo crear un índice XML en una columna (`XmlColx`). A continuación, se creará otro índice XML con el mismo nombre en una columna diferente (`XmlColy`). Dado que se ha especificado la opción `DROP_EXISTING` , el índice XML existente en (`XmlColx)` se quita y se crea un índice XML en (`XmlColy`).  
  
```  
DROP TABLE T  
GO  
CREATE TABLE T(Col1 int primary key, XmlColx xml, XmlColy xml)  
GO  
-- Create XML index on XmlColx.  
CREATE PRIMARY XML INDEX PIdx_T_XmlCol   
ON T(XmlColx)  
GO  
-- Create same name XML index on XmlColy.  
CREATE PRIMARY XML INDEX PIdx_T_XmlCol   
ON T(XmlColy)   
WITH (DROP_EXISTING = ON)  
-- Verify the index is created on XmlColy.d.  
SELECT sc.name   
FROM   sys.xml_indexes si inner join sys.index_columns sic   
ON     sic.object_id=si.object_id and sic.index_id=si.index_id  
INNER  join sys.columns sc on sc.object_id=sic.object_id   
AND    sc.column_id=sic.column_id  
WHERE  si.name='PIdx_T_XmlCol'   
AND    si.object_id=object_id('T')  
```  
  
 Esta consulta devuelve el nombre de la columna en la que el índice XML especificado se ha creado.  
  
## <a name="see-also"></a>Vea también  
 [Índices XML &#40;SQL Server&#41;](xml-indexes-sql-server.md)  
  
  
