---
title: SUSER_NAME (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SUSER_NAME
- SUSER_NAME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- security identification names [SQL Server]
- logins [SQL Server], users
- identification names for logins [SQL Server]
- users [SQL Server], logins
- SUSER_NAME function
- logins [SQL Server], names
- names [SQL Server], logins
ms.assetid: ae598d9f-9baa-49b8-b1c1-042854206de4
caps.latest.revision: 29
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a8d4eae9424d5c5cb2dbb2e7851d4e660fa0ba72
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="susername-transact-sql"></a>SUSER_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-xxx-md.md)]

  Devuelve el nombre de identificación de inicio de sesión del usuario.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SUSER_NAME ( [ server_user_id ] )   
```  
  
## <a name="arguments"></a>Argumentos  
 *server_user_id*  
 Es el número de identificación de inicio de sesión del usuario. *server_user_id*, que es opcional, es **int**. *server_user_id* puede ser el número de identificación de inicio de sesión de cualquier [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicio de sesión o [!INCLUDE[msCoName](../../includes/msconame-md.md)] usuario o grupo que tiene permiso para conectarse a una instancia de Windows [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si *server_user_id* no es se especifica, se devuelve el nombre de identificación de inicio de sesión para el usuario actual. Si el parámetro contiene la palabra NULL, se devolverá NULL.  
  
## <a name="return-types"></a>Tipos devueltos  
 **nvarchar (128)**  
  
## <a name="remarks"></a>Comentarios  
 En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versión 7.0, el número de identificación de seguridad (SID) reemplaza al número de identificación de usuario del servidor (SUID).  
  
 SUSER_NAME devuelve un nombre de inicio de sesión solo para un inicio de sesión que tenga una entrada en el **syslogins** tabla del sistema.  
  
 SUSER_NAME se puede utilizar en una lista de selección, en una cláusula WHERE y en cualquier lugar donde se admita una expresión, pero deberá ir seguido siempre de paréntesis, incluso si no se especifica ningún parámetro.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se devuelve el nombre de identificación de inicio de sesión del usuario con el número de identificación de inicio de sesión `1`.  
  
```  
SELECT SUSER_NAME(1);  
```  
  
## <a name="see-also"></a>Vea también  
 [SUSER_ID &#40; Transact-SQL &#41;](../../t-sql/functions/suser-id-transact-sql.md)   
 [Entidades de seguridad &#40;motor de base de datos&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  

