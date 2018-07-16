---
title: Superponer permisos de modelo y de miembro (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- models [Master Data Services], effective permissions
- permissions [Master Data Services], model and member overlaps
- members [Master Data Services], effective permissions
ms.assetid: 9fd7a555-43bf-4796-a8b6-1ca63a291216
caps.latest.revision: 5
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 468d23a4bddd0df301d263e6c2fd6e22a167ef27
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37219685"
---
# <a name="overlapping-model-and-member-permissions-master-data-services"></a>Superponer permisos de modelo y de miembro (Master Data Services)
  El permiso que se asigne a un miembro puede solaparse con el permiso asignado a un objeto del modelo. Cuando se producen las superposiciones, el permiso más restrictivo será el que surta efecto.  
  
 Si un miembro tiene permiso distinto al de su objeto del modelo correspondiente, se aplicarán las reglas siguientes:  
  
-   **Denegar** invalida al resto de permisos.  
  
-   **Solo lectura** invalida **actualización**.  
  
 La siguiente imagen muestra qué permisos surten efecto en un valor de atributo individual cuando los permisos de atributo son diferentes que los permisos de miembro.  
  
 ![mds_conc_security_member_overlap_table](../../2014/master-data-services/media/mds-conc-security-member-overlap-table.gif "mds_conc_security_member_overlap_table")  
  
## <a name="example-1"></a>Ejemplo 1  
 ![mds_conc_overlap_model_1](../../2014/master-data-services/media/mds-conc-overlap-model-1.gif "mds_conc_overlap_model_1")  
  
 En la pestaña **Modelos** , la entidad Product tiene asignado el permiso **Actualizar** . Todos los atributos de la entidad heredan ese permiso.  
  
 En la pestaña **Miembros de la jerarquía** , el nodo de subcategoría de bicicletas de montaña de una jerarquía derivada tiene asignado el permiso **Actualizar** .  
  
 Como consecuencia, el usuario tiene el permiso **Actualizar**para todos los valores de atributo de todos los miembros del nodo Mountain Bikes en **Explorador** . Se ocultan todos los demás miembros y atributos.  
  
 ![mds_conc_overlap_model_example_1](../../2014/master-data-services/media/mds-conc-overlap-model-example-1.gif "mds_conc_overlap_model_example_1")  
  
## <a name="example-2"></a>Ejemplo 2  
 ![mds_conc_overlap_model_2](../../2014/master-data-services/media/mds-conc-overlap-model-2.gif "mds_conc_overlap_model_2")  
  
 En la pestaña **Modelos** , el atributo Subcategory tiene asignado el permiso **Actualizar** .  
  
 En el **miembros de la jerarquía** ficha, el nodo de subcategoría de bicicletas de montaña de una jerarquía derivada se asigna explícitamente **de sólo lectura** permiso.  
  
 Resultado: En **Explorer**, el usuario tiene **de sólo lectura** permiso para los valores de atributo de subcategoría para los miembros en el nodo de bicicletas de montaña. Se ocultan todos los demás miembros y atributos.  
  
 ![mds_conc_overlap_model_example_2](../../2014/master-data-services/media/mds-conc-overlap-model-example-2.gif "mds_conc_overlap_model_example_2")  
  
## <a name="example-3"></a>Ejemplo 3  
 ![mds_conc_overlap_model_3](../../2014/master-data-services/media/mds-conc-overlap-model-3.gif "mds_conc_overlap_model_3")  
  
 En el **modelos** ficha, el atributo Subcategory tiene **de sólo lectura** asignado el permiso.  
  
 En la pestaña **Miembros** , el nodo de subcategoría de bicicletas de montaña de una jerarquía derivada tiene asignado el permiso **Actualizar** explícitamente.  
  
 Resultado: En **Explorer**, el usuario tiene **de sólo lectura** permiso a los valores de atributo. Se ocultan todos los demás miembros y atributos.  
  
 ![mds_conc_overlap_model_example_2](../../2014/master-data-services/media/mds-conc-overlap-model-example-2.gif "mds_conc_overlap_model_example_2")  
  
## <a name="see-also"></a>Vea también  
 [¿Cómo se determinan los permisos &#40;Master Data Services&#41;](how-permissions-are-determined-master-data-services.md)   
 [Superponer permisos de usuario y de grupo &#40;Master Data Services&#41;](../../2014/master-data-services/overlapping-user-and-group-permissions-master-data-services.md)  
  
  
