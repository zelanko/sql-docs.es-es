---
title: Tipos de suscriptor | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.newpubwizard.subscribertypes.f1
ms.assetid: a70656cb-21c9-4489-be77-ccd396747e3b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b9445c7b366a43253da4accabaf98d9c5b7f8d92
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62630639"
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
  
 Si selecciona esta opción, se habilitará la opción de sincronización web para la publicación. Para obtener más información acerca de la sincronización web, vea [Web Synchronization for Merge Replication](web-synchronization-for-merge-replication.md).  
  
## <a name="see-also"></a>Vea también  
 [Publicar datos y objetos de base de datos](publish/publish-data-and-database-objects.md)   
 [Create a Publication](publish/create-a-publication.md)   
 [Ver y modificar las propiedades del distribuidor y del publicador](view-and-modify-distributor-and-publisher-properties.md)   

  
