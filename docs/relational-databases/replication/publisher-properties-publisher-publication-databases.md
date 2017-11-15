---
title: "Propiedades del publicador - Publicador, Bases de datos de publicación | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.rep.configdistwizard.pubproperties.pubdb.f1
helpviewer_keywords: Publisher Properties dialog box
ms.assetid: 574ea2e7-4e7b-4733-ab52-429ca93c7b0a
caps.latest.revision: "21"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a89c93aef880f5d092c48f05bc3fef515cb8c4ff
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="publisher-properties---publisher-publication-databases"></a>Propiedades del publicador - Publicador, Bases de datos de publicaciones
  La página **Bases de datos de publicaciones** del cuadro de diálogo **Propiedades del publicador** permite a un usuario que tenga el rol fijo de servidor **sysadmin** habilitar bases de datos para replicación. Al habilitar una base de datos, ésta no se publica, sino que permite que cualquier usuario del rol fijo de base de datos **db_owner** para esa base de datos cree una o varias publicaciones en la base de datos.  
  
## <a name="options"></a>Opciones  
 **Transaccional**  
 Active esta casilla para permitir que los usuarios que tengan el rol fijo de base de datos **db_owner** creen publicaciones de instantáneas o publicaciones transaccionales en la base de datos.  
  
 **Mezcla**  
 Active esta casilla para permitir que los usuarios que tengan el rol fijo de base de datos **db_owner** creen publicaciones de combinación en la base de datos.  
  
## <a name="see-also"></a>Vea también  
 [Ver y modificar las propiedades del distribuidor y del publicador](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [Referencia de propiedades &#40;replicación&#41;](../../relational-databases/replication/properties-reference-replication.md)  
  
  
