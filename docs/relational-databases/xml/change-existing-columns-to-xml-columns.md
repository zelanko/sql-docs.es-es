---
title: Cambio de columnas existentes a columnas XML | Microsoft Docs
description: Aprenda a usar la instrucción ALTER TABLE para cambiar una columna de tipo cadena a una columna de tipo de datos XML.
ms.custom: fresh2019may
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- tables [XML]
ms.assetid: 0d951424-9862-41fe-bd46-127f1c059bcb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 801b762b80dd081e309d8c7d8569b0302d505dbd
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85775613"
---
# <a name="change-existing-columns-to-xml-columns"></a>Cambiar columnas existentes a columnas XML

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

La instrucción ALTER TABLE admite el tipo de datos **xml** . Por ejemplo, puede cambiar cualquier columna de tipo de cadena al tipo de datos **xml** . Tenga en cuenta que, en estos casos, los documentos contenidos en la columna deben tener un formato correcto. Asimismo, si cambia el tipo de la columna de cadena a xml con tipo, los documentos de la columna se validarán con los esquemas XSD especificados.  
  
```sql
CREATE TABLE T (Col1 int primary key, Col2 nvarchar(max));
GO  
INSERT INTO T   
  VALUES (1, '<Root><Product ProductID="1"/></Root>');
GO  
ALTER TABLE T   
  ALTER COLUMN Col2 xml;
```  
  
Puede cambiar una columna de tipo `xml` de XML sin tipo a XML con tipo. Por ejemplo:  
  
```sql
CREATE TABLE T (Col1 int primary key, Col2 xml);
GO  
INSERT INTO T   
  values (1, '<p1:ProductDescription ProductModelID="1"   
xmlns:p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">  
            </p1:ProductDescription>');
GO   
-- Make it a typed xml column by specifying a schema collection.  
ALTER TABLE T   
  ALTER COLUMN Col2 xml (Production.ProductDescriptionSchemaCollection);
```  
  
> [!NOTE]  
> el script se ejecutará sobre la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] porque la colección de esquemas XML, `Production.ProductDescriptionSchemaCollection`, se crea como parte de la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
 En el ejemplo anterior, todas las instancias almacenadas en la columna se validan y se les asigna un tipo con los esquemas XSD de la colección especificada. Si la columna contiene una o varias instancias XML no válidas respecto al esquema especificado, la instrucción `ALTER TABLE` no se ejecutará y no podrá cambiar la columna XML sin tipo a XML con tipo.  
  
> [!NOTE]  
> Si una tabla es de gran tamaño, la modificación de una columna de tipo **xml** puede resultar costosa. Esto se debe a que se tiene que comprobar que el formato de cada documento es correcto y, además, se deben validar los de XML con tipo.  
  
Para obtener más información sobre XML con tipo, vea [Comparar XML con tipo y XML sin tipo](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md).  
