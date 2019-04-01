---
title: Revocar los permisos en una colección de esquemas XML | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- revoking permissions [SQL Server]
ms.assetid: 4e542b70-2d56-4a65-8a39-96a1ed477ca6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 69605fbbca950abf4d014f0486f18ed6e17bd8e3
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58513012"
---
# <a name="revoke-permissions-on-an-xml-schema-collection"></a>Revocar los permisos en una colección de esquemas XML
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Para revocar el permiso para crear una colección de esquemas XML, realice uno de los procedimientos siguientes:  
  
-   Revocar el permiso ALTER para el esquema relacional. Entonces, la entidad de seguridad no podrá crear una colección de esquemas XML en el esquema relacional. No obstante, la entidad de seguridad todavía podría hacerlo en otros esquemas relacionales de la misma base de datos.  
  
-   Revocar el permiso ALTER ANY SCHEMA de la entidad de seguridad en la base de datos. Entonces, la entidad de seguridad no podrá crear ninguna colección de esquemas XML en ningún lugar de la base de datos.  
  
-   Revocar el permiso CREATE XML SCHEMA COLLECTION o ALTER XML SCHEMA COLLECTION de la entidad de seguridad en la base de datos. De esta forma, se impide a la entidad de seguridad importar una colección de esquemas XML a la base de datos. Revocar el permiso ALTER o CONTROL en la base de datos tiene el mismo efecto.  
  
## <a name="revoking-permissions-on-an-existing-xml-schema-collection-object"></a>Revocar los permisos en un objeto de colección de esquemas XML existente  
 A continuación se indican los permisos que se pueden revocar en una colección de esquemas XML y los resultados:  
  
-   Al revocar el permiso ALTER, se impide que una entidad de seguridad pueda modificar el contenido de la colección de esquemas XML.  
  
-   Al revocar el permiso TAKE OWNERSHIP, se impide que una entidad de seguridad pueda transferir la propiedad de la colección de esquemas XML.  
  
-   Al revocar el permiso REFERENCES, se impide que una entidad de seguridad pueda utilizar la colección de esquemas XML para asignar tipos o restringir columnas de tipo xml, en tablas y vistas, y parámetros. También se revoca el permiso para hacer referencia a esta colección de esquemas desde otras colecciones de esquemas XML.  
  
-   Al revocar el permiso VIEW DEFINITION, se impide que una entidad de seguridad pueda ver el contenido de una colección de esquemas XML.  
  
-   Al revocar el permiso EXECUTE, se impide que una entidad de seguridad pueda insertar o actualizar valores en columnas, variables y parámetros que reciban tipos o restricciones de la colección XML. También se revoca la posibilidad de realizar consultas en esas columnas, variables o parámetros de tipo **xml** .  
  
## <a name="examples"></a>Ejemplos  
 Los escenarios de los ejemplos siguientes ilustran el funcionamiento de los permisos de los esquemas XML. En cada ejemplo se crea la base de datos de prueba, los esquemas relacionales y los inicios de sesión necesarios. A estos inicios de sesión se les conceden los permisos necesarios para la colección de esquemas XML. Al final, cada ejemplo realiza las operaciones de limpieza necesarias.  
  
### <a name="a-revoking-permissions-to-create-an-xml-schema-collection"></a>A. Revocar los permisos para crear una colección de esquemas XML  
 En este ejemplo se crea un inicio de sesión y una base de datos de ejemplo. Asimismo, se agrega un esquema relacional en la base de datos. Inicialmente, al inicio de sesión se le concede el permiso ALTER para ambos esquemas relacionales y otros permisos necesarios para crear colecciones de esquemas XML. Después, se revoca el permiso ALTER en uno de los esquemas relacionales de la base de datos. De esta forma, se evita que el inicio de sesión cree una colección de esquemas XML.  
  
```  
setuser  
go  
create login TestLogin1 with password='SQLSvrPwd1'  
go  
create database SampleDBForSchemaPermissions  
go  
use SampleDBForSchemaPermissions  
go  
-- Create another relational schema in the db (in addition to dbo schema)  
CREATE SCHEMA myOtherDBSchema  
go  
CREATE USER TestLogin1  
go  
-- For TestLogin1 to create/import XML schema collection, following  
-- permission needed  
-- CREATE XML SCHEMA is a database level permission  
GRANT CREATE XML SCHEMA COLLECTION TO TestLogin1  
go  
GRANT ALTER ON SCHEMA::myOtherDBSchema TO TestLogin1  
go  
GRANT ALTER ON SCHEMA::dbo TO TestLogin1  
go  
-- Now TestLogin1 can import an XML schema collection in both relational schemas.  
setuser 'TestLogin1'  
go  
CREATE XML SCHEMA COLLECTION dbo.myTestSchemaCollection AS '<?xml version="1.0" encoding="UTF-8" ?>  
  
<xsd:schema targetNamespace="https://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
elementFormDefault="qualified">  
<xsd:element name="telephone" type="xsd:string" />  
</xsd:schema>'  
go  
-- TestLogin1 can create XML schema collection in myOtherDBSchema relational schema  
CREATE XML SCHEMA COLLECTION myOtherDBSchema.myTestSchemaCollection AS '<?xml version="1.0" encoding="UTF-8" ?>  
  
<xsd:schema targetNamespace="https://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
elementFormDefault="qualified">  
<xsd:element name="telephone" type="xsd:string" />  
</xsd:schema>'  
go  
-- Let us drop XML schema collections from both relational schemas  
DROP XML SCHEMA COLLECTION myOtherDBSchema.myTestSchemaCollection  
go  
DROP XML SCHEMA COLLECTION dbo.myTestSchemaCollection  
go  
-- now REVOKE permission from TestLogin1 to alter myOtherDBSchema  
setuser  
go  
REVOKE ALTER ON SCHEMA::myOtherDBSchema FROM TestLogin1  
go  
-- now TestLogin1 cannot create xml schema collection in myOtherDBSchema  
setuser 'TestLogin1'  
go  
CREATE XML SCHEMA COLLECTION myOtherDBSchema.myTestSchemaCollection AS '<?xml version="1.0" encoding="UTF-8" ?>  
<xsd:schema targetNamespace="https://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
elementFormDefault="qualified">  
<xsd:element name="telephone" type="xsd:string" />  
</xsd:schema>'  
go  
  
-- TestLogin1 can still create XML schema collections in dbo  
-- It cannot create XML schema collections anywhere in the database  
-- if we REVOKE CREATE XML SCHEMA COLLECTION permission  
SETUSER  
go  
REVOKE CREATE XML SCHEMA COLLECTION FROM TestLogin1  
go  
  
setuser 'TestLogin1'  
go  
-- the following now should fail  
CREATE XML SCHEMA COLLECTION dbo.myTestSchemaCollection AS '<?xml version="1.0" encoding="UTF-8" ?>  
<xsd:schema targetNamespace="https://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
elementFormDefault="qualified">  
<xsd:element name="telephone" type="xsd:string" />  
</xsd:schema>'  
go  
  
-- Final cleanup  
SETUSER  
go  
USE master  
go  
DROP DATABASE SampleDBForSchemaPermissions  
go  
DROP LOGIN TestLogin1  
Go  
```  
  
## <a name="see-also"></a>Consulte también  
 [Datos XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md)   
 [Comparar XML con tipo y XML sin tipo](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [Colecciones de esquemas XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-schema-collections-sql-server.md)   
 [Requisitos y limitaciones de las colecciones de esquemas XML en el servidor](../../relational-databases/xml/requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
