---
title: "Base de datos de publicación | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.rep.newpubwizard.publicationdatabase.f1
ms.assetid: a9fafc9b-9963-4b59-97a0-3472158fa665
caps.latest.revision: "23"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6247209184fd98d76c2d1b2be193e085a0336ceb
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/18/2018
---
# <a name="publication-database"></a>Base de datos de publicaciones
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] La base de datos de publicaciones es la base de datos del publicador que es el origen de los datos y objetos de base de datos que se van a replicar. Deberá habilitar cada base de datos de publicaciones utilizada en la replicación. La base de datos se habilita cuando un miembro del rol fijo del servidor **sysadmin** :  
  
-   Crea una publicación en esa base de datos con el Asistente para nueva publicación.  
  
-   Selecciona la base de datos en el cuadro de diálogo **Propiedades del publicador** .  
  
-   Ejecuta **sp_replicationdboption** y establece **True** en la opción **publish** (para publicaciones transaccionales o de instantáneas) o **merge publish**(para publicaciones de combinación).  
  
## <a name="options"></a>.  
 **Bases de datos**  
 Seleccione el nombre de la base de datos que contiene los datos o los objetos de base de datos que desea publicar.  
  
## <a name="see-also"></a>Ver también  
 [Publicar datos y objetos de base de datos](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Ver y modificar las propiedades del distribuidor y del publicador](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [sp_replicationdboption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md)  
  
  
