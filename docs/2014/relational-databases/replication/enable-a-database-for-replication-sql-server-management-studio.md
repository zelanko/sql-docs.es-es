---
title: Habilitar una base de datos para replicación (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- databases [SQL Server replication]
ms.assetid: 8092faa3-9cff-4f81-926c-6a0070d1ce2c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 307d52e24187e35c1c30f609facd13bfad569216
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85010740"
---
# <a name="enable-a-database-for-replication-sql-server-management-studio"></a>Habilitar una base de datos para replicación (SQL Server Management Studio)
  Una base de datos se habilita de forma implícita para replicación cuando un miembro del rol fijo de servidor **sysadmin** crea una publicación con el Asistente para nueva publicación. Un miembro del rol fijo de servidor **sysadmin** también puede habilitar una base de datos para replicación de forma explícita, de manera que un miembro del rol fijo de base de datos **db_owner** pueda crear una o varias publicaciones en esa base de datos. Para habilitar una base de datos de forma explícita, utilice la página bases de datos de **publicaciones** del cuadro de diálogo **propiedades del publicador \<Publisher> :** . Para obtener más información sobre el acceso a este cuadro de diálogo, vea [Create a Publication](publish/create-a-publication.md).  
  
### <a name="to-enable-a-database-for-replication"></a>Para habilitar una base de datos para replicación  
  
1.  En la página **bases de datos de publicaciones** del cuadro de diálogo Propiedades del **publicador: \<Publisher> ** , active las casillas **transaccional** y/o **mezclar** para cada base de datos que desee replicar. Active la casilla **Transaccional** para habilitar la base de datos para replicación de instantáneas.  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
  
