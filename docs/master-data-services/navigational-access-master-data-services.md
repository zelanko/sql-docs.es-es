---
title: "Acceso por navegaci&#243;n (Master Data Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "acceso por navegación [Master Data Services]"
  - "seguridad (Master Data Services), acceso por navegación"
ms.assetid: 3403b7b0-44e2-48c3-a1b7-9c4612b874b8
caps.latest.revision: 5
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 5
---
# Acceso por navegaci&#243;n (Master Data Services)
  El acceso por navegación se aplica a la seguridad de los objetos de modelos, que se asigna en la pestaña **Modelos** .  
  
 El acceso por navegación es el que se obtiene en niveles superiores a los que su seguridad le haya asignado.  
  
 En este ejemplo, los permisos se asignan a una entidad y el acceso por navegación se concede en el nivel de modelo.  
  
 ![mds_conc_inheritance_model](../master-data-services/media/mds-conc-inheritance-model.gif "mds_conc_inheritance_model")  
  
 **Entidades**  
  
 Cuando se asigna permiso a una entidad, a sus miembros hoja o a sus miembros consolidados, el acceso por navegación significa que se pueden leer o actualizar el nombre y el código de todos los miembros. También se puede leer el nombre del modelo.  
  
 **Atributos**  
  
 Cuando se asigna permiso a un atributo, el acceso por navegación significa que se pueden leer o actualizar el nombre y el código de todos los miembros de la entidad. También se puede leer el nombre del modelo.  
  
 **Colecciones**  
  
 Cuando se asignan permisos a las colecciones, se pueden leer o actualizar el nombre, el código, la descripción y el identificador del propietario. También se puede leer el nombre del modelo.  
  
## Vea también  
 [Cómo se determinan los permisos &#40;Master Data Services&#41;](../master-data-services/how-permissions-are-determined-master-data-services.md)  
  
  