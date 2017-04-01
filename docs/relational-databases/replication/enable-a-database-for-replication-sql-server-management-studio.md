---
title: "Habilitar una base de datos para replicaci&#243;n (SQL Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "bases de datos [replicación de SQL Server]"
ms.assetid: 8092faa3-9cff-4f81-926c-6a0070d1ce2c
caps.latest.revision: 33
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 33
---
# Habilitar una base de datos para replicaci&#243;n (SQL Server Management Studio)
  Una base de datos se habilita de forma implícita para replicación cuando un miembro del rol fijo de servidor **sysadmin** crea una publicación con el Asistente para nueva publicación. Miembro de la **sysadmin** rol fijo de servidor también puede habilitar una base de datos para la replicación de forma explícita, por lo que un miembro de la **db_owner** rol fijo de base de datos puede crear una o varias publicaciones en esa base de datos. Para habilitar una base de datos de forma explícita, utilice el **bases de datos de publicación** página de la **Propiedades del publicador: \< publicador>** cuadro de diálogo. Para obtener más información sobre el acceso a este cuadro de diálogo, vea [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md).  
  
### Para habilitar una base de datos para replicación  
  
1.  En el **bases de datos de publicación** página de la **Propiedades del publicador: \< publicador>** cuadro de diálogo, seleccione el **transaccional** o **mezcla** casilla de verificación para cada base de datos que van a replicar. Active la casilla **Transaccional** para habilitar la base de datos para replicación de instantáneas.  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
  