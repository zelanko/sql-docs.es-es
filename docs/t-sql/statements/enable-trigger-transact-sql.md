---
title: ACTIVAR el DESENCADENADOR (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 05/12/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ENABLE TRIGGER
- ENABLE_TSQL
- ENABLE_TRIGGER_TSQL
- ENABLE
dev_langs: TSQL
helpviewer_keywords:
- DDL triggers, enabling
- triggers [SQL Server], enabling
- DML triggers, enabling
- ENABLE TRIGGER statement
ms.assetid: 6e21f0ad-68d0-432f-9c7c-a119dd2d3fc9
caps.latest.revision: "39"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 7627fdb66a091d5add30a8384861d9b6b03b82b5
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="enable-trigger-transact-sql"></a>ENABLE TRIGGER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Habilita un desencadenador DML, DDL o logon.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
ENABLE TRIGGER { [ schema_name . ] trigger_name [ ,...n ] | ALL }  
ON { object_name | DATABASE | ALL SERVER } [ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *schema_name*  
 Es el nombre del esquema al que pertenece el desencadenador. *schema_name* no se puede especificar para desencadenadores DDL o logon.  
  
 *trigger_name*  
 Es el nombre del desencadenador que se va a habilitar.  
  
 ALL  
 Indica que todos los desencadenadores del ámbito de la cláusula ON están habilitados.  
  
 *object_name*  
 Es el nombre de la tabla o vista en la que el desencadenador DML *trigger_name* se creó para ejecutar.  
  
 DATABASE  
 Para un desencadenador DDL, indica que *trigger_name* se creó o modificó para ejecutarse en el ámbito de la base de datos.  
  
 ALL SERVER  
 **Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Para un desencadenador DDL, indica que *trigger_name* se creó o modificó para ejecutarse en el ámbito del servidor. ALL SERVER también se aplica a los desencadenadores de inicio de sesión.  
  
> [!NOTE]  
>  Esta opción no está disponible en las bases de datos independientes.  
  
## <a name="remarks"></a>Comentarios  
 Si se habilita un desencadenador, éste no se vuelve a crear. Un desencadenador deshabilitado sigue existiendo como objeto en la base de datos actual, pero no se activa. La habilitación de un desencadenador hace que se active cuando se ejecute cualquier instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] en que se programó originalmente. Los desencadenadores se deshabilitan con [DISABLE TRIGGER](../../t-sql/statements/disable-trigger-transact-sql.md). Desencadenadores DML definidos en tablas pueden ser también puede habilitar o deshabilitar mediante el uso de [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 Para habilitar un desencadenador DML, como mínimo, el usuario debe tener permiso ALTER en la tabla o vista en la que se creó el desencadenador.  
  
 Para habilitar un desencadenador DDL con ámbito del servidor (ON ALL SERVER) o un desencadenador logon, el usuario debe tener el permiso CONTROL SERVER en el servidor. Para habilitar un desencadenador DDL con ámbito de la base de datos (ON DATABASE), un usuario debe tener permiso ALTER ANY DATABASE DDL TRIGGER en la base de datos actual.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-enabling-a-dml-trigger-on-a-table"></a>A. Habilitar un desencadenador DML en una tabla  
 En el ejemplo siguiente se deshabilita el desencadenador `uAddress` que se creó en la tabla `Address` en la base de datos de AdventureWorks y, a continuación, vuelva a habilitarla.  
  
```  
DISABLE TRIGGER Person.uAddress ON Person.Address;  
GO  
ENABLE Trigger Person.uAddress ON Person.Address;  
GO  
```  
  
### <a name="b-enabling-a-ddl-trigger"></a>B. Habilitar un desencadenador DDL  
 En el ejemplo siguiente se crea un desencadenador DDL `safety` con ámbito, la base de datos y, a continuación, deshabilitar y lo habilita.  
  
```  
CREATE TRIGGER safety   
ON DATABASE   
FOR DROP_TABLE, ALTER_TABLE   
AS   
   PRINT 'You must disable Trigger "safety" to drop or alter tables!'   
   ROLLBACK;  
GO  
DISABLE TRIGGER safety ON DATABASE;  
GO  
ENABLE TRIGGER safety ON DATABASE;  
GO  
```  
  
### <a name="c-enabling-all-triggers-that-were-defined-with-the-same-scope"></a>C. Habilitar todos los desencadenadores que se definieron con el mismo ámbito  
 En el ejemplo siguiente se habilitan todos los desencadenadores DDL creados en el ámbito del servidor.  
  
**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```  
ENABLE Trigger ALL ON ALL SERVER;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [DISABLE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/disable-trigger-transact-sql.md)   
 [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [DROP TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-trigger-transact-sql.md)   
 [sys.triggers &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md)  
  
  
