---
title: EVENTDATA (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- EVENTDATA
- fn_event_data
- EVENTDATA_TSQL
- fn_event_data_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- server instance event data [SQL Server]
- event notifications [SQL Server], event status
- events [SQL Server], status infromation
- EVENTDATA function
- status information [SQL Server], events
- DDL triggers, returning event data
ms.assetid: 03a80e63-6f37-4b49-bf13-dc35cfe46c44
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 45f9d434e5833180320dcb3184fdcceec56c715c
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="eventdata-transact-sql"></a>EVENTDATA (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve información acerca de los eventos de base de datos o servidor. EVENTDATA se llama cuando se activa una notificación de eventos y el resultado se devuelve al Service Broker especificado. EVENTDATA también se puede utilizar dentro del cuerpo de un desencadenador DDL o logon.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
EVENTDATA( )  
```  
  
## <a name="remarks"></a>Comentarios  
 EVENTDATA devuelve datos solo cuando se hace referencia al mismo directamente dentro de un desencadenador DDL o logon. EVENTDATA devuelve NULL si se llama desde otras rutinas, aunque un desencadenador DDL o logon llame a esas rutinas.  
  
 Los datos devueltos por EVENTDATA no son válidos después de confirmar o revertir una transacción que ha llamado a EVENTDATA, de forma implícita o explícita.  
  
> [!CAUTION]  
>  EVENTDATA devuelve datos XML. Estos datos se envían al cliente como Unicode que utiliza 2 bytes para cada carácter. Los siguientes puntos de código Unicode se pueden representar en XML que devuelve EVENTDATA:  
>   
>  `0x0009`  
>   
>  `0x000A`  
>   
>  `0x000D`  
>   
>  `>= 0x0020 && <= 0xD7FF`  
>   
>  `>= 0xE000 && <= 0xFFFD`  
>   
>  Algunos caracteres que pueden aparecer en identificadores y datos de [!INCLUDE[tsql](../../includes/tsql-md.md)] no se pueden expresar o permitir en XML. Los caracteres o datos que tienen puntos de código que no se muestran en la lista anterior se asignan a un signo de interrogación (?).  
  
 Para proteger la seguridad de los inicios de sesión, cuando se ejecutan las instrucciones CREATE LOGIN o ALTER LOGIN, las contraseñas no se muestran.  
  
## <a name="schemas-returned"></a>Esquemas devueltos  
 EVENTDATA devuelve un valor de tipo **xml**. De forma predeterminada, la definición de esquema para todos los eventos se instala en el directorio siguiente: [!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)]Tools\Binn\schemas\sqlserver\2006\11\events\events.xsd.  
  
 Como alternativa, el esquema de eventos se publica en el [Microsoft SQL Server XML Schemas](http://go.microsoft.com/fwlink/?LinkID=31850) página Web.  
  
 Para extraer el esquema de un evento concreto, busque el esquema del tipo complejo `EVENT_INSTANCE_\<event_type>`. Por ejemplo, para extraer el esquema del evento DROP_TABLE, busque el esquema de `EVENT_INSTANCE_DROP_TABLE`.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-querying-event-data-in-a-ddl-trigger"></a>A. Consultar datos de evento en un desencadenador DDL  
 En el siguiente ejemplo se crea un desencadenador DDL para impedir que se creen tablas nuevas en la base de datos. La instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] que activa el desencadenador se captura con XQuery con los datos XML que genera EVENTDATA. Para obtener más información, vea [Referencia del lenguaje XQuery &#40;SQL Server&#41;](../../xquery/xquery-language-reference-sql-server.md).  
  
> [!NOTE]  
>  Al consultar el `\<TSQLCommand>` elemento mediante **resultados a cuadrícula** en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], saltos de línea en el texto del comando no aparecen. Use **resultados a texto** en su lugar.  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TRIGGER safety   
ON DATABASE   
FOR CREATE_TABLE   
AS   
    PRINT 'CREATE TABLE Issued.'  
    SELECT EVENTDATA().value  
        ('(/EVENT_INSTANCE/TSQLCommand/CommandText)[1]','nvarchar(max)')  
   RAISERROR ('New tables cannot be created in this database.', 16, 1)   
   ROLLBACK  
;  
GO  
--Test the trigger.  
CREATE TABLE NewTable (Column1 int);  
GO  
--Drop the trigger.  
DROP TRIGGER safety  
ON DATABASE;  
GO  
```  
  
> [!NOTE]  
>  Si desea devolver datos de evento, se recomienda que utilice la expresión XQuery **value()** en lugar del método la **query()** método. El **query()** método devuelve XML y retornos de carro con caracteres de escape "y" comercial devuelto y avance de línea de instancias (CR/LF) en la salida, mientras que la **value()** método representa instancias de CR/LF invisibles en el resultado.  
  
### <a name="b-creating-a-log-table-with-event-data-in-a-ddl-trigger"></a>B. Crear una tabla de registro con datos de evento en un desencadenador DDL  
 En el siguiente ejemplo se crea una tabla para almacenar información sobre todos los eventos de nivel de base de datos y se rellena con un desencadenador DDL. El tipo de evento y la instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] se capturan mediante XQuery con los datos XML generados por `EVENTDATA`.  
  
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
--Test the trigger.  
CREATE TABLE TestTable (a int);  
DROP TABLE TestTable ;  
GO  
SELECT * FROM ddl_log ;  
GO  
--Drop the trigger.  
DROP TRIGGER log  
ON DATABASE;  
GO  
--Drop table ddl_log.  
DROP TABLE ddl_log;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Usar la función EVENTDATA](../../relational-databases/triggers/use-the-eventdata-function.md)   
 [Desencadenadores DDL](../../relational-databases/triggers/ddl-triggers.md)   
 [Notificaciones de eventos](../../relational-databases/service-broker/event-notifications.md)   
 [Desencadenadores logon](../../relational-databases/triggers/logon-triggers.md)  
  
  
