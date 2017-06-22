---
title: Tipos de suscriptor | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rep.newpubwizard.subscribertypes.f1
ms.assetid: a70656cb-21c9-4489-be77-ccd396747e3b
caps.latest.revision: 28
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ae9c8cf11d6a95554f56d6c6bde1b2eb18b36d70
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="subscriber-types"></a>Tipos de suscriptor
  La replicación de mezcla le permite especificar los tipos de suscriptor compatibles con una publicación. Si selecciona Tipos de suscriptor, podrá establecer el *nivel de compatibilidad de la publicación*, que determina las características que puede usar una publicación.  
  
 Una vez creada una instantánea de publicación, se puede aumentar (restringir) el nivel de compatibilidad de la publicación en la página **General** del cuadro de diálogo **Propiedades de la publicación** ; no se puede reducir el nivel de compatibilidad.  
  
## <a name="options"></a>Opciones  
 Seleccione los tipos de suscriptor compatibles con la publicación.  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
 La publicación podrá usar todas las características.  
  
 [!INCLUDE[ssEW](../../includes/ssew-md.md)]  
 La publicación necesita que los archivos de instantáneas tengan un formato de caracteres (el agente de instantáneas lo controlará automáticamente). [!INCLUDE[ssEW](../../includes/ssew-md.md)] también presenta varias restricciones no relacionadas con el nivel de compatibilidad.  
  
 Si selecciona esta opción, se habilitará la opción de sincronización web para la publicación. Para obtener más información acerca de la sincronización web, vea [Web Synchronization for Merge Replication](../../relational-databases/replication/web-synchronization-for-merge-replication.md).  
  
## <a name="see-also"></a>Vea también  
 [Publicar datos y objetos de base de datos](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Crear una publicación](../../relational-databases/replication/publish/create-a-publication.md)   
 [Ver y modificar las propiedades del distribuidor y del publicador](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [Referencia de propiedades &#40;replicación&#41;](../../relational-databases/replication/properties-reference-replication.md)  
  
  
