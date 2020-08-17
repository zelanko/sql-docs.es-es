---
description: Explorador de dependencias de entidad
title: Explorador de dependencias de entidad
ms.custom: ''
ms.date: 04/06/2016
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
keywords:
- master data services
ms.assetid: 9d922118-1412-4a9d-9c02-70d6c48d6c0d
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 8a0fcbcee1d17a98025a1c8adbc02c3409b1db06
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88389301"
---
# <a name="entity-dependencies-explorer"></a>Explorador de dependencias de entidad

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  
[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 2016 agrega una nueva página del explorador, Dependencias de entidades, que proporciona una forma alternativa de visualizar las relaciones entre miembros de la entidad dentro de un modelo, según lo especificado por sus valores de atributo basados en dominio (DBA), pero sin tener que definir primero una jerarquía derivada.   
  
Ayuda a responder a la pregunta "¿Quién consume mi entidad y cómo?". La vista es similar a la de la página del explorador de la jerarquía derivada, pero es más inclusiva. Muestra todas las relaciones de DBA, no solo las que se definen como parte de una jerarquía determinada. No se necesita una definición de jerarquía porque la estructura jerárquica mostrada se deduce simplemente de los DBA existentes.  
  
En el menú de página del explorador, el elemento de menú de las dependencias de la entidad enumera todas las entidades en el modelo que dependen de, al menos, una entidad (es decir, al menos una entidad tiene un DBA que hace referencia a la entidad de la lista). El número de dependencias (directas e indirectas) se muestra junto al nombre de la entidad y la lista está ordenada por este número con las entidades a las que se les hace más referencia en la parte superior. La siguiente captura de pantalla, tomada del modelo de cliente de los [datos de ejemplo](https://msdn.microsoft.com/library/master-data-services-sample.aspx), muestra que 7 entidades hacen referencia a la entidad BigArea (directa o indirectamente):  
  
![MDS_EntityDependencies_Menu.jpg](../master-data-services/media/mds-entitydependencies-menu-jpg.jpg)  
    
Al hacer clic en este elemento de menú se abre la nueva página de explorador de dependencias de la entidad para la entidad BigArea, que muestra cómo se consumen los miembros de la entidad. Muestra una vista jerárquica con los miembros de BigArea en la parte superior del árbol, con los miembros de las 7 entidades de consumo anidadas debajo:  
  
![MDS_EntityDependencies_Tree.jpg](../master-data-services/media/mds-entitydependencies-tree-jpg.jpg)  
    
Más de una entidad puede consumir directamente a una entidad. En el ejemplo anterior, las entidades SubRegion y RegionClimate consumen (tienen referencias DBA a) la entidad Region. Los miembros de cada entidad de consumo se agrupan bajo un nodo primario que lleva el nombre de la entidad:   
  
![MDS_EntityDependencies_Entity_Node.jpg](../master-data-services/media/mds-entitydependencies-entity-node-jpg.jpg)  
  
Estos nodos de árbol contenedores tienen un icono de cuadrícula a la izquierda del nombre de entidad y el texto está coloreado según la profundidad de nivel de la jerarquía. En el ejemplo anterior se muestra que SubRegion "CDSR {Canada}" tiene una referencia DBA a Region "CDR {Canada}", que hace referencia a Area "CDA {Canada}", que hace referencia a BigArea "NAm {N. America}".  
  
La vista se puede modificar por completo, al igual que en la página del explorador de la jerarquía. Se pueden modificar las relaciones primarias y secundarias en el árbol al cortar y pegar o arrastrar y soltar miembros secundarios de un elemento primario a otro. Se pueden modificar otros valores de atributo de miembro en el panel de detalles a la derecha del árbol.   
  
  
  
  

