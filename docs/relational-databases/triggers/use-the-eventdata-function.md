---
title: Usar la función EVENTDATA | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- EVENTDATA function
- DDL triggers, EVENTDATA function
ms.assetid: 675b8320-9c73-4526-bd2f-91ba42c1b604
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: aef51bd94bf7cffb3e9481b409477a3830fabffb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68058603"
---
# <a name="use-the-eventdata-function"></a>Usar la función EVENTDATA
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]
  La información acerca de un evento que activa un desencadenador DDL se captura mediante la función EVENTDATA. Esta función devuelve un valor **xml** . El esquema XML incluye información acerca de lo siguiente:  
  
-   La hora del evento.  
  
-   El Id. de proceso del sistema (SPID) de la conexión en la cual se ha ejecutado el desencadenador.  
  
-   El tipo de evento que ha activado el desencadenador.  
  
 En función del tipo de evento, el esquema incluirá información adicional, como la base de datos en la que se ha producido el evento, el objeto en el que se ha producido el evento y la instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] del evento. Para más información, consulte [DDL Triggers](../../relational-databases/triggers/ddl-triggers.md).  
  
 Por ejemplo, el siguiente desencadenador DDL se crea en la base de datos de ejemplo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] :  
  
```  
CREATE TRIGGER safety   
ON DATABASE   
FOR CREATE_TABLE   
AS   
    PRINT 'CREATE TABLE Issued.'  
    SELECT EVENTDATA().value('(/EVENT_INSTANCE/TSQLCommand/CommandText)[1]','nvarchar(max)')  
   RAISERROR ('New tables cannot be created in this database.', 16, 1)   
   ROLLBACK  
;  
```  
  
 Se ejecutará la siguiente instrucción `CREATE TABLE` :  
  
 `CREATE TABLE NewTable (Column1 int);`  
  
 La instrucción `EVENTDATA()` del desencadenador DDL captura el texto de la instrucción `CREATE TABLE` que no se admite. Esto se consigue usando una instrucción XQuery en los datos **xml** generados por EVENTDATA y recuperando el elemento \<CommandText>. Para obtener más información, vea [Referencia del lenguaje XQuery &#40;SQL Server&#41;](../../xquery/xquery-language-reference-sql-server.md).  
  
> [!CAUTION]  
>  EVENTDATA captura los datos de los eventos CREATE_SCHEMA, así como el >schema_element< de la definición CREATE SCHEMA correspondiente, si existe. Además, EVENTDATA reconoce la definición <schema_element> como un evento aparte. Por lo tanto, un desencadenador DDL creado en un evento CREATE_SCHEMA y en un evento representado por el <schema_element> de la definición CREATE SCHEMA, puede devolver los mismos datos de evento dos veces, por ejemplo, datos `TSQLCommand`. Por ejemplo, considere un desencadenador DDL creado en los eventos CREATE_SCHEMA y CREATE_TABLE, y que se ejecute el siguiente lote:  
>   
>  `CREATE SCHEMA s`  
>   
>  `CREATE TABLE t1 (col1 int)`  
>   
>  Si la aplicación recupera los datos de `TSQLCommand` del evento CREATE_TABLE, tenga en cuenta que estos datos pueden aparecer dos veces: una vez cuando tiene lugar el evento CREATE_SCHEMA, y otra cuando tiene lugar el evento CREATE_TABLE. Evite crear desencadenadores DDL en los eventos CREATE_SCHEMA y en los textos <schema_element> de cualquier definición CREATE SCHEMA correspondiente, o cree la lógica en su aplicación para que el mismo evento no se procese dos veces.  
  
## <a name="alter-table-and-alter-database-events"></a>Eventos ALTER TABLE y ALTER DATABASE  
 Los datos de evento para los eventos ALTER_TABLE y ALTER_DATABASE también incluyen los nombres y los tipos de otros objetos afectados por la instrucción DDL y la acción realizada en estos objetos. Los datos del evento ALTER_TABLE incluyen los nombres de las columnas, restricciones o desencadenadores afectados por la instrucción ALTER TABLE y la acción (crear, modificar, quitar, habilitar o deshabilitar) realizada en los objetos afectados. Los datos del evento ALTER_DATABASE incluyen los nombres de los archivos o grupos de archivos afectados por la instrucción ALTER DATABASE y la acción (crear, modificar o quitar) realizada en los objetos afectados.  
  
 Por ejemplo, cree el siguiente desencadenador DDL en la base de datos de ejemplo AdventureWorks:  
  
```  
CREATE TRIGGER ColumnChanges  
ON DATABASE   
FOR ALTER_TABLE  
AS  
-- Detect whether a column was created/altered/dropped.  
SELECT EVENTDATA().value('(/EVENT_INSTANCE/TSQLCommand/CommandText)[1]', 'nvarchar(max)')  
RAISERROR ('Table schema cannot be modified in this database.', 16, 1);  
ROLLBACK;  
```  
  
 A continuación, ejecute la siguiente instrucción ALTER TABLE que infringe una restricción:  
  
```  
ALTER TABLE Person.Address ALTER COLUMN ModifiedDate date;   
```  
  
 La instrucción EVENTDATA() del desencadenador DDL captura el texto de la instrucción `ALTER TABLE` que no se permite.  
  
## <a name="example"></a>Ejemplo  
 Puede utilizar la función EVENTDATA para crear un registro de eventos. En el siguiente ejemplo, una tabla se crea para almacenar la información del evento. A continuación, se crea un desencadenador DDL en la base de datos actual que rellena la tabla con la siguiente información siempre que tiene lugar un evento DDL en la base de datos:  
  
-   La hora del evento (mediante la función GETDATE).  
  
-   El usuario de la base de datos contra cuya sesión se ha producido el evento (mediante la función CURRENT_USER).  
  
-   El tipo de evento.  
  
-   La instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] que contenía el evento.  
  
 Una vez más, los dos últimos elementos se capturan mediante XQuery con los datos **xml** generados por EVENTDATA.  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE ddl_log (PostTime datetime, DB_User nvarchar(100), Event nvarchar(100), TSQL nvarchar(2000));  
GO  
CREATE TRIGGER log   
ON DATABASE   
FOR DDL_DATABASE_LEVEL_EVENTS   
AS  
DECLARE @data XML  
SET @data = EVENTDATA()  
INSERT ddl_log   
   (PostTime, DB_User, Event, TSQL)   
   VALUES   
   (GETDATE(),   
   CONVERT(nvarchar(100), CURRENT_USER),   
   @data.value('(/EVENT_INSTANCE/EventType)[1]', 'nvarchar(100)'),   
   @data.value('(/EVENT_INSTANCE/TSQLCommand)[1]', 'nvarchar(2000)') ) ;  
GO  
--Test the trigger  
CREATE TABLE TestTable (a int)  
DROP TABLE TestTable ;  
GO  
SELECT * FROM ddl_log ;  
GO  
```  
  
> [!NOTE]  
>  Cuando quiera devolver datos de evento, se recomienda usar el método XQuery **value()** en vez del método **query()** . El método **query()** devuelve XML e instancias de retorno de carro y avance de línea (CRLF) con el carácter de escape Y comercial en el resultado, mientras que el método **value()** representa instancias de CRLF invisibles en el resultado.  
  
 Un ejemplo de desencadenador DDL parecido se proporciona con la base de datos de ejemplo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] . Para obtener el ejemplo, localice la carpeta Database Triggers mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Esta carpeta se encuentra en la carpeta **Programación** de la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] . Haga clic con el botón derecho en **ddlDatabaseTriggerLog** y seleccione **Script Database Trigger as** (desencadenador de base de datos de script como). De forma predeterminada, el desencadenador DDL **ddlDatabaseTriggerLog** está deshabilitado.  
  
## <a name="see-also"></a>Consulte también  
 [Eventos DDL](../../relational-databases/triggers/ddl-events.md)   
 [Grupos de eventos DDL](../../relational-databases/triggers/ddl-event-groups.md)  
  
  
