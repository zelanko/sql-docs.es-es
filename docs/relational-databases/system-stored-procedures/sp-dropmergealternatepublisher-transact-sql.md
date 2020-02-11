---
title: sp_dropmergealternatepublisher (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropmergealternatepublisher
- sp_dropmergealternatepublisher_TSQL
helpviewer_keywords:
- sp_dropmergealternatepublisher
ms.assetid: a7dee4e2-2a60-41da-9d1d-6f991d7e2c5e
author: stevestein
ms.author: sstein
ms.openlocfilehash: b6938a94b2cfe322abf55cbf663f91b4328c2120
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68054291"
---
# <a name="sp_dropmergealternatepublisher-transact-sql"></a>sp_dropmergealternatepublisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Quita un publicador alternativo de una publicación de combinación. Este procedimiento almacenado se ejecuta en el suscriptor de la base de datos de suscripciones.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_dropmergealaternatepublisher [ @publisher = ] 'publisher'    , [ @publisher_db = ] 'publisher_db'    , [ @publication = ] 'publication'    , [ @alternate_publisher = ] 'alternate_publisher'    , [ @alternate_publisher_db = ] 'alternate_publisher_db'    , [ @alternate_publication = ] 'alternate_publication'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publisher = ] 'publisher'`Es el nombre del publicador actual. *Publisher*es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
`[ @publisher_db = ] 'publisher_db'`Es el nombre de la base de datos de publicación actual. *publisher_db*es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
`[ @publication = ] 'publication'`Es el nombre de la publicación actual. *Publication* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
`[ @alternate_publisher = ] 'alternate_publisher'`Es el nombre del publicador alternativo que se va a quitar como asociado de sincronización alternativo. *alternate_publisher*es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
`[ @alternate_publisher_db = ] 'alternate_publisher_db'`Es el nombre de la base de datos de publicación que se va a quitar como base de datos de publicación de asociados de sincronización alternativos. *alternate_publisher_db*es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
`[ @alternate_publication = ] 'alternate_publication'`Es el nombre de la publicación que se va a quitar como la publicación de asociado de sincronización alternativo. *alternate_publication*es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Observaciones  
 **sp_dropmergealternatepublisher** se utiliza en la replicación de mezcla.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de servidor **sysadmin** o del rol fijo de base de datos **db_owner** pueden ejecutar **sp_dropmergelternatepublisher**.  
  
## <a name="see-also"></a>Consulte también  
 [sp_addmergealternatepublisher &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-addmergealternatepublisher-transact-sql.md)  
  
  
