---
title: SUSER_ID (Transact-SQL) | Documentos de Microsoft
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
- SUSER_ID_TSQL
- SUSER_ID
dev_langs:
- TSQL
helpviewer_keywords:
- users [SQL Server], IDs
- logins [SQL Server], IDs
- SUSER_ID function
- IDs [SQL Server], logins
- identification numbers [SQL Server], logins
- user IDs [SQL Server]
ms.assetid: 348911ab-b0b6-4867-aee7-e6f42e053a4a
caps.latest.revision: 22
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7e098c614f4e70cabf718ee4413920e61eb634c1
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="suserid-transact-sql"></a>SUSER_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve el número de identificación de inicio de sesión del usuario.  
  
> [!NOTE]  
>  A partir de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], SUSER_ID devuelve el valor que aparece como **principal_id** en el **sys.server_principals** vista de catálogo.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SUSER_ID ( [ 'login' ] )   
```  
  
## <a name="arguments"></a>Argumentos  
 **'** *inicio de sesión* **'**  
 Nombre de inicio de sesión del usuario. *inicio de sesión* es **nchar**. Si *inicio de sesión* se especifica como **char**, *inicio de sesión* se convierte implícitamente en **nchar**. *inicio de sesión* puede ser cualquier [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicio de sesión o usuario de Windows o grupo que tiene permiso para conectarse a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si *inicio de sesión* no es se especifica, se devuelve el número de identificación de inicio de sesión del usuario actual. Si el parámetro contiene la palabra NULL, se devolverá NULL.  
  
## <a name="return-types"></a>Tipos devueltos  
 **int**  
  
## <a name="remarks"></a>Comentarios  
 SUSER_ID devuelve un número de identificación solo para los inicios de sesión aprovisionados de forma explícita en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Este Id. se utiliza en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para realizar un seguimiento de la propiedad y los permisos. Este Id. no equivale al SID del inicio de sesión devuelto por SUSER_SID. Si *inicio de sesión* es un inicio de sesión de SQL Server, el SID se asigna a un GUID. Si *inicio de sesión* es un inicio de sesión de Windows o grupo de Windows, el SID se asigna a un identificador de seguridad de Windows.  
  
 SUSER_SID devuelve el SUID solo para un inicio de sesión que tenga una entrada en el **syslogins** tabla del sistema.  
  
 Es posible utilizar funciones de sistema en la lista de selección, en la cláusula WHERE y en cualquier lugar donde se admita una expresión, pero deberán ir seguidas siempre de paréntesis incluso si no se especifica ningún parámetro.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se obtiene el número de identificación del nombre de inicio de sesión `sa`.  
  
```  
SELECT SUSER_ID('sa');  
```  
  
## <a name="see-also"></a>Vea también  
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [SUSER_SID &#40; Transact-SQL &#41;](../../t-sql/functions/suser-sid-transact-sql.md)   
 [Funciones del sistema &#40; Transact-SQL &#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)  
  
  
