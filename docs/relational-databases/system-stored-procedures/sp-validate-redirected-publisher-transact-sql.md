---
title: sp_validate_redirected_publisher (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_validate_redirected_publisher
- sp_validate_redirected_publisher_TSQL
helpviewer_keywords:
- sp_validate_redirected_publisher
ms.assetid: 2b7fdbad-17e4-4442-b0b2-9b5e8f84b91d
author: stevestein
ms.author: sstein
ms.openlocfilehash: b01fba8260e86d135e740964022187b9914e5fc0
ms.sourcegitcommit: c426c7ef99ffaa9e91a93ef653cd6bf3bfd42132
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/10/2019
ms.locfileid: "72252053"
---
# <a name="sp_validate_redirected_publisher-transact-sql"></a>sp_validate_redirected_publisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Comprueba que el host actual de la base de datos de publicación admite la replicación. Debe ejecutarse desde una base de datos de distribución. **Sp_get_redirected_publisher**llama a este procedimiento.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
      sp_validate_redirected_publisher   
    [ @original_publisher = ] 'original_publisher',  
    [ @publisher_db = ] 'database_name',   
    [ @redirected_publisher = ] 'new_publisher' output  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @original_publisher = ] 'original_publisher'` el nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que publicó originalmente la base de datos. *original_publisher* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
`[ @publisher_db = ] 'publisher_db'` el nombre de la base de datos que se está publicando. *publisher_db* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
`[ @redirected_publisher = ] 'redirected_publisher'` el destino de la redirección especificada cuando se llamó a **sp_redirect_publisher** para el par publicador/base de datos. *redirected_publisher* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Ninguno.  
  
## <a name="remarks"></a>Remarks  
 Si no existe ninguna entrada para el publicador y la base de datos de publicación, **sp_validate_redirected_publisher** devuelve null en el parámetro de salida *\@redirected_publisher*. Si existe una entrada, esta se devuelve en el parámetro de salida en ambos casos: correcto y error.  
  
 Si la validación se realiza correctamente, **sp_validate_redirected_publisher** devuelve una indicación de éxito.  
  
 Si la validación no se realiza correctamente, se producen errores que describen el motivo.  
  
## <a name="permissions"></a>Permisos  
 El autor de la llamada debe ser miembro del rol fijo de servidor **sysadmin** , el rol fijo de base de datos **db_owner** para la base de datos de distribución, o un miembro de una lista de acceso a la publicación para una publicación definida asociada a la base de datos del publicador.  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [sp_get_redirected_publisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-get-redirected-publisher-transact-sql.md)   
 [sp_redirect_publisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-redirect-publisher-transact-sql.md)   
 [sp_validate_replica_hosts_as_publishers &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-validate-replica-hosts-as-publishers-transact-sql.md)  
  
  
