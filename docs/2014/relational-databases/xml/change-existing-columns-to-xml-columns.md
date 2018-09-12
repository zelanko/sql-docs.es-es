---
title: Cambio de columnas existentes a columnas XML | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- tables [XML]
ms.assetid: 0d951424-9862-41fe-bd46-127f1c059bcb
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ef71809c5d54fff77bed4ff3a1fd7c9b471337b7
ms.sourcegitcommit: 2666ca7660705271ec5b59cc5e35f6b35eca0a96
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2018
ms.locfileid: "43889371"
---
# <a name="change-existing-columns-to-xml-columns"></a>Cambiar columnas existentes a columnas XML
  La instrucción ALTER TABLE admite el `xml` tipo de datos. Por ejemplo, puede modificar cualquier columna de tipo de cadena para el `xml` tipo de datos. Tenga en cuenta que, en estos casos, los documentos contenidos en la columna deben tener un formato correcto. Asimismo, si cambia el tipo de la columna de cadena a xml con tipo, los documentos de la columna se validarán con los esquemas XSD especificados.  
  
```  
CREATE TABLE T (Col1 int primary key, Col2 nvarchar(max))  
GO  
INSERT INTO T   
VALUES (1, '<Root><Product ProductID="1"/></Root>')  
GO  
ALTER TABLE T   
ALTER COLUMN Col2 xml  
GO  
```  
  
 Puede cambiar una columna de tipo `xml` de XML sin tipo a XML con tipo. Por ejemplo:  
  
```  
CREATE TABLE T (Col1 int primary key, Col2 xml)  
GO  
INSERT INTO T   
values (1, '<p1:ProductDescription ProductModelID="1"   
xmlns:p1="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">  
            </p1:ProductDescription>')  
GO   
-- Make it a typed xml column by specifying a schema collection.  
ALTER TABLE T   
ALTER COLUMN Col2 xml (Production.ProductDescriptionSchemaCollection)  
GO  
```  
  
> [!NOTE]  
>  el script se ejecutará sobre la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] porque la colección de esquemas XML, `Production.ProductDescriptionSchemaCollection`, se crea como parte de la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
 En el ejemplo anterior, todas las instancias almacenadas en la columna se validan y se les asigna un tipo con los esquemas XSD de la colección especificada. Si la columna contiene una o varias instancias XML no válidas respecto al esquema especificado, la instrucción `ALTER TABLE` no se ejecutará y no podrá cambiar la columna XML sin tipo a XML con tipo.  
  
> [!NOTE]  
>  Si una tabla es grande, modificando un `xml` columna de tipo puede ser costoso. Esto se debe a que se tiene que comprobar que el formato de cada documento es correcto y, además, se deben validar los de XML con tipo.  
  
 Para obtener más información sobre XML con tipo, vea [Comparar XML con tipo y XML sin tipo](compare-typed-xml-to-untyped-xml.md).  
  
  
