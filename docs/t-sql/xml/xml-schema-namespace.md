---
title: xml_schema_namespace (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 07/27/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- xml_schema_namespace_TSQL
- xml_schema_namespace
dev_langs:
- TSQL
helpviewer_keywords:
- XML schema collections [SQL Server], reconstructing schemas
- xml_schema_namespace function
- reconstructing schemas
- schemas [SQL Server], XML
- schema collections [SQL Server], reconstructing schemas
ms.assetid: ee9873d8-dd3a-4bff-a10c-68bbadbdf1a6
caps.latest.revision: 18
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 449e545672192baa9d16204afe1fb23497959094
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="xmlschemanamespace"></a>xml_schema_namespace
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Reconstruye todos los esquemas o un esquema determinado en la colección de esquemas XML especificada. La función devuelve una instancia de tipo de datos **xml** .  
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
xml_schema_namespace( Relational_schema , XML_schema_collection_name , [ Namespace ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Relational_schema*  
 Es el nombre del esquema relacional. *Relational_schema* es **sysname**.  
  
 *XML_schema_collection_name*  
 Es el nombre de la colección de esquemas XML que se va a reconstruir. *XML_schema_collection_name* es **sysname**.  
  
 *Espacio de nombres*  
 Es el URI de espacio de nombres del esquema XML que desea reconstruir. Tiene un límite de 1.000 caracteres. Si no se proporciona ningún URI de espacio de nombres, se reconstruye toda la colección de esquemas XML. *Namespace* es **nvarchar (4000)**.  
  
## <a name="return-types"></a>Tipos devueltos  
 **xml**  
  
## <a name="remarks"></a>Comentarios  
 Al importar componentes del esquema XML en la base de datos mediante [CREATE XML SCHEMA COLLECTION](../../t-sql/statements/create-xml-schema-collection-transact-sql.md) o [ALTER XML SCHEMA COLLECTION](../../t-sql/statements/alter-xml-schema-collection-transact-sql.md), se conservan los aspectos del esquema utilizado para la validación. Por lo tanto, el esquema reconstruido puede no ser léxicamente el mismo que el documento del esquema original. De forma específica, se pierden comentarios, espacios en blanco y anotaciones; asimismo, la información implícita se hace explícita. Por ejemplo, \<xs: element name = "e1" / > se convierte en \<xs: element name = "e1" type = "xs: anyType" / >. Los prefijos de los espacios de nombres no se mantienen.  
  
 Si especifica un parámetro de espacio de nombres, el documento del esquema resultante contendrá definiciones para todos los componentes del esquema en ese espacio de nombres, incluso si se han agregado en diferentes documentos de esquema o pasos de DDL, o ambos.  
  
 No se puede utilizar esta función para construir documentos de esquema XML desde el **sys.sys** colección de esquemas XML.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente recupera la colección de esquemas XML `ProductDescriptionSchemaCollection` desde el esquema relacional de producción en la base de datos `AdventureWorks2012`.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT xml_schema_namespace(N'production',N'ProductDescriptionSchemaCollection');  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Ver una colección de esquemas XML almacenada](../../relational-databases/xml/view-a-stored-xml-schema-collection.md)   
 [Colecciones de esquemas XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-schema-collections-sql-server.md)  
  
  

