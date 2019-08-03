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
ms.openlocfilehash: 7927eef8105fff23a3fe790f32794fe5dd44cdae
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2019
ms.locfileid: "68769190"
---
# <a name="spaddmergealternatepublisher-transact-sql"></a>sp_addmergealternatepublisher (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Agrega la capacidad de un suscriptor para utilizar un asociado de sincronización alternativo. Las propiedades de la publicación deben especificar que los suscriptores pueden sincronizarse con otros publicadores. Este procedimiento almacenado se ejecuta en el suscriptor de la base de datos de suscripciones.  
  
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
`[ @publisher = ] 'publisher'`Es el nombre del publicador. *Publisher* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
`[ @publisher_db = ] 'publisher_db'`Es el nombre de la base de datos de publicación. *publisher_db* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
`[ @publication = ] 'publication'`Es el nombre de la publicación. *Publication* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
`[ @alternate_publisher = ] 'alternate_synchronization_partner'`Es el nombre del publicador alternativo. *alternate_synchronization_partner* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
`[ @alternate_publisher_db = ] 'alternate_publisher_db'`Es el nombre de la base de datos de publicación en el publicador alternativo. *alternate_publisher_db* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
`[ @alternate_publication = ] 'alternate_synchronization_partner'`Es el nombre de la publicación en el asociado de sincronización alternativo. *alternate_synchronization_partner* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
`[ @alternate_distributor = ] 'alternate_distributor'`Es el nombre del distribuidor para el asociado de sincronización alternativo. *alternate_distributor* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
`[ @friendly_name = ] 'friendly_name'`Es un nombre para mostrar con el que se puede identificar la Asociación del publicador, la publicación y el distribuidor que conforma un asociado de sincronización alternativo. *Nombre_descriptivo* es de tipo **nvarchar (255)** y su valor predeterminado es NULL.  
  
`[ @reserved = ] 'reserved'` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_addmergealternatepublisher** se utiliza en la replicación de mezcla.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de servidor **sysadmin** o del rol fijo de base de datos **db_owner** pueden ejecutar **sp_addmergealternatepublisher**.  
  
## <a name="see-also"></a>Vea también  
 [sp_dropmergealternatepublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergealternatepublisher-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
