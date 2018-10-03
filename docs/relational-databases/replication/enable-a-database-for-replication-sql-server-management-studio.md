---
title: Habilitar una base de datos para replicación (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- databases [SQL Server replication]
ms.assetid: 8092faa3-9cff-4f81-926c-6a0070d1ce2c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ce3bc10ad615e449da26e55d64b05ca36b6d10ca
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47729513"
---
# <a name="enable-a-database-for-replication-sql-server-management-studio"></a>Habilitar una base de datos para replicación (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Una base de datos se habilita de forma implícita para replicación cuando un miembro del rol fijo de servidor **sysadmin** crea una publicación con el Asistente para nueva publicación. Un miembro del rol fijo de servidor **sysadmin** también puede habilitar una base de datos para replicación de forma explícita, de manera que un miembro del rol fijo de base de datos **db_owner** pueda crear una o varias publicaciones en esa base de datos. Para habilitar una base de datos de forma explícita, utilice la página **Bases de datos de publicación** del cuadro de diálogo **Propiedades del publicador: \<Publicador>**. Para obtener más información sobre el acceso a este cuadro de diálogo, vea [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md).  
  
### <a name="to-enable-a-database-for-replication"></a>Para habilitar una base de datos para replicación  
  
1.  En la página **Bases de datos de publicación** del cuadro de diálogo **Propiedades del publicador: \<Publicador>**, active las casillas **Transaccional** y/o **Mezclar** para cada una de las bases de datos que desee replicar. Active la casilla **Transaccional** para habilitar la base de datos para replicación de instantáneas.  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
  
