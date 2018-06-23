---
title: Base de datos de publicación | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.rep.newpubwizard.publicationdatabase.f1
ms.assetid: a9fafc9b-9963-4b59-97a0-3472158fa665
caps.latest.revision: 22
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: cb4f3f0e770b1511145f079908e0fd019d1b0c57
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36111984"
---
# <a name="publication-database"></a>Base de datos de publicaciones
  La base de datos de publicaciones es la base de datos del publicador que es el origen de los datos y objetos de base de datos que va a replicar. Deberá habilitar cada base de datos de publicaciones utilizada en la replicación. La base de datos se habilita cuando un miembro del rol fijo del servidor **sysadmin** :  
  
-   Crea una publicación en esa base de datos con el Asistente para nueva publicación.  
  
-   Selecciona la base de datos en el cuadro de diálogo **Propiedades del publicador** .  
  
-   Ejecuta **sp_replicationdboption** y establece **True** en la opción **publish** (para publicaciones transaccionales o de instantáneas) o **merge publish**(para publicaciones de combinación).  
  
## <a name="options"></a>Opciones  
 **Bases de datos**  
 Seleccione el nombre de la base de datos que contiene los datos o los objetos de base de datos que desea publicar.  
  
## <a name="see-also"></a>Vea también  
 [Publicar datos y objetos de base de datos](publish/publish-data-and-database-objects.md)   
 [Create a Publication](publish/create-a-publication.md)   
 [Ver y modificar las propiedades del distribuidor y del publicador](view-and-modify-distributor-and-publisher-properties.md)   
 [sp_replicationdboption &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql)  
  
  
