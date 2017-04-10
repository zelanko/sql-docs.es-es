---
title: "Bloquear una versi&#243;n (Master Data Services) | Microsoft Docs"
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
  - "versiones [Master Data Services], bloquear"
  - "bloquear versiones [Master Data Services]"
ms.assetid: 7bb62a84-12d8-4b29-9b6e-6aa25410618e
caps.latest.revision: 7
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 7
---
# Bloquear una versi&#243;n (Master Data Services)
  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], bloquee una versión de un modelo para impedir cambios en los miembros del modelo y en sus atributos.  
  
> [!NOTE]  
>  Aunque se bloquee una versión, los superusuarios y administradores del modelo pueden continuar agregando, modificando y quitando miembros. Otros usuarios con permiso en el modelo solo pueden ver los miembros.  
  
## Requisitos previos  
 Para realizar este procedimiento:  
  
-   Debe ser administrador de modelo. Para obtener más información, vea [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
-   El estado de la versión debe ser **Abierta**.  
  
-   Debe disponer del permiso para tener acceso al área funcional de Administración de versiones. Para obtener más información, consulte [Permisos del área funcional &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md).  
  
### Para bloquear una versión  
  
1.  En [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], haga clic en **Administración de versiones**.  
  
2.  En la página **Administrar versiones** , seleccione la fila de la versión que desea bloquear.  
  
3.  Haga clic en **Bloquear**.  
  
4.  En el cuadro de diálogo de confirmación, haga clic en **Aceptar**.  
  
## Pasos siguientes  
  
-   [Validar una versión con las reglas de negocios &#40;Master Data Services&#41;](../master-data-services/validate-a-version-against-business-rules-master-data-services.md)  
  
-   [Confirmar una versión &#40;Master Data Services&#41;](../master-data-services/commit-a-version-master-data-services.md)  
  
## Vea también  
 [Versiones &#40;Master Data Services&#41;](../master-data-services/versions-master-data-services.md)   
 [Desbloquear una versión &#40;Master Data Services&#41;](../master-data-services/unlock-a-version-master-data-services.md)  
  
  