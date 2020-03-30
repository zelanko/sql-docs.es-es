---
title: Creación de índices XML | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- indexes [XML in SQL Server]
- XML indexes [SQL Server], creating
ms.assetid: 6ecac598-355d-4408-baf7-1b2e8d4cf7c1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8115350b3ead26a28c03fce975d058f393e0411b
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "67984777"
---
# <a name="create-xml-indexes"></a>Crear índices XML
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  En este tema se describe cómo crear índices XML principales y secundarios.  
  
## <a name="creating-a-primary-xml-index"></a>Crear un índice XML principal  
 Para crear un índice XML principal, use la instrucción DDL [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)]. Los índices XML no admiten todas las opciones que están disponibles para índices que no son XML.  
  
 Cuando cree un índice XML, tenga en cuenta lo siguiente:  
  
-   Para crear un índice XML principal, la tabla que contiene la columna XML que se va a indizar, llamada tabla base, debe tener un índice clúster en la clave principal. Esto garantiza que si la tabla base tiene particiones, se pueden crear particiones en el índice XML principal usando el mismo esquema y función de partición.  
  
-   Si ya existe un índice XML, la clave principal agrupada de la tabla no puede modificarse. Antes de modificar la clave principal, deberá quitar todos los índices XML de la tabla.  
  
-   Un índice XML principal puede crearse en una sola columna de tipo **xml** . No es posible crear ningún otro índice con una columna de tipo XML como columna de clave. Pero puede incluir la columna de tipo L **xml** en un índice que no sea XML. Cada columna de tipo **xml** de una tabla puede tener su propio índice XML principal. No obstante, solo se admite un índice XML principal por cada columna de tipo **xml** .  
  
-   Los índices XML existen en el mismo espacio de nombres que los índices que no son XML. Por tanto, no puede tener un índice XML y otro que no lo sea en la misma tabla y con el mismo nombre.  
  
-   Las opciones IGNORE_DUP_KEY y ONLINE siempre se establecen en OFF para los índices XML. Puede especificar estas opciones con el valor OFF.  
  
-   La información de partición o grupo de archivos de la tabla de usuarios se aplica al índice XML. Los usuarios no pueden especificar dicha información por separado en un índice XML.  
  
-   La opción de índice DROP_EXISTING permite quitar un índice XML principal y crear uno nuevo o efectuar la misma operación con un índice XML secundario. No obstante, esta opción no puede quitar un índice XML secundario para crear un índice XML principal ni viceversa.  
  
-   Los nombres de índice XML principal tienen las mismas restricciones que los nombres de vista.  
  
 No se puede crear un índice XML en un columna de tipo **xml** de una vista, en una variable con el valor **table** con columnas de tipo **xml** ni en variables de tipo **xml** .  
  
-   Para cambiar una columna de tipo **xml** de XML con tipo a XML sin tipo, o viceversa, con la opción ALTER TABLE ALTER COLUMN, la columna no debe incluir ningún índice XML. Si existe alguno, debe quitarse antes de intentar cambiar el tipo de columna.  
  
-   Al crear un índice XML, la opción ARITHABORT debe configurarse en ON. Para consultar, insertar, eliminar o actualizar valores en la columna XML usando métodos de tipo de datos XML, debe establecerse la misma opción en la conexión. De lo contrario, los métodos de tipo de datos XML darán error.  
  
    > [!NOTE]  
    >  Las vistas de catálogo incluyen información acerca de los índices XML. Pero no se admite **sp_helpindex** . Los ejemplos que se ofrecen más adelante en este tema muestran cómo consultar las vistas de catálogo para encontrar información de índices XML.  
  
 Al crear o volver a crear un índice XML principal o una columna de tipo de datos XML que contiene valores de los tipos de esquema XML **xs:date** o **xs:dateTime** (o cualquier subtipo de estos tipos) que tengan un año de menos de 1, se producirá un error en la creación del índice en [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] y versiones posteriores. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] permitía estos valores, por lo que este problema se puede producir al crear índices en una base de datos generada en [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Para obtener más información, vea [Comparar XML con tipo y XML sin tipo](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md).  
  
### <a name="example-creating-a-primary-xml-index"></a>Ejemplo: Crear un índice XML principal  
 En la mayoría de los ejemplos, se utiliza la tabla T (pk INT PRIMARY KEY, xCol XML) con una columna XML sin tipo. Se pueden ampliar a XML con tipo de forma directa. Para simplificar el trabajo, las consultas se describen para instancias de datos XML como se indica a continuación:  
  
```  
<book genre="security" publicationdate="2002" ISBN="0-7356-1588-2">  
   <title>Writing Secure Code</title>  
   <author>  
      <first-name>Michael</first-name>  
      <last-name>Howard</last-name>  
   </author>  
   <author>  
      <first-name>David</first-name>  
      <last-name>LeBlanc</last-name>  
   </author>  
   <price>39.99</price>  
</book>  
```  
  
 La siguiente instrucción crea un índice XML, denominado idx_xCol, en la columna XML xCol de la tabla T:  
  
```  
CREATE PRIMARY XML INDEX idx_xCol on T (xCol)  
```  
  
## <a name="creating-a-secondary-xml-index"></a>Crear un índice XML secundario  
 Use la instrucción DDL [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)] para crear índices XML secundarios y especificar el tipo de índice XML secundario que quiere.  
  
 Cuando cree índices XML secundarios, tenga en cuenta lo siguiente:  
  
-   Todas las opciones de indización que se aplican a un índice no clúster, salvo IGNORE_DUP_KEY y ONLINE, se admiten para los índices XML secundarios. Las dos opciones deben establecerse siempre en OFF para los índices XML secundarios.  
  
-   Los índices secundarios se dividen en particiones al igual que el índice XML principal.  
  
-   DROP_EXISTING permite quitar un índice secundario de la tabla de usuario y crear otro en la misma tabla.  
  
 Puede consultar la vista de catálogo **sys.xml_indexes** para recuperar información de índices XML. Tenga en cuenta que la columna **secondary_type_desc** de la vista de catálogo **sys.xml_indexes** proporciona el tipo de índice secundario:  
  
```  
SELECT  *   
FROM    sys.xml_indexes;  
```  
  
 Los valores que se devuelven en la columna **secondary_type_desc** pueden ser NULL, PATH, VALUE o PROPERTY. El valor devuelto para el índice XML principal es NULL.  
  
### <a name="example-creating-secondary-xml-indexes"></a>Ejemplo: Crear índices XML secundarios  
 El ejemplo siguiente muestra cómo crear índices XML secundarios. En el ejemplo también se muestra información acerca de los índices XML que ha creado.  
  
```  
CREATE TABLE T (Col1 INT PRIMARY KEY, XmlCol XML);  
GO  
-- Create primary index.  
CREATE PRIMARY XML INDEX PIdx_T_XmlCol   
ON T(XmlCol);  
GO  
-- Create secondary indexes (PATH, VALUE, PROPERTY).  
CREATE XML INDEX PIdx_T_XmlCol_PATH ON T(XmlCol)  
USING XML INDEX PIdx_T_XmlCol  
FOR PATH;  
GO  
CREATE XML INDEX PIdx_T_XmlCol_VALUE ON T(XmlCol)  
USING XML INDEX PIdx_T_XmlCol  
FOR VALUE;  
GO  
CREATE XML INDEX PIdx_T_XmlCol_PROPERTY ON T(XmlCol)  
USING XML INDEX PIdx_T_XmlCol  
FOR PROPERTY;  
GO  
```  
  
 Puede consultar `sys.xml_indexes` para recuperar información de índices XML. La columna `secondary_type_desc` proporciona el tipo de índice secundario.  
  
```  
SELECT  *   
FROM    sys.xml_indexes;  
```  
  
 También puede consultar la vista de catálogo para obtener información de índice.  
  
```  
SELECT *  
FROM sys.xml_indexes  
WHERE object_id = object_id('T');  
```  
  
 Puede agregar datos de ejemplo y, a continuación, revisar la información de índices XML.  
  
```  
INSERT INTO T VALUES (1,  
'<doc id="123">  
<sections>  
<section num="2">  
<heading>Background</heading>  
</section>  
<section num="3">  
<heading>Sort</heading>  
</section>  
<section num="4">  
<heading>Search</heading>  
</section>  
</sections>  
</doc>');  
GO  
-- Check XML index information.  
SELECT *  
FROM   sys.dm_db_index_physical_stats (db_id(), object_id('T'), NULL, NULL, 'DETAILED');  
GO  
-- Space usage of primary XML index  
DECLARE @index_id int;  
SELECT  @index_id = i.index_id  
FROM    sys.xml_indexes i   
WHERE   i.name = 'PIdx_T_XmlCol' and object_name(i.object_id) = 'T';  
  
SELECT *  
FROM sys.dm_db_index_physical_stats (db_id(), object_id('T') , @index_id, DEFAULT, 'DETAILED');  
go  
--- Space usage of secondary XML index (for example PATH secondary index)  PIdx_T_XmlCol_PATH  
DECLARE @index_id int;  
SELECT  @index_id = i.index_id   
FROM    sys.xml_indexes i   
WHERE  i.name = 'PIdx_T_XmlCol_PATH' and object_name(i.object_id) = 'T';  
  
SELECT *  
FROM sys.dm_db_index_physical_stats (db_id(), object_id('T') , @index_id, DEFAULT, 'DETAILED');  
go  
  
-- Space usage of all secondary XML indexes for a particular table  
SELECT i.name, object_name(i.object_id), stats.*   
FROM   sys.dm_db_index_physical_stats (db_id(), object_id('T'), NULL, DEFAULT, 'DETAILED') stats  
JOIN sys.xml_indexes i ON (stats.object_id = i.object_id and stats.index_id = i.index_id)  
WHERE secondary_type is not null;  
-- Drop secondary indexes.  
DROP INDEX PIdx_T_XmlCol_PATH ON T;  
GO  
DROP INDEX PIdx_T_XmlCol_VALUE ON T;  
GO  
DROP INDEX PIdx_T_XmlCol_PROPERTY ON T;  
GO  
-- Drop primary index.  
DROP INDEX PIdx_T_XmlCol ON T;  
-- Drop table T.  
DROP TABLE T;  
Go  
```  
  
## <a name="see-also"></a>Consulte también  
 [Índices XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-indexes-sql-server.md)   
 [Datos XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md)  
  
  
