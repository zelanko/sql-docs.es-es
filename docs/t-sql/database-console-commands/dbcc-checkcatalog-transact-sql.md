---
title: DBCC CHECKCATALOG (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 11/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|database-console-commands
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DBCC_CHECKCATALOG_TSQL
- DBCC CHECKCATALOG
- CHECKCATALOG_TSQL
- CHECKCATALOG
dev_langs:
- TSQL
helpviewer_keywords:
- catalogs [SQL Server], consistency checks
- checking catalog consistency
- DBCC CHECKCATALOG statement
- integrity [SQL Server], catalogs
- consistency [SQL Server], catalogs
ms.assetid: 8076eb4e-f049-44bf-9a35-45cdd6ef0105
caps.latest.revision: 51
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f63850a2cf39d783daee65431da349d04cba3b03
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="dbcc-checkcatalog-transact-sql"></a>DBCC CHECKCATALOG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Comprueba la coherencia del catálogo en la base de datos especificada. La base de datos debe en línea.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DBCC CHECKCATALOG   
[   
    (   
    database_name | database_id | 0  
    )  
]  
    [ WITH NO_INFOMSGS ]   
```  
  
## <a name="arguments"></a>Argumentos  
 *database_name* | *database_id* | 0  
 Es el nombre o Id. de la base de datos en la que se va a comprobar la coherencia del catálogo. Si no se especifica o se especifica 0, se utiliza la base de datos actual. Nombres de base de datos deben cumplir las reglas de [identificadores](../../relational-databases/databases/database-identifiers.md).  
  
 WITH NO_INFOMSGS  
 Suprime todos los mensajes de información.  
  
## <a name="remarks"></a>Comentarios  
Cuando finaliza el comando DBCC CATALOG, se escribe un mensaje en el registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si el comando DBCC se ejecuta correctamente, el mensaje lo indica, así como el tiempo de ejecución del comando. Si el comando DBCC se detiene antes de completar la comprobación debido a un error, el mensaje indica que se ha cancelado el comando, un valor de estado y la cantidad de tiempo de ejecución del comando. En la tabla siguiente se muestran y describen los valores de estado que pueden aparecer en el mensaje.
  
|State|Description|  
|-----------|-----------------|  
|0|Se ha generado el error número 8930. Indica un daño en los metadatos que provoca la cancelación del comando DBCC.|  
|1|Se ha generado el error número 8967. Error DBCC interno.|  
|2|Error durante una reparación de base de datos en modo de emergencia.|  
|3|Indica un daño en los metadatos que provoca la cancelación del comando DBCC.|  
|4|Se ha detectado una infracción de acceso o aserción.|  
|5|Error desconocido que cancela el comando DBCC.|  
  
DBCC CHECKCATALOG realiza varias comprobaciones de coherencia entre las tablas de metadatos del sistema. DBCC CHECKCATALOG utiliza una instantánea de base de datos interna para proporcionar la coherencia transaccional que necesita para realizar estas comprobaciones. Para obtener más información, vea [ver el tamaño del archivo disperso de una instantánea de base de datos &#40; Transact-SQL &#41; ](../../relational-databases/databases/view-the-size-of-the-sparse-file-of-a-database-snapshot-transact-sql.md) y en la sección "DBCC de interno uso de instantáneas de base de datos" [DBCC &#40; Transact-SQL &#41; ](../../t-sql/database-console-commands/dbcc-transact-sql.md).
Si no se puede crear una instantánea, DBCC CHECKCATALOG adquiere un bloqueo de base de datos exclusivo para obtener la coherencia necesaria. Si se detecta cualquier incoherencia, no se podrá reparar y será necesario restaurar la base de datos a partir de una copia de seguridad.
  
> [!NOTE]  
>  Ejecutar DBCC CHECKCATALOG en **tempdb** no realiza ninguna comprobación. Esto es porque, por motivos de rendimiento, instantáneas de base de datos no están disponibles en **tempdb**. Eso significa que no es posible obtener la coherencia transaccional necesaria. Reciclar el servidor para resolver cualquier **tempdb** problemas de metadatos.  
  
> [!NOTE]  
>  DBCC CHECKCATALOG no comprueba los FILESTREAM datos. FILESTREAM almacena los objetos binarios grandes (BLBS) en el sistema de archivos.  
  
DBCC CHECKCATALOG también se ejecuta como parte de [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md).
  
## <a name="result-sets"></a>Conjuntos de resultados  
Si no se especifica una base de datos, DBCC CHECKCATALOG devuelve:
  
```sql
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
Si se especifica [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] como nombre de la base de datos, DBCC CHECKCATALOG devuelve:
  
```sql
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>Permissions  
 Debe pertenecer a la **sysadmin** fija de servidor sysadmin o el **db_owner** rol fijo de base de datos.  
  
## <a name="examples"></a>Ejemplos  
El ejemplo siguiente comprueba la integridad del catálogo tanto en la base de datos actual como en la base de datos `AdventureWorks`.
  
```sql
-- Check the current database.  
DBCC CHECKCATALOG;  
GO  
-- Check the AdventureWorks2012 database.  
DBCC CHECKCATALOG (AdventureWorks2012);  
GO  
```  
  
## <a name="see-also"></a>Vea también  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[Tablas del sistema &#40; Transact-SQL &#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)
  

