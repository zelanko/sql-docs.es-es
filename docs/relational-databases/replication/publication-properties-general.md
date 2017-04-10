---
title: "Propiedades de la publicaci&#243;n, General | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.newpubwizard.pubproperties.general.f1"
ms.assetid: 7912362f-c4d6-4f60-bd39-dee1f656ed18
caps.latest.revision: 25
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 25
---
# Propiedades de la publicaci&#243;n, General
  La página **General** del cuadro de diálogo **Propiedades de la publicación** contiene información básica acerca de la publicación, incluido el nombre, la descripción y la directiva de expiración de la suscripción.  
  
## Opciones  
 **Nombre**  
 Nombre de la publicación (solo lectura).  
  
 **Base de datos**  
 Nombre de la base de datos de publicación (solo lectura).  
  
 **Descripción**  
 Descripción de la publicación.  
  
 **Tipo**  
 Tipo de publicación (solo lectura).  
  
 **Expiración de la suscripción**  
 Seleccione una de las opciones de caducidad de la suscripción: **las suscripciones no caducan nunca** o **las suscripciones caducan**, con un período de tiempo explícito (**intervalo**).  
  
 En las publicaciones de instantáneas y transaccionales, [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomienda que acepte la opción predeterminada **Las suscripciones no expiran nunca**.  
  
 En las replicaciones de mezcla, [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomienda que acepte la opción predeterminada **Las suscripciones expiran** y establezca el mínimo valor posible en **Intervalo**. A medida que aumenta el período de expiración de la suscripción, también aumentará la cantidad de datos almacenados, lo que podría afectar al rendimiento. Evalúe la necesidad de desconectar suscriptores o de sincronizarlos durante un período prolongado ante los posibles problemas de rendimiento del almacenamiento y procesamiento de grandes cantidades de metadatos.  
  
 Para más información, consulte [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md).  
  
 **nivel de compatibilidad**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y versiones posteriores únicamente; publicaciones de mezcla. Seleccione la versión mínima de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] necesaria para que los suscriptores se sincronicen con esta publicación. Existen diversas reglas asociadas a la determinación del nivel de compatibilidad.  
  
## Vea también  
 [Crear una publicación](../../relational-databases/replication/publish/create-a-publication.md)   
 [Ver y modificar propiedades de publicación](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Publicar datos y objetos de base de datos](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  