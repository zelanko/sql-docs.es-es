---
title: "Purga de miembros de versi&#243;n (Master Data Services) | Microsoft Docs"
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
ms.assetid: adecce2d-46bb-49ff-8be9-0b31b8dd3cb6
caps.latest.revision: 7
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 7
---
# Purga de miembros de versi&#243;n (Master Data Services)
  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], la eliminación de un miembro solo lo desactiva, es decir, lo elimina de forma temporal. Los datos aún residen en la base de datos. En este tema se describe cómo purgar (eliminar de forma permanente) todos los miembros eliminados temporalmente en una versión de modelo.  
  
## Requisitos previos  
 Para realizar este procedimiento.  
  
-   Debe disponer del permiso para tener acceso al área funcional de Administración de versiones.  
  
-   Debe ser administrador de modelo. Para obtener más información, vea [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
## Para purgar los miembros eliminados temporalmente  
  
1.  En [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], haga clic en **Administración de versiones**.  
  
2.  En la página **Administrar versiones** , seleccione el modelo cuya versión desea purgar. Se muestra la lista de versiones del modelo.  
  
3.  Seleccione la fila para la versión que desea purgar.  
  
4.  Haga clic en **Purge Members**(Purgar miembros).  
  
5.  En el mensaje de confirmación, haga clic en "Aceptar".  
  
## Métodos adicionales para purgar los miembros  
 Al purgar los miembros de la versión, se eliminarán de manera permanente los miembros eliminados temporalmente de todas las entidades que pertenecen a la versión seleccionada. Una alternativa bastante más precisa consiste en usar el almacenamiento provisional de base de entidades para eliminar permanentemente algunos miembros concretos de una entidad. Además, los administradores de la entidad con permiso funcional de explorador pueden purgar una versión de la entidad en la página del explorador de la entidad.  
  
 Para obtener más información, consulte [Tabla de almacenamiento provisional de miembros hoja &#40;Master Data Services&#41;](../master-data-services/leaf-member-staging-table-master-data-services.md)  
  
  