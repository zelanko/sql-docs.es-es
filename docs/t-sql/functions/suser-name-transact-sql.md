---
title: SUSER_NAME (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3b3de8ceac86cf0c08f1ff543c8d964a1960f615
ms.sourcegitcommit: b3d84abfa4e2922951430772c9f86dce450e4ed1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/22/2019
ms.locfileid: "56662639"
---
# <a name="susername-transact-sql"></a>SUSER_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-xxx-md.md)]

Devuelve el nombre de identificación de inicio de sesión del usuario.  
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SUSER_NAME ( [ server_user_id ] )   
```  
  
## <a name="arguments"></a>Argumentos  
_server\_user\_id_  
Es el número de identificación de inicio de sesión del usuario. _server\_user\_id_, que es opcional, es **int**. _server\_user\_id_ puede ser el número de identificación de inicio de sesión de cualquier inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o de cualquier usuario o grupo de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows que tenga permiso para conectarse a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si no se especifica _server\_user\_id_, se devuelve el nombre de identificación de inicio de sesión del usuario actual. Si el parámetro contiene la palabra NULL, se devolverá NULL.  
  
## <a name="return-types"></a>Tipos devueltos  
**nvarchar(128)**  
  
## <a name="remarks"></a>Notas  
En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versión 7.0, el número de identificación de seguridad (SID) reemplaza al número de identificación de usuario del servidor (SUID).  
  
SUSER_NAME solo devuelve un nombre de un inicio de sesión que tenga una entrada en la tabla del sistema **syslogins**.  
  
Se puede usar SUSER_NAME en una lista de selección, en una cláusula WHERE, y en cualquier parte en la que se permita una expresión. Use paréntesis después SUSER_NAME, incluso si no se especifica ningún parámetro.  
  
## <a name="examples"></a>Ejemplos  
En el ejemplo siguiente se devuelve el nombre de identificación de inicio de sesión del usuario con el número de identificación de inicio de sesión `1`.  
  
```  
SELECT SUSER_NAME(1);  
```  
  
## <a name="see-also"></a>Consulte también  
[SUSER_ID &#40;Transact-SQL&#41;](../../t-sql/functions/suser-id-transact-sql.md)   
[Entidades de seguridad &#40;motor de base de datos&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
