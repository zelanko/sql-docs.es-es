---
title: Desencadenadores DDL | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- DDL triggers, about DDL triggers
ms.assetid: 1a4a6564-9820-4a14-9305-2c0e9ea37454
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 87f260bc69a582726c2e995ed1934d10a1481db9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62654981"
---
# <a name="ddl-triggers"></a>Desencadenadores DDL
  Los desencadenadores DDL se inician en respuesta a una variedad de eventos de lenguaje de definición de datos (DDL). Estos eventos corresponden principalmente a las instrucciones de [!INCLUDE[tsql](../../includes/tsql-md.md)] que comienzan por las palabras clave CREATE, ALTER, DROP, GRANT, DENY, REVOKE o UPDATE STATISTICS. Algunos procedimientos almacenados del sistema que ejecutan operaciones de tipo DDL también pueden activar desencadenadores DDL.  
  
 Use desencadenadores DDL cuando desee hacer lo siguiente:  
  
-   Impedir determinados cambios en el esquema de la base de datos.  
  
-   Que ocurra algo en la base de datos como respuesta a un cambio realizado en el esquema de la base de datos.  
  
-   Registrar cambios o eventos en el esquema de la base de datos.  
  
> [!IMPORTANT]  
>  Pruebe los desencadenadores DDL para determinar su respuesta a los procedimientos almacenados del sistema que se ejecutan. Por ejemplo, tanto la instrucción CREATE TYPE como el procedimiento almacenado **sp_addtype** activarán un desencadenador DDL que se crea en un evento CREATE_TYPE.  
  
## <a name="types-of-ddl-triggers"></a>Tipos de desencadenadores DDL  
 Desencadenador DDL de Transact-SQL  
 Un tipo especial de procedimiento almacenado de [!INCLUDE[tsql](../../includes/tsql-md.md)] que ejecuta una o más instrucciones de [!INCLUDE[tsql](../../includes/tsql-md.md)] como respuesta a un evento con ámbito de servidor o de base de datos. Por ejemplo, un desencadenador DDL se puede activar si se ejecuta una instrucción como ALTER SERVER CONFIGURATION o si se elimina una tabla mediante DROP TABLE.  
  
 Desencadenador DDL de CLR  
 En lugar de ejecutar un procedimiento almacenado [!INCLUDE[tsql](../../includes/tsql-md.md)] , un desencadenador CLR ejecuta uno o más métodos escritos en código administrado que son miembros de un ensamblado creado en .NET Framework y cargado en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Los desencadenadores DDL solo se activan cuando se ejecutan las instrucciones DDL que los desencadenan. Los desencadenadores DDL no se pueden usar como desencadenadores INSTEAD OF. Los desencadenadores DDL no se activan como respuesta a eventos que afectan a procedimientos almacenados y tablas temporales, ya sean locales o globales.  
  
 Los desencadenadores DDL no crean las tablas `inserted` y `deleted` especiales.  
  
 La información acerca de un evento que activa un desencadenador DDL y las modificaciones posteriores provocadas por el mismo se capturan con la función EVENTDATA.  
  
 Por cada evento DDL se crean varios desencadenadores.  
  
 A diferencia de los desencadenadores DML, los desencadenadores DDL no tienen como ámbito los esquemas. Por tanto, las funciones como OBJECT_ID, OBJECT_NAME, OBJECTPROPERTY y OBJECTPROPERTYEX no se pueden usar para efectuar consultas en metadatos sobre desencadenadores DDL. Utilice en su lugar las vistas de catálogo.  
  
 Los desencadenadores DDL con ámbito en el servidor aparecen en el Explorador de objetos de SQL Server Management Studio, en la carpeta **Desencadenadores** . Dicha carpeta se encuentra en la carpeta **Server Objects** . Los desencadenadores DDL de ámbito de base de datos aparecen en la carpeta **Desencadenadores de bases de datos** . Esta carpeta se encuentra en la carpeta **Programación** de la base de datos correspondiente.  
  
> [!IMPORTANT]  
>  El código malintencionado de los desencadenadores se puede ejecutar con privilegios concentrados. Para obtener más información sobre cómo reducir este riesgo, vea [Administrar la seguridad de los desencadenadores](manage-trigger-security.md).  
  
## <a name="ddl-trigger-scope"></a>Ámbito de desencadenadores DDL  
 Los desencadenadores DDL pueden activarse en respuesta a un evento de [!INCLUDE[tsql](../../includes/tsql-md.md)] procesado en la base de datos actual o en el servidor actual. El ámbito del desencadenador depende del evento. Por ejemplo, un desencadenador DDL creado para activarse como respuesta a un evento CREATE_TABLE se activará siempre que se produzca un evento CREATE_TABLE en la base de datos o en la instancia de servidor. Un desencadenador DDL creado para activarse como respuesta a un evento CREATE_LOGIN se activará únicamente cuando que se produzca un evento CREATE_LOGIN en la instancia de servidor.  
  
 En el ejemplo siguiente, el desencadenador DDL `safety` se activará siempre que se produzca un evento `DROP_TABLE` o `ALTER_TABLE` en la base de datos.  
  
```  
CREATE TRIGGER safety   
ON DATABASE   
FOR DROP_TABLE, ALTER_TABLE   
AS   
   PRINT 'You must disable Trigger "safety" to drop or alter tables!'   
   ROLLBACK;  
```  
  
 En el ejemplo siguiente, un desencadenador DDL imprime un mensaje si se produce algún evento `CREATE_DATABASE` en la instancia de servidor actual. El ejemplo usa la función `EVENTDATA` para recuperar el texto de la instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] correspondiente. Para obtener más información sobre el uso de EVENTDATA con desencadenadores DDL, vea [Usar la función EVENTDATA](use-the-eventdata-function.md).  
  
```  
IF EXISTS (SELECT * FROM sys.server_triggers  
    WHERE name = 'ddl_trig_database')  
DROP TRIGGER ddl_trig_database  
ON ALL SERVER;  
GO  
CREATE TRIGGER ddl_trig_database   
ON ALL SERVER   
FOR CREATE_DATABASE   
AS   
    PRINT 'Database Created.'  
    SELECT EVENTDATA().value('(/EVENT_INSTANCE/TSQLCommand/CommandText)[1]','nvarchar(max)')  
GO  
DROP TRIGGER ddl_trig_database  
ON ALL SERVER;  
GO  
  
```  
  
 Las listas que asignan las instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] a los ámbitos que se pueden especificar para ellas están disponibles en los vínculos de la sección "Seleccionar una instrucción DDL concreta para activar un desencadenador DDL".  
  
 Los desencadenadores DDL de ámbito de base de datos se almacenan como objetos en la base de datos donde se crean. Estos desencadenadores se pueden crear en la base de datos **maestra** y actuar como los creados en bases de datos diseñadas por el usuario. Para obtener información acerca de los desencadenadores DDL, consulte la vista de catálogo **sys.triggers** . Puede consultar **sys.triggers** dentro del contexto de la base de datos en la que se crean los desencadenadores o si especifica el nombre de la base de datos como un identificador, como **master.sys.triggers**.  
  
 Los desencadenadores DDL de ámbito de servidor se almacenan como objetos en la base de datos **maestra** . Pero puede obtenerse información sobre los desencadenadores DDL de ámbito de servidor si se consulta la vista de catálogo **sys.server_triggers** en cualquier contexto de base de datos.  
  
## <a name="specifying-a-transact-sql-statement-or-group-of-statements"></a>Especificar una instrucción o grupo de instrucciones Transact-SQL  
  
### <a name="selecting-a-particular-ddl-statement-to-fire-a-ddl-trigger"></a>Seleccionar una instrucción DDL concreta para activar un desencadenador DDL  
 Los desencadenadores DDL se pueden diseñar para activarse después de ejecutar una o varias instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] determinadas. En el anterior ejemplo, el desencadenador `safety` se activa después de un evento `DROP_TABLE` o `ALTER_TABLE` . Para obtener una lista de las instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] que pueden especificarse para activar un desencadenador DDL y el ámbito en el que el desencadenador se puede activar, vea [Eventos DDL](ddl-events.md).  
  
### <a name="selecting-a-predefined-group-of-ddl-statements-to-fire-a-ddl-trigger"></a>Seleccionar un grupo predefinido de instrucciones DDL para activar un desencadenador DDL  
 Los desencadenadores DDL se pueden activar tras la ejecución de un evento de [!INCLUDE[tsql](../../includes/tsql-md.md)] que pertenezca a una agrupación predefinida de eventos similares. Por ejemplo, si desea activar un desencadenador DDL después de que se ejecute una instrucción CREATE TABLE, ALTER TABLE o DROP TABLE, puede especificar FOR DDL_TABLE_EVENTS en la instrucción CREATE TRIGGER. Después de ejecutar CREATE TRIGGER, los eventos incluidos en un grupo de eventos se agregan a la vista de catálogo **sys.trigger_events** .  
  
 En [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], si se crea un desencadenador en un grupo de eventos, **sys.trigger_events** no incluye la información sobre el grupo de eventos, mientras que **sys.trigger_events** incluye solo la información sobre los eventos individuales cubiertos por dicho grupo. En [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] y versiones posteriores, **sys.trigger_events** conserva los metadatos sobre el grupo de eventos en el que se crean los desencadenadores y también sobre los eventos individuales cubiertos por el grupo de eventos. Por consiguiente, los cambios en los eventos cubiertos por los grupos de eventos en [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] y posteriores no se aplican a los desencadenadores DDL creados en los grupos de eventos en [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
 Para obtener una lista de los grupos predefinidos de instrucciones DDL disponibles para los desencadenadores DDL, las instrucciones concretas que cubren los grupos de eventos y los ámbitos donde se pueden programar estos grupos de eventos, vea [DDL Event Groups](ddl-event-groups.md).  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Tarea|Tema|  
|----------|-----------|  
|Describe cómo crear, modificar, eliminar o deshabilitar los desencadenadores DDL.|[Implementar desencadenadores DDL](implement-ddl-triggers.md)|  
|Describe cómo crear un desencadenador DDL de CLR.|[Crear desencadenadores CLR](create-clr-triggers.md)|  
|Describe cómo devolver información acerca de los desencadenadores DDL.|[Obtener información acerca de los desencadenadores DDL](get-information-about-ddl-triggers.md)|  
|Describe cómo devolver información acerca de un evento que activa un desencadenador DDL mediante la función EVENTDATA.|[Usar la función EVENTDATA](use-the-eventdata-function.md)|  
|Describe cómo administrar la seguridad de los desencadenadores.|[Administrar la seguridad de los desencadenadores](manage-trigger-security.md)|  
  
## <a name="see-also"></a>Vea también  
 [Desencadenadores DML](dml-triggers.md)   
 [Desencadenadores logon](logon-triggers.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-trigger-transact-sql)  
  
  
