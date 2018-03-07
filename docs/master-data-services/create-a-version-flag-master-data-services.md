---
title: "Crear una marca de versión (Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: non-specific
ms.reviewer: 
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- creating version flags [Master Data Services]
- version flags [Master Data Services], creating
- versions [Master Data Services], creating flags
ms.assetid: 3067e1e3-05b7-4f11-9206-c612ef4e7e42
caps.latest.revision: 
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 65ed241cb8cf0b3918a8789a2dbe5907cec7d6e3
ms.sourcegitcommit: 6ac1956307d8255dc544e1063922493b30907b80
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/05/2018
---
# <a name="create-a-version-flag-master-data-services"></a>Crear una marca de versión (Master Data Services)
  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], cree una marca de versión para asignarla a una versión. La marca puede indicar la versión que los usuarios o los sistemas que se suscriben deben utilizar.  
  
## <a name="prerequisites"></a>Prerequisites  
 Para realizar este procedimiento:  
  
-   Debe disponer del permiso para tener acceso al área funcional de **Administración de versiones** .  
  
-   Debe ser administrador de modelo. Para obtener más información, vea [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
-   Debe disponer del permiso para tener acceso al área funcional de Administración de versiones. Para obtener más información, consulte [Permisos del área funcional &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md).  
  
### <a name="to-create-a-version-flag"></a>Crear una marca de versión  
  
1.  En [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], haga clic en **Administración de versiones**.  
  
2.  En la página **Administración de versiones** , en la barra de menús, seleccione **Administrar** y, a continuación, haga clic en **Marcas**.  
  
3.  En la página **Administrar marcas de versión** , en el campo **Modelo** , seleccione el modelo para el que desea crear una marca.  
  
4.  Haga clic en **Agregar**.  
  
5.  En el cuadro **Nombre** , escriba un nombre.  
  
6.  En el cuadro **Descripción** , escriba una descripción.  
  
7.  En el campo **Solo versiones confirmadas** , seleccione **Verdadero** para indicar que la marca solo puede asignarse a las versiones con el estado **Confirmado** . Seleccione **Falso** para indicar que la marca puede asignarse a versiones que tengan cualquier estado.  
  
8.  Haga clic en **Guardar**.  
  
## <a name="next-steps"></a>Next Steps  
  
-   [Asignar una marca a una versión &#40;Master Data Services&#41;](../master-data-services/assign-a-flag-to-a-version-master-data-services.md)  
  
## <a name="see-also"></a>Ver también  
 [Versiones &#40;Master Data Services&#41;](../master-data-services/versions-master-data-services.md)   
 [Cambiar el nombre de marca de una versión &#40;Master Data Services&#41;](../master-data-services/change-a-version-flag-name-master-data-services.md)  
  
  
