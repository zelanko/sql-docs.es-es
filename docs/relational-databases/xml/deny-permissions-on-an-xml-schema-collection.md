---
title: Revocación de los permisos en una colección de esquemas XML | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- denying permissions [SQL Server], XML server collections
ms.assetid: e2b300b0-e734-4c43-a4da-c78e6e5d4fba
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 068701e16d192ca5edfb45267ebee0cece3619a8
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "68052281"
---
# <a name="deny-permissions-on-an-xml-schema-collection"></a>Denegar permisos en una colección de esquemas XML
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Es posible denegar permisos para crear una colección de esquemas XML nueva o utilizar una existente.  
  
## <a name="denying-permission-to-create-an-xml-schema-collection"></a>Denegar permisos para crear una colección de esquemas XML  
 Puede denegar los permisos para crear una colección de esquemas XML del modo siguiente:  
  
-   Denegar el permiso ALTER en el esquema relacional.  
  
-   Denegar el permiso CONTROL en el esquema relacional para denegar todos los permisos en el esquema relacional y en todos los objetos incluidos.  
  
-   Denegar el permiso ALTER ANY SCHEMA en la base de datos. En este caso, la entidad de seguridad no puede crear una colección de esquemas XML en ninguna parte de la base de datos. Observe que al denegar los permisos ALTER o CONTROL en la base de datos, se denegarán todos los permisos en todos los objetos de la base de datos.  
  
## <a name="denying-permissions-on-an-xml-schema-collection-object"></a>Denegar permisos en un objeto de colección de esquemas XML  
 A continuación, se enumeran los permisos que pueden denegarse en una colección de esquemas XML y los resultados:  
  
-   Denegar el permiso ALTER deniega a la entidad de seguridad la posibilidad de modificar el contenido de la colección de esquemas XML.  
  
-   Denegar el permiso CONTROL deniega a la entidad de seguridad la posibilidad de efectuar cualquier operación en la colección de esquemas XML.  
  
-   Denegar el permiso REFERENCES deniega a la entidad de seguridad la posibilidad de escribir o restringir parámetros y columnas de tipo xml utilizando la colección de esquemas XML. También deniega a la entidad de seguridad la posibilidad de consultar esta colección de esquemas XML desde otras colecciones de esquemas XML.  
  
-   Denegar el permiso VIEW DEFINITION deniega a la entidad de seguridad la posibilidad de ver el contenido de una colección de esquemas XML.  
  
-   Denegar el permiso EXECUTE deniega a la entidad de seguridad la posibilidad de insertar o actualizar los valores de las columnas, variables y parámetros que se escriben o limitan por parte de la colección de esquemas XML. También deniega a la entidad de seguridad la posibilidad de consultar los valores en las mismas variables y columnas de tipo xml.  
  
## <a name="examples"></a>Ejemplos  
 Los escenarios de los ejemplos siguientes muestran el funcionamiento de los permisos de los esquemas XML En cada ejemplo se crea la base de datos de prueba, los esquemas relacionales y los inicios de sesión necesarios. A estos inicios de sesión se les conceden los permisos necesarios para la colección de esquemas XML. Al final, cada ejemplo realiza las operaciones de limpieza necesarias.  
  
### <a name="a-preventing-a-user-from-creating-an-xml-schema-collection"></a>A. Evitar que un usuario cree una colección de esquemas XML  
 Una de las formas de evitar que un usuario cree una colección de esquemas XML consiste en denegar el permiso ALTER en un esquema relacional. Esto se muestra en el ejemplo siguiente.  
  
 El ejemplo crea un usuario, `TestLogin1`, y una base de datos. Además del esquema `dbo` , también se crea un esquema relacional en la base de datos. Inicialmente, el permiso `CREATE XML SCHEMA` permite al usuario crear una colección de esquemas en cualquier lugar de la base de datos. A continuación, se deniega el permiso `ALTER` al usuario en uno de los esquemas relacionales. Esto impide al usuario crear una colección de esquemas XML en ese esquema relacional.  
  
```  
CREATE LOGIN TestLogin1 WITH password='SQLSvrPwd1'  
GO  
CREATE DATABASE SampleDBForSchemaPermissions  
GO  
USE SampleDBForSchemaPermissions  
GO  
-- Create another relational schema in the database.  
CREATE SCHEMA myOtherDBSchema  
GO  
CREATE USER TestLogin1  
GO  
-- For TestLogin1 to create/import XML schema collection, following  
-- permission needed.  
-- Database-level permissions  
GRANT CREATE XML SCHEMA COLLECTION TO TestLogin1  
GO  
GRANT ALTER ANY SCHEMA TO TestLogin1  
GO  
-- Now TestLogin1 can import an XML schema collection.  
SETUSER 'TestLogin1'  
GO  
CREATE XML SCHEMA COLLECTION myOtherDBSchema.myTestSchemaCollection AS '<?xml version="1.0" encoding="UTF-8" ?>  
<xsd:schema targetNamespace="https://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
elementFormDefault="qualified">  
<xsd:element name="telephone" type="xsd:string" />  
</xsd:schema>'  
GO  
DROP XML SCHEMA COLLECTION myOtherDBSchema.myTestSchemaCollection  
GO  
-- Now deny permission from TestLogin1 to alter myOtherDBSchema.  
setuser  
GO  
DENY ALTER ON SCHEMA::myOtherDBSchema TO TestLogin1  
GO  
-- Now TestLogin1 cannot create xml schema collection.  
SETUSER 'TestLogin1'  
GO  
CREATE XML SCHEMA COLLECTION myOtherDBSchema.myTestSchemaCollection AS '<?xml version="1.0" encoding="UTF-8" ?>  
<xsd:schema targetNamespace="https://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
elementFormDefault="qualified">  
<xsd:element name="telephone" type="xsd:string" />  
</xsd:schema>'  
GO  
-- Final cleanup  
SETUSER  
GO  
USE master  
GO  
DROP DATABASE SampleDBForSchemaPermissions  
GO  
DROP LOGIN TestLogin1  
GO  
```  
  
### <a name="b-denying-permissions-on-an-xml-schema-collection"></a>B. Denegar permisos en una colección de esquemas XML  
 El ejemplo siguiente muestra cómo se puede denegar a un inicio de sesión un permiso específico en una colección de esquemas XML existente. En este ejemplo, se deniega el permiso REFERENCES a un inicio de sesión de prueba para una colección de esquemas XML existente.  
  
 El ejemplo crea un usuario, `TestLogin1`, y una base de datos. Además del esquema `dbo` , también se crea un esquema relacional en la base de datos. Inicialmente, el permiso `CREATE XML SCHEMA` permite al usuario crear una colección de esquemas en cualquier lugar de la base de datos.  
  
 El permiso `REFERENCES` para la colección de esquemas XML permite a `TestLogin1` utilizar el esquema para crear una columna `xml` con tipo en una tabla. Si se deniega el permiso `REFERENCES` para la colección de esquemas XML, se evita que `TestLogin1` use la colección de esquemas XML.  
  
```  
CREATE LOGIN TestLogin1 WITH password='SQLSvrPwd1'  
GO  
CREATE DATABASE SampleDBForSchemaPermissions  
GO  
USE SampleDBForSchemaPermissions  
GO  
-- Create another relational schema in the database.  
CREATE SCHEMA myOtherDBSchema  
GO  
CREATE USER TestLogin1  
GO  
-- For TestLogin1 to create/import XML schema collection, the following  
-- permission is required.  
-- Database-level permissions  
GRANT CREATE XML SCHEMA COLLECTION TO TestLogin1  
GO  
GRANT ALTER ANY SCHEMA TO TestLogin1  
GO  
-- Now TestLogin1 can import an XML schema collection.  
SETUSER 'TestLogin1'  
GO  
CREATE XML SCHEMA COLLECTION myOtherDBSchema.myTestSchemaCollection AS '<?xml version="1.0" encoding="UTF-8" ?>  
<xsd:schema targetNamespace="https://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
elementFormDefault="qualified">  
<xsd:element name="telephone" type="xsd:string" />  
</xsd:schema>'  
GO  
-- Grant permission to TestLogin1 to create a table and reference the XML schema collection.  
SETUSER  
GO  
GRANT CREATE TABLE TO TestLogin1  
GO  
-- The user also needs REFERENCES permission to use the XML schema collection  
-- to create a typed XML column (REFERENCES permission on the schema   
-- collection is not needed).  
GRANT REFERENCES ON XML SCHEMA COLLECTION::myOtherDBSchema.myTestSchemaCollection   
TO TestLogin1  
GO  
  
--TestLogin1 can use the schema.  
CREATE TABLE T(i int, x xml (myOtherDBSchema.myTestSchemaCollection))  
GO  
-- Drop the table.  
DROP TABLE T  
GO  
-- Now deny REFERENCES permission to TestLogin1 on the schema created previously.  
SETUSER  
GO  
DENY REFERENCES ON XML SCHEMA COLLECTION::myOtherDBSchema.myTestSchemaCollection TO TestLogin1  
  
GO  
-- Now TestLogin1 cannot create xml schema collection  
SETUSER 'TestLogin1'  
GO  
-- Following statement fails. TestLogin1 does not have REFERENCES   
-- permission on the XML schema collection.  
CREATE TABLE T(i int, x xml (myOtherDBSchema.myTestSchemaCollection))  
GO  
  
-- Final cleanup  
SETUSER  
GO  
USE master  
GO  
DROP DATABASE SampleDBForSchemaPermissions  
GO  
DROP LOGIN TestLogin1  
GO  
```  
  
## <a name="see-also"></a>Consulte también  
 [Comparar XML con tipo y XML sin tipo](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [Colecciones de esquemas XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-schema-collections-sql-server.md)   
 [Requisitos y limitaciones de las colecciones de esquemas XML en el servidor](../../relational-databases/xml/requirements-and-limitations-for-xml-schema-collections-on-the-server.md)   
 [Permisos de objeto DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-object-permissions-transact-sql.md)   
 [Permisos de objeto GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)   
 [Datos XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md)  
  
  
