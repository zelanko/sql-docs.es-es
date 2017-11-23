---
title: DBCC INPUTBUFFER (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 11/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|database-console-commands
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DBCC INPUTBUFFER
- INPUTBUFFER
- DBCC_INPUTBUFFER_TSQL
- INPUTBUFFER_TSQL
dev_langs: TSQL
helpviewer_keywords:
- input buffers [SQL Server]
- last statement from client
- displaying last statement sent
- statements [SQL Server], last statement
- DBCC INPUTBUFFER statement
ms.assetid: a44d702b-b3fb-4950-8c8f-1adcf3f514ba
caps.latest.revision: "51"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 23ac916dccb2f8d4c6511f9e672aa07834001cad
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="dbcc-inputbuffer-transact-sql"></a>DBCC INPUTBUFFER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Muestra la última instrucción enviada desde el cliente a una instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
DBCC INPUTBUFFER ( session_id [ , request_id ])  
[WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>Argumentos  
*session_id*  
Es el Id. de sesión asociado a cada conexión principal activa.  
  
*request_id*  
Solicitud exacta (en lote) que se buscará en la sesión actual.  

La siguiente consulta devuelve *request_id*:  
```sql
SELECT request_id   
FROM sys.dm_exec_requests   
WHERE session_id = @@spid;  
```  
por  
Habilita la especificación de opciones.  
  
NO_INFOMSGS  
Suprime todos los mensajes informativos con niveles de gravedad entre 0 y 10.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
DBCC INPUTBUFFER devuelve un conjunto de filas con las siguientes columnas.
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**EventType**|**nvarchar (30)**|Tipo de evento. Esto podría ser **RPC Event** o **eventos de lenguaje**. El resultado será **No Event** cuando no se detectó ningún último evento.|  
|**Parámetros**|**smallint**|0 = Texto<br /><br /> 1 -  *n*  = parámetros|  
|**EventInfo**|**nvarchar(4000)**|Para una **EventType** de RPC, **EventInfo** contiene solo el nombre del procedimiento. Para una **EventType** del lenguaje, se muestran solo los primeros 4.000 caracteres del evento.|  
  
Por ejemplo, DBCC INPUTBUFFER devuelve el siguiente conjunto de resultados cuando el último evento del búfer es DBCC INPUTBUFFER(11).
  
```
EventType      Parameters EventInfo               
-------------- ---------- ---------------------   
Language Event 0          DBCC INPUTBUFFER (11)  
  
(1 row(s) affected)  
  
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  

> [!NOTE]
> A partir de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2, use [sys.dm_exec_input_buffer](../../relational-databases/system-dynamic-management-views/sys-dm-exec-input-buffer-transact-sql.md) para devolver información sobre las instrucciones enviadas a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

## <a name="permissions"></a>Permissions  
En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] requiere uno de los siguientes:
-   Usuario debe ser un miembro de la **sysadmin** rol fijo de servidor.  
-   El usuario debe tener el permiso VIEW SERVER STATE.  
-   *session_id* debe ser el mismo que el identificador de sesión en el que se está ejecutando el comando. Para determinar el Id. de sesión ejecute la siguiente consulta:  
  
```sql
SELECT @@spid;  
```
  
En [!INCLUDE[ssSDS](../../includes/sssds-md.md)] niveles Premium requieren el permiso VIEW DATABASE STATE en la base de datos. En [!INCLUDE[ssSDS](../../includes/sssds-md.md)] niveles estándar y básico requiere la [!INCLUDE[ssSDS](../../includes/sssds-md.md)] cuenta de administrador.
  
## <a name="examples"></a>Ejemplos  
En el ejemplo siguiente se ejecuta `DBCC INPUTBUFFER` en una segunda conexión mientras una transacción larga se ejecuta en una conexión anterior.
  
```sql
CREATE TABLE dbo.T1 (Col1 int, Col2 char(3));  
GO  
DECLARE @i int = 0;  
BEGIN TRAN  
SET @i = 0;  
WHILE (@i < 100000)  
BEGIN  
INSERT INTO dbo.T1 VALUES (@i, CAST(@i AS char(3)));  
SET @i += 1;  
END;  
COMMIT TRAN;  
--Start new connection #2.  
DBCC INPUTBUFFER (52);  
```  

## <a name="see-also"></a>Vea también  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[sp_who &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)  
[Sys.dm_exec_input_buffer &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-input-buffer-transact-sql.md)
  
  
