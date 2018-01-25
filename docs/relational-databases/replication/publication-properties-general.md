---
title: "Propiedades de la publicación, General | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.rep.newpubwizard.pubproperties.general.f1
ms.assetid: 7912362f-c4d6-4f60-bd39-dee1f656ed18
caps.latest.revision: "25"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dcf399256c9dd1a691211e7d6188ec869abafd21
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/18/2018
---
# <a name="publication-properties-general"></a>Propiedades de la publicación, General
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] La página **General** del cuadro de diálogo **Propiedades de la publicación** contiene información básica acerca de la publicación, incluido el nombre, la descripción y la directiva de expiración de la suscripción.  
  
## <a name="options"></a>.  
 **Nombre**  
 Nombre de la publicación (solo lectura).  
  
 **Base de datos**  
 Nombre de la base de datos de publicación (solo lectura).  
  
 **Descripción**  
 Descripción de la publicación.  
  
 **Tipo**  
 Tipo de publicación (solo lectura).  
  
 **Expiración de la suscripción**  
 Seleccione una de las opciones para la expiración de la suscripción: **Las suscripciones no expiran nunca** o **Las suscripciones expiran**, con un período de tiempo explícito (**Intervalo**).  
  
 En las publicaciones de instantáneas y transaccionales, [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomienda que acepte la opción predeterminada **Las suscripciones no expiran nunca**.  
  
 En las replicaciones de mezcla, [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomienda que acepte la opción predeterminada **Las suscripciones expiran** y establezca el mínimo valor posible en **Intervalo**. A medida que aumenta el período de expiración de la suscripción, también aumentará la cantidad de datos almacenados, lo que podría afectar al rendimiento. Evalúe la necesidad de desconectar suscriptores o de sincronizarlos durante un período prolongado ante los posibles problemas de rendimiento del almacenamiento y procesamiento de grandes cantidades de metadatos.  
  
 Para más información, consulte [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md).  
  
 **Nivel de compatibilidad**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y versiones posteriores solamente, publicaciones de combinación solamente. Seleccione la versión mínima de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] necesaria para que los suscriptores se sincronicen con esta publicación. Existen diversas reglas asociadas a la determinación del nivel de compatibilidad.  
  
## <a name="see-also"></a>Ver también  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Ver y modificar propiedades de publicación](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Publicar datos y objetos de base de datos](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
