---
title: sp_msx_get_account (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_msx_get_account_TSQL
- sp_msx_get_account
dev_langs: TSQL
helpviewer_keywords: sp_msx_get_account
ms.assetid: 7b478049-e2d0-4bac-865a-b97fd1d8dfbc
caps.latest.revision: "20"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a7a8702d1537ef91a5c090a8769abedefb470406
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="spmsxgetaccount-transact-sql"></a>sp_msx_get_account (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Muestra información sobre la credencial que el servidor de destino utiliza para conectarse al servidor maestro.  
  
||  
|-|  
|**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de la [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_msx_get_account  
```  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Devuelve el siguiente conjunto de resultados:  
  
|Nombre de la columna|Tipo|Description|  
|-----------------|----------|-----------------|  
|msx_connection|**int**|Número de conexión del servidor maestro.|  
|msx_credential_id|**int**|Id. de la credencial utilizada para esta conexión al servidor maestro.|  
|msx_credential_name|**sysname**|Nombre de la credencial utilizada para esta conexión al servidor maestro.|  
|msx_login_name|**nvarchar(4000)**|Nombre de dominio y nombre de usuario de Windows para la credencial.|  
  
## <a name="remarks"></a>Comentarios  
 Devuelve un conjunto de resultados vacío si no se especifica ninguna credencial para este servidor de destino. Para configurar la credencial, utilice sp_msx_set_account.  
  
## <a name="permissions"></a>Permissions  
 Requiere la pertenencia al rol fijo de servidor sysadmin.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se muestra información de la credencial que utiliza este servidor de destino para iniciar una sesión en el servidor maestro.  
  
```  
USE msdb ;  
GO  
  
EXECUTE dbo.sp_msx_get_account ;  
GO  
```  
  
 A continuación se muestra un conjunto de resultados de ejemplo:  
  
 `msx_connection msx_credential_id msx_credential_name  msx_login_name`  
  
 `-------------- ----------------- -------------------- ------------------------------`  
  
 `1              65538             MsxAccount           AdventureWorks2012\MsxAccount`  
  
## <a name="see-also"></a>Vea también  
 [Agente SQL Server almacena procedimientos &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [sp_msx_set_account &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-msx-set-account-transact-sql.md)  
  
  
