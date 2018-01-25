---
title: DROP XML SCHEMA COLLECTION (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 11/25/2015
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP XML SCHEMA COLLECTION
- DROP_XML_SCHEMA_COLLECTION_TSQL
dev_langs: TSQL
helpviewer_keywords:
- deleting XML schema collections
- XML schema collections [SQL Server], removing
- schema collections [SQL Server], removing
- removing XML schema collections
- dropping XML schema collections
- DROP XML SCHEMA COLLECTION statement
ms.assetid: d686f2f5-e03a-4ffe-a566-6036628f46f1
caps.latest.revision: "15"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 01ee022bf8d9cb03b6f3fb47451c969955b5c255
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="drop-xml-schema-collection-transact-sql"></a>DROP XML SCHEMA COLLECTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Elimina toda la colección de esquemas XML y todos sus componentes.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DROP XML SCHEMA COLLECTION [ relational_schema. ]sql_identifier  
```  
  
## <a name="arguments"></a>Argumentos  
 *relational_schema*  
 Identifica el nombre del esquema relacional. Si no se especifica, se usará el esquema relacional predeterminado.  
  
 *sql_identifier*  
 Es el nombre de la colección de esquemas XML que se va a quitar.  
  
## <a name="remarks"></a>Comentarios  
 La eliminación de una colección de esquemas XML es una operación transaccional. Esto significa que si quita una colección de esquemas XML de una transacción y, después, revierte la transacción, no se quitará la colección de esquemas XML.  
  
 No podrá quitar una colección de esquemas XML cuando esté en uso. Esto significa que la colección que se desea quitar no puede cumplir ninguna de las condiciones siguientes:  
  
-   Asociada a cualquier **xml** columna o parámetro de tipo.  
  
-   Estar especificada en restricciones de tabla.  
  
-   Estar referenciada en una función enlazada a esquema o a un procedimiento almacenado. Por ejemplo, la función siguiente bloqueará la colección de esquemas XML `MyCollection` porque la función especifica `WITH SCHEMABINDING`. Si la quita, no habrá ningún bloqueo en XML SCHEMA COLLECTION.  
  
    ```  
    CREATE FUNCTION dbo.MyFunction()  
    RETURNS int  
    WITH SCHEMABINDING  
    AS  
    BEGIN  
       ...  
       DECLARE @x XML(MyCollection)  
       ...  
    END;  
    ```  
  
## <a name="permissions"></a>Permissions  
 Para quitar una colección de esquemas XML (XML SCHEMA COLLECTION) es necesario el permiso DROP sobre la colección.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se muestra cómo eliminar una colección de esquemas XML.  
  
```  
DROP XML SCHEMA COLLECTION ManuInstructionsSchemaCollection;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Crear colección de esquemas XML &#40; Transact-SQL &#41;](../../t-sql/statements/create-xml-schema-collection-transact-sql.md)   
 [ALTER XML SCHEMA COLLECTION &#40; Transact-SQL &#41;](../../t-sql/statements/alter-xml-schema-collection-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [Comparar XML con tipo y XML sin tipo](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [Requisitos y limitaciones de las colecciones de esquemas XML en el servidor](../../relational-databases/xml/requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
