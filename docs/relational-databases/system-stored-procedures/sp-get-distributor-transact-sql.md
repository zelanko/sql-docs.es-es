---
title: sp_get_distributor (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_get_distributor
- sp_get_distributor_TSQL
helpviewer_keywords:
- sp_get_distributor
ms.assetid: f0134448-bc17-4f2f-bd81-619351ce56ac
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ccdc8529bb62e4e1db15f0a5ea85a64c5b679abf
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62521020"
---
# <a name="spgetdistributor-transact-sql"></a>sp_get_distributor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Determina si hay un distribuidor instalado en un servidor. Este procedimiento almacenado se ejecuta en el equipo donde se está buscando el distribuidor, en cualquier base de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_get_distributor   
```  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**installed**|**int**|**0** = No; **1** = yes|  
|**servidor de distribución**|**sysname**|Nombre del servidor distribuidor|  
|**base de datos de distribución instalada**|**int**|**0** = No; **1** = yes|  
|**es el publicador de distribución**|**int**|**0** = No; **1** = yes|  
|**con publicador de distribución remoto**|**int**|**0** = No; **1** = yes|  
  
## <a name="remarks"></a>Comentarios  
 **sp_get_distributor** se usa principalmente en el [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] en instantáneas, transaccional y replicación de mezcla.  
  
## <a name="permissions"></a>Permisos  
 Cualquier usuario puede ejecutar **sp_get_distributor**. Un conjunto de resultados distinto de NULL se devuelve cuando este almacenado se ejecuta el procedimiento los miembros de la **db_owner** o **replmonitor** roles fijos de base de datos la base de datos de distribución o los miembros de la  **db_owner** rol fijo de base de datos en al menos una base de datos publicada. Un conjunto de resultados no NULL también se devuelve cuando se ejecuta este procedimiento almacenado por los usuarios en la lista de acceso de publicación (PAL) de al menos una base de datos publicada, o en la lista PAL de la base de datos de distribución para un publicador que no es - SQL Server, también puede ejecutar **sp _get_distributor**.  
  
## <a name="see-also"></a>Vea también  
 [Configurar la publicación y la distribución](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [Distributor and Publisher Information Script](../../relational-databases/replication/administration/distributor-and-publisher-information-script.md)  (Script de información del distribuidor y del publicador)  
 [Procedimientos almacenados de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
