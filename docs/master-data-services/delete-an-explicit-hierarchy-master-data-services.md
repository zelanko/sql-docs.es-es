---
title: "Eliminar una jerarqu&#237;a expl&#237;cita (Master Data Services) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "jerarquías explícitas, eliminar"
  - "eliminar jerarquías explícitas [Master Data Services]"
ms.assetid: 4ce177b0-9884-47a2-9cea-212e845dd762
caps.latest.revision: 6
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 6
---
# Eliminar una jerarqu&#237;a expl&#237;cita (Master Data Services)
  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], elimine una jerarquía explícita cuando ya no la necesite.  
  
> [!WARNING]  
>  Cuando elimine una jerarquía explícita, se eliminarán también todos los miembros consolidados de la jerarquía. Si elimina todas las jerarquías explícitas de una entidad, también se eliminarían todas las recopilaciones de la entidad y la entidad dejaría de estar habilitada para las jerarquías explícitas y las recopilaciones.  
  
## Requisitos previos  
 Para realizar este procedimiento:  
  
-   Debe disponer de permiso para tener acceso al área funcional de **Administración del sistema** .  
  
-   Debe ser administrador de modelo. Para obtener más información, vea [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
### Eliminar una jerarquía explícita  
  
1.  En [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], haga clic en **Administración del sistema**.  
  
2.  En la página **Manage Model** (Administrar modelo), seleccione un modelo de la cuadrícula y después haga clic en **Entidades**.  
  
3.  En la página **Manage Entity** (Administrar entidad), en la cuadrícula, seleccione la fila de la entidad que contiene la jerarquía explícita que quiere eliminar.  
  
4.  Haga clic en **Jerarquías explícitas**.  
  
5.  En la página **Manage Explicit Hierarchy** (Administrar jerarquía explícita), haga clic en la jerarquía explícita que desea eliminar.  
  
6.  Haga clic en **Editar**.  
  
7.  En el cuadro de diálogo de confirmación, haga clic en **Aceptar**.  
  
## Vea también  
 [Crear una jerarquía explícita &#40;Master Data Services&#41;](../master-data-services/create-an-explicit-hierarchy-master-data-services.md)   
 [Jerarquías explícitas &#40;Master Data Services&#41;](../master-data-services/explicit-hierarchies-master-data-services.md)  
  
  