---
title: Base de datos de publicación | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.rep.newpubwizard.publicationdatabase.f1
ms.assetid: a9fafc9b-9963-4b59-97a0-3472158fa665
caps.latest.revision: 23
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a769b77c22c733d2ce99ee1c9dffeee63a148b0b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="publication-database"></a>Base de datos de publicaciones
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  La base de datos de publicaciones es la base de datos del publicador que es el origen de los datos y objetos de base de datos que va a replicar. Deberá habilitar cada base de datos de publicaciones utilizada en la replicación. La base de datos se habilita cuando un miembro del rol fijo del servidor **sysadmin** :  
  
-   Crea una publicación en esa base de datos con el Asistente para nueva publicación.  
  
-   Selecciona la base de datos en el cuadro de diálogo **Propiedades del publicador** .  
  
-   Ejecuta **sp_replicationdboption** y establece **True** en la opción **publish** (para publicaciones transaccionales o de instantáneas) o **merge publish**(para publicaciones de combinación).  
  
## <a name="options"></a>Opciones  
 **Bases de datos**  
 Seleccione el nombre de la base de datos que contiene los datos o los objetos de base de datos que desea publicar.  
  
## <a name="see-also"></a>Ver también  
 [Publicar datos y objetos de base de datos](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Ver y modificar las propiedades del distribuidor y del publicador](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [sp_replicationdboption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md)  
  
  
