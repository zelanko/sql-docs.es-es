---
title: DBCC CHECKCATALOG (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: pmasl
ms.author: umajay
ms.openlocfilehash: 0a19aa7e89494d27d073c1305a75c531cf3ffda0
ms.sourcegitcommit: edba1c570d4d8832502135bef093aac07e156c95
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/20/2020
ms.locfileid: "86485106"
---
# <a name="dbcc-checkcatalog-transact-sql"></a>DBCC CHECKCATALOG (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

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
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *database_name* | *database_id* | 0  
 Es el nombre o Id. de la base de datos en la que se va a comprobar la coherencia del catálogo. Si no se especifica o se especifica 0, se utiliza la base de datos actual. Los nombres de las bases de datos deben cumplir las reglas de los [identificadores](../../relational-databases/databases/database-identifiers.md).  
  
 WITH NO_INFOMSGS  
 Suprime todos los mensajes de información.  
  
## <a name="remarks"></a>Observaciones  
Cuando finaliza el comando DBCC CATALOG, se escribe un mensaje en el registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si el comando DBCC se ejecuta correctamente, el mensaje lo indica, así como el tiempo de ejecución del comando. Si el comando DBCC se detiene antes de finalizar la comprobación debido a un error, el mensaje indica que el comando se ha cancelado, un valor de estado y el tiempo de ejecución del comando. En la tabla siguiente se muestran y describen los valores de estado que pueden aparecer en el mensaje.
  
|State|Descripción|  
|-----------|-----------------|  
|0|Se ha generado el error número 8930. Indica un daño en los metadatos que provoca la cancelación del comando DBCC.|  
|1|Se ha generado el error número 8967. Error DBCC interno.|  
|2|Error durante una reparación de base de datos en modo de emergencia.|  
|3|Indica un daño en los metadatos que provoca la cancelación del comando DBCC.|  
|4|Se ha detectado una infracción de acceso o aserción.|  
|5|Error desconocido que cancela el comando DBCC.|  
  
DBCC CHECKCATALOG realiza varias comprobaciones de coherencia entre las tablas de metadatos del sistema. DBCC CHECKCATALOG utiliza una instantánea de base de datos interna para proporcionar la coherencia transaccional que necesita para realizar estas comprobaciones. Para más información, vea [Ver el tamaño del archivo disperso de una instantánea de base de datos &#40;Transact-SQL&#41;](../../relational-databases/databases/view-the-size-of-the-sparse-file-of-a-database-snapshot-transact-sql.md) y la sección "Uso de comandos DBCC en instantáneas internas de la base de datos" de [DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md).
Si no se puede crear una instantánea, DBCC CHECKCATALOG adquiere un bloqueo de base de datos exclusivo para obtener la coherencia necesaria. Si se detecta cualquier incoherencia, no se podrá reparar y será necesario restaurar la base de datos a partir de una copia de seguridad.
  
> [!NOTE]  
> Al ejecutar DBCC CHECKCATALOG en **tempdb**, no se realiza ninguna comprobación. Esto se debe a que, por motivos de rendimiento, las instantáneas de base de datos no están disponibles en **tempdb**. Eso significa que no es posible obtener la coherencia transaccional necesaria. Recicle el servidor para solucionar cualquier problema con los metadatos de **tempdb**.  
  
> [!NOTE]  
> DBCC CHECKCATALOG no comprueba los FILESTREAM datos. FILESTREAM almacena los objetos binarios grandes (BLBS) en el sistema de archivos.  
  
DBCC CHECKCATALOG se ejecuta también como parte de [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md).
  
## <a name="result-sets"></a>Conjuntos de resultados  
Si no se especifica una base de datos, DBCC CHECKCATALOG devuelve:
  
```
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
Si se especifica [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] como nombre de la base de datos, DBCC CHECKCATALOG devuelve:
  
```
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>Permisos  
 Debe pertenecer al rol fijo de servidor **sysadmin** o al rol fijo de base de datos **db_owner**.  
  
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
  
## <a name="see-also"></a>Consulte también  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[Tablas del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)
  
