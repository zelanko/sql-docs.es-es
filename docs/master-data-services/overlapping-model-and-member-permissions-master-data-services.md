---
title: "Superponer permisos de modelo y de miembro (Master Data Services) | Microsoft Docs"
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
  - "modelos [Master Data Services], permisos efectivos"
  - "permisos [Master Data Services], superposiciones de modelos y miembros"
  - "miembros [Master Data Services], permisos efectivos"
ms.assetid: 9fd7a555-43bf-4796-a8b6-1ca63a291216
caps.latest.revision: 7
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 7
---
# Superponer permisos de modelo y de miembro (Master Data Services)
  El permiso que se asigne a un miembro puede solaparse con el permiso asignado a un objeto del modelo. Cuando se producen las superposiciones, el permiso más restrictivo será el que surta efecto.  
  
 Si un miembro tiene permiso distinto al de su objeto del modelo correspondiente, se aplicarán las reglas siguientes:  
  
-   **Denegar** invalida al resto de permisos.  
  
-   **Administración** permiso en el nivel de modelo todos los permisos y se cambia a permiso de acceso de todos los (CRUD) en los niveles de sub.  
  
-   El permiso de acceso efectivo forma intersección con los permisos de los miembros y atributos.  
  
     Por ejemplo, si los permisos de miembro incluyen **Crear** y **Actualizar**, el permiso de los atributos es **Actualizar**. El permiso efectivo es **Actualizar**.  
  
 La siguiente imagen muestra qué permisos surten efecto en un valor de atributo individual cuando los permisos de atributo son diferentes que los permisos de miembro.  
  
 ![mds_conc_security_member_overlap_table](../master-data-services/media/mds-conc-security-member-overlap-table.gif "mds_conc_security_member_overlap_table")  
  
## Ejemplo 1  
 ![mds_conc_overlap_model_1](../master-data-services/media/mds-conc-overlap-model-1.gif "mds_conc_overlap_model_1")  
  
 En la pestaña **Modelos** , la entidad Product tiene asignado el permiso **Actualizar** . Todos los atributos de la entidad heredan ese permiso.  
  
 En la pestaña **Miembros de la jerarquía** , el nodo de subcategoría de bicicletas de montaña de una jerarquía derivada tiene asignado el permiso **Actualizar** .  
  
 Como consecuencia, el usuario tiene el permiso **Actualizar**para todos los valores de atributo de todos los miembros del nodo Mountain Bikes en **Explorador** . Se ocultan todos los demás miembros y atributos.  
  
 ![mds_conc_overlap_model_example_1](../master-data-services/media/mds-conc-overlap-model-example-1.gif "mds_conc_overlap_model_example_1")  
  
## Ejemplo 2  
 ![mds_conc_overlap_model_2](../master-data-services/media/mds-conc-overlap-model-2.gif "mds_conc_overlap_model_2")  
  
 En la pestaña **Modelos** , el atributo Subcategory tiene asignado el permiso **Actualizar** .  
  
 En la pestaña **Miembros de la jerarquía** , al nodo de subcategoría de bicicletas de montaña de una jerarquía derivada se le asigna el permiso de **Lectura** explícitamente.  
  
 En consecuencia, en el **Explorador**el usuario tiene el permiso de **Lectura** para los valores de atributo de subcategoría para los miembros del nodo de bicicletas de montaña. Se ocultan todos los demás miembros y atributos.  
  
 ![mds_conc_overlap_model_example_2](../master-data-services/media/mds-conc-overlap-model-example-2.gif "mds_conc_overlap_model_example_2")  
  
## Ejemplo 3  
 ![mds_conc_overlap_model_3](../master-data-services/media/mds-conc-overlap-model-3.gif "mds_conc_overlap_model_3")  
  
 En la pestaña **Modelos** , el atributo de subcategoría tiene asignado el permiso de **Lectura** .  
  
 En la pestaña **Miembros** , el nodo de subcategoría de bicicletas de montaña de una jerarquía derivada tiene asignado el permiso **Actualizar** explícitamente.  
  
 Resultado: en el **Explorador**, el usuario tiene el permiso de **Lectura** para los valores de atributo. Se ocultan todos los demás miembros y atributos.  
  
 ![mds_conc_overlap_model_example_2](../master-data-services/media/mds-conc-overlap-model-example-2.gif "mds_conc_overlap_model_example_2")  
  
## Vea también  
 [Cómo se determinan los permisos & #40; Master Data Services & #41;](../master-data-services/how-permissions-are-determined-master-data-services.md)   
 [Superposición de permisos del grupo de & usuario y Nº 40; Master Data Services & #41;](../master-data-services/overlapping-user-and-group-permissions-master-data-services.md)  
  
  