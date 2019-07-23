---
title: '@@CONNECTIONS (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/18/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: b614ba90bddad592bedbf67e82d250ea8ba51e25
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68132078"
---
# <a name="x40x40connections-transact-sql"></a>&#x40;&#x40;CONNECTIONS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Esta función devuelve el número de intentos de conexión, ya sean correctos o no, desde que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se inició por última vez.
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
@@CONNECTIONS  
```  
  
## <a name="return-types"></a>Tipos de valores devueltos
**integer**
  
## <a name="remarks"></a>Notas  
Las conexiones son distintas de los usuarios. Las aplicaciones, por ejemplo, pueden abrir múltiples conexiones con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sin que el usuario las vea.
  
Ejecute **sp_monitor** para ver un informe que contiene varias estadísticas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], incluido un número de intentos de conexión.
  
@@MAX_CONNECTIONS es el número máximo de conexiones simultáneas permitidas para el servidor. @@CONNECTIONS se incrementa con cada intento de inicio de sesión; por tanto, @@CONNECTIONS puede superar @@MAX_CONNECTIONS.
  
## <a name="examples"></a>Ejemplos  
Este ejemplo devuelve el número de intentos de inicio de sesión a partir de la fecha y hora actuales.
  
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
[Funciones estadísticas del sistema &#40;Transact-SQL&#41;](../../t-sql/functions/system-statistical-functions-transact-sql.md)  
[sp_monitor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md)
  
  
