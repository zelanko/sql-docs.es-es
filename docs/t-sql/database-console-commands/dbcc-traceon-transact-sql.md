---
title: DBCC TRACEON (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 07/17/2017
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
- DBCC_TRACEON_TSQL
- TRACEON
- DBCC TRACEON
- TRACEON_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DBCC TRACEON statement
- trace flags [SQL Server], enabling
ms.assetid: 93085324-ebaa-4e38-aac8-5e57b4b0d36d
caps.latest.revision: 36
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e1950c1ab5214066a92a037358c26f7edd054aa0
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="dbcc-traceon-transact-sql"></a>DBCC TRACEON (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Habilita las marcas de seguimiento especificadas.
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
DBCC TRACEON ( trace# [ ,...n ][ , -1 ] ) [ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>Argumentos  
*Trace #*  
Es el número de la marca de seguimiento que se va a activar.  
  
*n*  
Es una marca de posición que indica que se pueden especificar varias marcas de seguimiento.  
  
-1  
Activa las marcas de seguimiento especificadas de forma global.  
  
WITH NO_INFOMSGS  
Suprime todos los mensajes de información.  
  
## <a name="remarks"></a>Comentarios  
En un servidor de producción, para evitar un comportamiento impredecible, se recomienda habilitar únicamente marcas de seguimiento en todo el servidor mediante uno de los siguientes métodos:
-   Use la **-T** opción de línea de comandos de inicio de Sqlservr.exe. Es una práctica recomendada porque garantiza que todas las instrucciones se ejecutarán con la marca de seguimiento habilitada. Incluye comandos en scripts de inicio. Para más información, consulte [sqlservr Application](../../tools/sqlservr-application.md).  
-   Use DBCC TRACEON **(***trace #* [**,** ... *.n*]**, -1)** solo mientras los usuarios o aplicaciones no ejecuten simultáneamente instrucciones en el sistema.  

Las marcas de seguimiento se utilizan para personalizar algunas características controlando el funcionamiento de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Las marcas de seguimiento, una vez habilitadas, permanecen habilitadas en el servidor hasta que son deshabilitadas al ejecutarse una instrucción DBCC TRACEOFF. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], hay dos tipos de marcas de seguimiento: sesión y global. Las marcas de seguimiento de sesión se activan para una conexión y solo están visibles para esa conexión. Las marcas de seguimiento globales se establecen en el nivel del servidor y están visibles para todas las conexiones del servidor. Para determinar el estado de las marcas de seguimiento, utilice DBCC TRACESTATUS. Para deshabilitar marcas de seguimiento, utilice DBCC TRACEOFF.
  
Después de activar una marca de seguimiento que afecta a los planes de consulta, ejecute `DBCC FREEPROCCACHE;` para que se vuelve a compilar planes almacenados en caché con el nuevo plan afecta al comportamiento.
  
## <a name="result-sets"></a>Conjuntos de resultados  
 DBCC TRACEON devuelve el siguiente conjunto de resultados (mensaje):  
  
```sql
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>Permissions  
Requiere la pertenencia al rol fijo de servidor **sysadmin** .
  
## <a name="examples"></a>Ejemplos  
En el ejemplo siguiente se deshabilita la compresión de hardware para controladores de cinta activando una marca de seguimiento `3205`. Esta marca solo se activa para la conexión actual.
  
```sql  
DBCC TRACEON (3205);  
GO  
```  
  
En el siguiente ejemplo se activa la marca de seguimiento `3205` de forma global.
  
```sql  
DBCC TRACEON (3205, -1);  
GO  
```  
  
En el siguiente ejemplo se activan las marca de seguimiento `3205` y `260` de forma global.
  
```sql  
DBCC TRACEON (3205, 260, -1);  
GO  
```  
  
## <a name="see-also"></a>Vea también  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[DBCC TRACEOFF &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceoff-transact-sql.md)  
[DBCC TRACESTATUS &#40; Transact-SQL &#41;](../../t-sql/database-console-commands/dbcc-tracestatus-transact-sql.md)  
[Marcas de seguimiento &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)  
[Habilitar que afectan al plan consulta optimizador comportamiento de SQL Server que puede controlarse mediante distintas marcas de seguimiento en un nivel de consulta específica](https://support.microsoft.com/kb/2801413)
  
  

