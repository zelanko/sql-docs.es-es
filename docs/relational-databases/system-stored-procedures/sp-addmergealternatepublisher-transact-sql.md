---
title: sp_addmergealternatepublisher (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addmergealternatepublisher_TSQL
- sp_addmergealternatepublisher
helpviewer_keywords:
- sp_addmergealternatepublisher
ms.assetid: de46e0b1-d946-4021-bff6-2d8e3187656d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 21d0ea34f3521333976ce00a3f5b823c3fcb816a
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/09/2019
ms.locfileid: "54129305"
---
# <a name="spaddmergealternatepublisher-transact-sql"></a>sp_addmergealternatepublisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Agrega la capacidad de un suscriptor para utilizar un asociado de sincronización alternativo. Las propiedades de la publicación deben especificar que los suscriptores pueden sincronizarse con otros publicadores. Este procedimiento almacenado se ejecuta en el suscriptor de la base de datos de suscripción.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_addmergealternatepublisher [ @publisher= ] 'publisher'  
          , [ @publisher_db= ] 'publisher_db'  
          , [ @publication= ] 'publication'  
          , [ @alternate_publisher= ] 'alternate_synchronization_partner'  
          , [ @alternate_publisher_db= ] 'alternate_publisher_db'  
          , [ @alternate_publication= ] 'alternate_synchronization_partner'  
     , [ @alternate_distributor= ] 'alternate_distributor'   
    [ , [ @friendly_name= ] 'friendly_name' ]   
    [ , [ @reserved= ] 'reserved' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publisher=**] **'**_publisher_**'**  
 Es el nombre del publicador. *publicador* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@publisher_db=**] **'**_publisher_db_**'**  
 Es el nombre de la base de datos de publicación. *publisher_db* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@publication=**] **'**_publicación_**'**  
 Es el nombre de la publicación. *publicación* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@alternate_publisher=**] **'**_alternate_synchronization_partner_**'**  
 Es el nombre del publicador alternativo. *alternate_synchronization_partner* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@alternate_publisher_db=**] **'**_publisher_db_**'**  
 Es el nombre de la base de datos de publicación en el publicador alternativo. *publisher_db* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@alternate_publication=**] **'**_alternate_synchronization_partner_**'**  
 Es el nombre de la publicación en el asociado de sincronización alternativo. *alternate_synchronization_partner* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@alternate_distributor=**] **'**_alternate_distributor_**'**  
 Es el nombre del distribuidor en el asociado de sincronización alternativo. *alternate_distributor* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@friendly_name=**] **'**_Nombre_descriptivo_**'**  
 Es un nombre para mostrar con el que se identifica la asociación del publicador, la publicación y el distribuidor que conforma un asociado de sincronización alternativo. *Nombre_descriptivo* es **nvarchar (255)**, su valor predeterminado es null.  
  
 [  **@reserved=**] **'**_reservada_**'**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_addmergealternatepublisher** se utiliza en la replicación de mezcla.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor o **db_owner** rol fijo de base de datos se puede ejecutar **sp_addmergealternatepublisher**.  
  
## <a name="see-also"></a>Vea también  
 [sp_dropmergealternatepublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergealternatepublisher-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
