---
title: DBCC INPUTBUFFER (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2018
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DBCC INPUTBUFFER
- INPUTBUFFER
- DBCC_INPUTBUFFER_TSQL
- INPUTBUFFER_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- input buffers [SQL Server]
- last statement from client
- displaying last statement sent
- statements [SQL Server], last statement
- DBCC INPUTBUFFER statement
ms.assetid: a44d702b-b3fb-4950-8c8f-1adcf3f514ba
author: pmasl
ms.author: umajay
ms.openlocfilehash: d0b6f9dac0cb065a9509040b5693b09b1fa9d5e5
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "68039097"
---
# <a name="dbcc-inputbuffer-transact-sql"></a>DBCC INPUTBUFFER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Muestra la última instrucción enviada desde un cliente a una instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
DBCC INPUTBUFFER ( session_id [ , request_id ])  
[WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>Argumentos  
*session_id*  
Es el Id. de sesión asociado a cada conexión principal activa.  
  
*id_de_solicitud*  
Solicitud exacta (en lote) que se buscará en la sesión actual.  

La consulta siguiente devuelve *id_de_solicitud*:  
```sql
SELECT request_id   
FROM sys.dm_exec_requests   
WHERE session_id = @@spid;  
```  
WITH  
Habilita la especificación de opciones.  
  
NO_INFOMSGS  
Suprime todos los mensajes informativos con niveles de gravedad entre 0 y 10.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
DBCC INPUTBUFFER devuelve un conjunto de filas con las siguientes columnas.
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**EventType**|**nvarchar(30)**|Tipo de evento. Puede ser **RPC Event** o **Language Event**. La salida será **No Event** si no se detectó el último evento.|  
|**Parámetros**|**smallint**|0 = Texto<br /><br /> 1- *n* = Parámetros|  
|**EventInfo**|**nvarchar(4000)**|En un argumento **EventType** de tipo RPC, **EventInfo** contiene solo el nombre del procedimiento. Si el valor de **EventType** es Language, solo se muestran los primeros 4000 caracteres del evento.|  
  
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

## <a name="permissions"></a>Permisos  
En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es necesario cumplir una de las siguientes condiciones:
-   El usuario debe ser miembro del rol fijo de servidor **sysadmin**.  
-   El usuario debe tener el permiso VIEW SERVER STATE.  
-   *session_id* debe ser igual al identificador de sesión en el que se está ejecutando el comando. Para determinar el Id. de sesión ejecute la siguiente consulta:  
  
```sql
SELECT @@spid;  
```
  
En los niveles Premium y críticos para la empresa de [!INCLUDE[ssSDS](../../includes/sssds-md.md)] se necesita el permiso VIEW DATABASE STATE en la base de datos. En los niveles estándar, básico y de uso general de [!INCLUDE[ssSDS](../../includes/sssds-md.md)], se requiere la cuenta de administrador de [!INCLUDE[ssSDS](../../includes/sssds-md.md)].
  
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

## <a name="see-also"></a>Consulte también  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[sp_who &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)  
[sys.dm_exec_input_buffer &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-input-buffer-transact-sql.md)
  
  
