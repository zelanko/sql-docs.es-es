---
title: Propiedades del publicador - Publicador, Bases de datos de publicación | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.rep.configdistwizard.pubproperties.pubdb.f1
helpviewer_keywords:
- Publisher Properties dialog box
ms.assetid: 574ea2e7-4e7b-4733-ab52-429ca93c7b0a
caps.latest.revision: 20
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a05c853ff23e0b10434a5e4abc072c950b1cb713
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37276661"
---
# <a name="publisher-properties---publisher-publication-databases"></a>Propiedades del publicador - Publicador, Bases de datos de publicaciones
  La página **Bases de datos de publicaciones** del cuadro de diálogo **Propiedades del publicador** permite a un usuario que tenga el rol fijo de servidor **sysadmin** habilitar bases de datos para replicación. Al habilitar una base de datos, ésta no se publica, sino que permite que cualquier usuario del rol fijo de base de datos **db_owner** para esa base de datos cree una o varias publicaciones en la base de datos.  
  
## <a name="options"></a>Opciones  
 **Transaccional**  
 Active esta casilla para permitir que los usuarios que tengan el rol fijo de base de datos **db_owner** creen publicaciones de instantáneas o publicaciones transaccionales en la base de datos.  
  
 **Mezcla**  
 Active esta casilla para permitir que los usuarios que tengan el rol fijo de base de datos **db_owner** creen publicaciones de combinación en la base de datos.  
  
## <a name="see-also"></a>Vea también  
 [Ver y modificar las propiedades del distribuidor y del publicador](view-and-modify-distributor-and-publisher-properties.md)   
 [Referencia de propiedades &#40;replicación&#41;](properties-reference-replication.md)  
  
  
