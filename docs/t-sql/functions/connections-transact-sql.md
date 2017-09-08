---
title: '@@CONNECTIONS (Transact-SQL) | Documentos de Microsoft'
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@CONNECTIONS'
- '@@CONNECTIONS_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@CONNECTIONS function'
- connections [SQL Server], number of
- connections [SQL Server], attempted
- number of connection attempts
- attempted connections
ms.assetid: c59836a8-443c-4b9a-8b96-8863ada97ac7
caps.latest.revision: 32
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5619f7fd0ea769af7a614178be5242174cc66fde
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="connections-transact-sql"></a>@@CONNECTIONS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Devuelve el número de intentos de conexión, ya sean correctos o no, desde que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se inició por última vez.
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
@@CONNECTIONS  
```  
  
## <a name="return-types"></a>Tipos de valor devuelto
**integer**
  
## <a name="remarks"></a>Comentarios  
Las conexiones son distintas de los usuarios. Las aplicaciones, por ejemplo, pueden abrir múltiples conexiones con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sin que el usuario las vea.
  
Para mostrar un informe que contenga varias [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estadísticas, incluidos los intentos de conexión, ejecute **sp_monitor**.
  
@@MAX_CONNECTIONS es el número máximo de conexiones permitidas para el servidor. @@CONNECTIONS se incrementa con cada intento de inicio de sesión, por lo tanto,@CONNECTIONS puede ser mayor que @@MAX_CONNECTIONS.
  
## <a name="examples"></a>Ejemplos  
El ejemplo siguiente muestra el número de intentos de inicio de sesión en la fecha y hora actuales.
  
```sql
SELECT GETDATE() AS 'Today''s Date and Time',   
@@CONNECTIONS AS 'Login Attempts';  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
  
Today's Date and Time  Login Attempts  
---------------------- --------------  
12/5/2006 10:32:45 AM  211023         
```  
  
## <a name="see-also"></a>Vea también
[Funciones estadísticas del sistema &#40; Transact-SQL &#41;](../../t-sql/functions/system-statistical-functions-transact-sql.md)  
[sp_monitor &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md)
  
  

