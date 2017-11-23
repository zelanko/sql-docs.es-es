---
title: sp_validate_redirected_publisher (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_validate_redirected_publisher
- sp_validate_redirected_publisher_TSQL
helpviewer_keywords: sp_validate_redirected_publisher
ms.assetid: 2b7fdbad-17e4-4442-b0b2-9b5e8f84b91d
caps.latest.revision: "9"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bafe71c88b5fc47c822275ebfb9be102db65b22b
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="spvalidateredirectedpublisher-transact-sql"></a>sp_validate_redirected_publisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Comprueba que el host actual de la base de datos de publicación admite la replicación. Debe ejecutarse desde una base de datos de distribución. Llama a este procedimiento **sp_get_redirected_publisher**.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
      sp_validate_redirected_publisher   
    [ @original_publisher = ] 'original_publisher',  
    [ @publisher_db = ] 'database_name',   
    [ @redirected_publisher = ] 'new_publisher' output  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@original_publisher**  =] **'***original_publisher***'**  
 El nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que publicó originalmente la base de datos. *original_publisher* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@publisher_db**  =] **'***publisher_db***'**  
 El nombre de la base de datos que se va a publicar. *publisher_db* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@redirected_publisher**  =] **'***redirected_publisher***'**  
 Especifica el destino de la redirección cuando **sp_redirect_publisher** se llamó para el par publicador/base de datos. *redirected_publisher* es **sysname**, no tiene ningún valor predeterminado.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Ninguno.  
  
## <a name="remarks"></a>Comentarios  
 Si no existe ninguna entrada para el publicador y la base de datos de publicación, **sp_validate_redirected_publisher** devuelve null en el parámetro de salida  *@redirected_publisher* . Si existe una entrada, esta se devuelve en el parámetro de salida en ambos casos: correcto y error.  
  
 Si la validación es correcta, **sp_validate_redirected_publisher** devuelve una indicación de éxito.  
  
 Si la validación no se realiza correctamente, se producen errores que describen el motivo.  
  
## <a name="permissions"></a>Permissions  
 Autor de la llamada debe ser un miembro de la **sysadmin** rol fijo de servidor, el **db_owner** rol fijo de base de datos para la base de datos de distribución o un miembro de una lista de acceso de publicación para una publicación definida asociado a la base de datos del publicador.  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [sp_get_redirected_publisher &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-get-redirected-publisher-transact-sql.md)   
 [sp_redirect_publisher &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-redirect-publisher-transact-sql.md)   
 [sp_validate_replica_hosts_as_publishers &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-validate-replica-hosts-as-publishers-transact-sql.md)  
  
  
