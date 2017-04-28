---
title: "Ver una colección de esquemas XML almacenada | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- schema collections [SQL Server], viewing
- XML schemas [SQL Server], viewing
- CREATE XML SCHEMA COLLECTION statement
- xml_schema_namespace function
- XML schema collections [SQL Server], viewing
- displaying XML schema collections
- viewing XML schema collections
ms.assetid: e38031af-22df-4cd9-a14e-e316b822f91b
caps.latest.revision: 30
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2bacfd298e992c64739442605f986afffefdb443
ms.lasthandoff: 04/11/2017

---
# <a name="view-a-stored-xml-schema-collection"></a>Ver una colección de esquemas XML almacenada
  Después de importar una colección de esquemas XML mediante [CREATE XML SCHEMA COLLECTION](../../t-sql/statements/create-xml-schema-collection-transact-sql.md), los componentes del esquema se almacenan en los metadatos. Puede usar la función intrínseca [xml_schema_namespace](../../t-sql/xml/xml-schema-namespace.md)para reconstruir la colección de esquemas XML. La función devuelve una instancia de tipo de datos **xml** .  
  
 Por ejemplo, la siguiente consulta recupera una colección de esquemas XML (`ProductDescriptionSchemaCollection`) del esquema relacional de producción de la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
```  
SELECT xml_schema_namespace(N'Production',N'ProductDescriptionSchemaCollection')  
GO  
```  
  
 Si solo quiere ver un esquema de la colección de esquemas XML, puede especificar XQuery en el resultado de tipo **xml** devuelto por `xml_schema_namespace`.  
  
```  
SELECT xml_schema_namespace(N'RelationalSchemaName',N'XmlSchemaCollectionName').query('  
/xs:schema[@targetNamespace="TargetNameSpace"]  
')  
GO  
```  
  
 La siguiente consulta, por ejemplo, recupera información de garantía del producto y de mantenimiento del esquema XML a partir de la colección de esquemas XML `ProductDescriptionSchemaCollection` .  
  
```  
SELECT xml_schema_namespace(N'Production',N'ProductDescriptionSchemaCollection').query('  
/xs:schema[@targetNamespace="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain"]  
')  
GO  
```  
  
 También puede pasar el espacio de nombres de destino opcional como tercer parámetro a la función `xml_schema_namespace` con el fin de recuperar un esquema específico de la colección, tal y como muestra la consulta siguiente:  
  
```  
SELECT xml_schema_namespace(N'Production',N'ProductDescriptionSchemaCollection', N'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain')  
GO  
```  
  
 Al crear una colección de esquemas XML mediante CREATE XML SCHEMA COLLECTION en la base de datos, la instrucción almacena los componentes de esquema en los metadatos. Observe que solo se almacenarán aquellos componentes de esquema que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pueda interpretar. No se almacenarán comentarios, anotaciones ni atributos que no sean XSD. Por tanto, el esquema reconstruido por **xml_schema_namespace** será funcionalmente equivalente al esquema original, pero no tendrá necesariamente la misma apariencia. Por ejemplo, no se observarán los mismos prefijos del esquema original. El esquema devuelto por **xml_schema_namespace** usa **t** como el prefijo para el espacio de nombres de destino y **ns1**, **ns2**, etc., para otros espacios de nombres.  
  
 Si desea conservar una copia idéntica de los esquemas XML, debería guardarlos en un archivo o en una tabla de base de datos en una columna de tipo **xml** .  
  
 La vista de catálogo [sys.xml_schema_collections](../../relational-databases/system-catalog-views/sys-xml-schema-collections-transact-sql.md) también devuelve información sobre las colecciones de esquemas XML. La información consiste en el nombre la colección, la fecha de creación y el nombre del propietario.  
  
## <a name="see-also"></a>Vea también  
 [Colecciones de esquemas XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-schema-collections-sql-server.md)  
  
  
