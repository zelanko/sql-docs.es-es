---
title: "Asignar una marca a una versi&#243;n (Master Data Services) | Microsoft Docs"
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
  - "marcas de versiones [Master Data Services], asignar marcas"
  - "versiones [Master Data Services], asignar marcas"
ms.assetid: 6629ec7e-32e7-4a1e-8b31-eb43c5923766
caps.latest.revision: 7
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 7
---
# Asignar una marca a una versi&#243;n (Master Data Services)
  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], asigne una marca a una versión para indicar la versión que los usuarios o los sistemas que se suscriben deberían utilizar.  
  
> [!NOTE]  
>  Solo se pueden asignar marcas de versión a una versión al mismo tiempo. Si asigna una marca que ya está asignada a otra versión, se mueve a la versión que seleccionó.  
  
## Requisitos previos  
 Para realizar este procedimiento:  
  
-   Debe disponer del permiso para tener acceso al área funcional de **Administración de versiones** .  
  
-   Debe ser administrador de modelo. Para obtener más información, vea [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
-   Debe haber creado una marca de versión para asignarla. Para obtener más información, consulte [Crear una marca de versión &#40;Master Data Services&#41;](../master-data-services/create-a-version-flag-master-data-services.md).  
  
-   Debe disponer del permiso para tener acceso al área funcional de Administración de versiones. Para obtener más información, consulte [Permisos del área funcional &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md).  
  
### Asignar una marca a una versión  
  
1.  En [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], haga clic en **Administración de versiones**.  
  
2.  En la página **Administrar versiones**, en la fila de la versión a la que quiere asignar una marca, haga doble clic en la celda de la columna **Marca**.  
  
3.  En la lista, seleccione la marca que desea asignar.  
  
    > [!NOTE]  
    >  Si la marca que desea no está disponible, puede que solo esté disponible para versiones **Confirmado** . Para confirmar, ir a la página **Administrar marcas de versión** y ver el campo **Solo versiones confirmadas** para la marca.  
  
4.  Presione ENTRAR para guardar el cambio.  
  
## Vea también  
 [Crear una marca de versión &#40;Master Data Services&#41;](../master-data-services/create-a-version-flag-master-data-services.md)   
 [Versiones &#40;Master Data Services&#41;](../master-data-services/versions-master-data-services.md)  
  
  