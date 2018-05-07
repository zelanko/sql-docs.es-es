---
title: sp_dropmergealternatepublisher (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_dropmergealternatepublisher
- sp_dropmergealternatepublisher_TSQL
helpviewer_keywords:
- sp_dropmergealternatepublisher
ms.assetid: a7dee4e2-2a60-41da-9d1d-6f991d7e2c5e
caps.latest.revision: 29
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 46c3e124cee4c4d8ff9190c063433ca97f19aa72
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
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
 [  **@publisher=**] **'***publisher***'**  
 Es el nombre del publicador actual. *Publisher*es **sysname**, no tiene ningún valor predeterminado.  
  
 [ **@publisher_db=**] **'***publisher_db***'**  
 Es el nombre de la base de datos de publicación actual. *publisher_db*es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@publication =**] **'***publicación***'**  
 Es el nombre de la publicación actual. *publicación* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@alternate_publisher=**] **'***alternate_publisher***'**  
 Es el nombre del publicador alternativo que se va a quitar como asociado de sincronización alternativo. *alternate_publisher*es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@alternate_publisher_db=**] **'***publisher_db***'**  
 Es el nombre de la base de datos de publicación que se va a quitar como base de datos de publicación de asociado de sincronización alternativo. *publisher_db*es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@alternate_publication=**] **'***Alternate***'**  
 Es el nombre de la publicación que se va a quitar como la publicación de asociado de sincronización alternativo. *Alternate*es **sysname**, no tiene ningún valor predeterminado.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_dropmergealternatepublisher** se utiliza en la replicación de mezcla.  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor o el **db_owner** rol fijo de base de datos puede ejecutar **sp_dropmergelternatepublisher**.  
  
## <a name="see-also"></a>Vea también  
 [sp_addmergealternatepublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergealternatepublisher-transact-sql.md)  
  
  
