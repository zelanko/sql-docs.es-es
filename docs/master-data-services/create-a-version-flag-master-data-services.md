---
title: "Crear una marca de versión (Master Data Services) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- creating version flags [Master Data Services]
- version flags [Master Data Services], creating
- versions [Master Data Services], creating flags
ms.assetid: 3067e1e3-05b7-4f11-9206-c612ef4e7e42
caps.latest.revision: 7
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: be3585a40a7ce8312e4e31b13118f6b128e2be13
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="create-a-version-flag-master-data-services"></a>Crear una marca de versión (Master Data Services)
  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], cree una marca de versión para asignarla a una versión. La marca puede indicar la versión que los usuarios o los sistemas que se suscriben deben utilizar.  
  
## <a name="prerequisites"></a>Requisitos previos  
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
  
## <a name="next-steps"></a>Pasos siguientes  
  
-   [Asignar una marca a una versión &#40; Master Data Services &#41;](../master-data-services/assign-a-flag-to-a-version-master-data-services.md)  
  
## <a name="see-also"></a>Vea también  
 [Versiones de &#40; Master Data Services &#41;](../master-data-services/versions-master-data-services.md)   
 [Cambiar el nombre de una marca de versión &#40; Master Data Services &#41;](../master-data-services/change-a-version-flag-name-master-data-services.md)  
  
  
