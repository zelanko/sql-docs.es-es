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
manager: craigg
ms.openlocfilehash: 722a8092a799695be0ab5e4f6925cd7416b7c1b9
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/09/2019
ms.locfileid: "54134725"
---
# <a name="spdropmergealternatepublisher-transact-sql"></a>sp_dropmergealternatepublisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Quita un publicador alternativo de una publicación de combinación. Este procedimiento almacenado se ejecuta en el suscriptor de la base de datos de suscripción.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_dropmergealaternatepublisher [ @publisher = ] 'publisher'    , [ @publisher_db = ] 'publisher_db'    , [ @publication = ] 'publication'    , [ @alternate_publisher = ] 'alternate_publisher'    , [ @alternate_publisher_db = ] 'alternate_publisher_db'    , [ @alternate_publication = ] 'alternate_publication'  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publisher=**] **'**_publisher_**'**  
 Es el nombre del publicador actual. *publicador*es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@publisher_db=**] **'**_publisher_db_**'**  
 Es el nombre de la base de datos de publicación actual. *publisher_db*es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@publication =**] **'**_publicación_**'**  
 Es el nombre de la publicación actual. *publicación* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@alternate_publisher=**] **'**_alternate_publisher_**'**  
 Es el nombre del publicador alternativo que se va a quitar como asociado de sincronización alternativo. *alternate_publisher*es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@alternate_publisher_db=**] **'**_publisher_db_**'**  
 Es el nombre de la base de datos de publicación que se va a quitar como base de datos de publicación de asociado de sincronización alternativo. *publisher_db*es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@alternate_publication=**] **'**_Alternate_**'**  
 Es el nombre de la publicación que se va a quitar como la publicación de asociado de sincronización alternativo. *Alternate*es **sysname**, no tiene ningún valor predeterminado.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_dropmergealternatepublisher** se utiliza en la replicación de mezcla.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor o el **db_owner** rol fijo de base de datos se puede ejecutar **sp_dropmergelternatepublisher**.  
  
## <a name="see-also"></a>Vea también  
 [sp_addmergealternatepublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergealternatepublisher-transact-sql.md)  
  
  
