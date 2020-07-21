---
title: Crear una vista de suscripciones (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- subscription views [Master Data Services], creating
- creating subscription views [Master Data Services]
ms.assetid: a5e28961-af16-414a-9845-d2e06aac5214
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: de6ee4b3ba52dec87d71bb97707a8cd8f748d854
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84971775"
---
# <a name="create-a-subscription-view-master-data-services"></a>Crear una vista de suscripciones (Master Data Services)
  Cree una vista de suscripciones cuando desee crear una vista de los datos en la [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] base de datos para su uso en sistemas de suscripción.  
  
## <a name="prerequisites"></a>Requisitos previos  
 Para realizar este procedimiento:  
  
-   Debe disponer del permiso para tener acceso al área funcional de **Administración de integraciones** .  
  
-   Debe ser administrador de modelo. Para obtener más información, vea [administradores &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
### <a name="to-create-a-subscription-view"></a>Crear una vista de suscripción  
  
1.  En [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], haga clic en **Administración de integraciones**.  
  
2.  En la barra de menús, haga clic en **Crear vistas**.  
  
3.  En la página **vistas de suscripciones** , haga clic en **Agregar vista de suscripciones**.  
  
4.  En el panel **crear vista de suscripciones** , en el cuadro **nombre de vista de suscripciones** , escriba un nombre para la vista.  
  
5.  En la lista **Modelo** , seleccione un modelo.  
  
6.  Seleccione la opción **versión** o **marca de versión** y, a continuación, seleccione en la lista correspondiente.  
  
    > [!TIP]  
    >  Cree una vista de suscripción basada en una marca de versión. Al bloquear una versión, puede reasignar la marca a una versión abierta sin actualizar la vista de suscripción.  
  
7.  Seleccione la opción **entidad** o **jerarquía derivada** y, a continuación, seleccione en la lista correspondiente.  
  
8.  En la lista **Formato** , seleccione un formato de vista de suscripción.  
  
9. Si elige **Niveles explícitos** o **Niveles derivados** en la lista **Formato** , escriba el número de niveles en la jerarquía que se incluirán en la vista.  
  
10. Haga clic en **Save**(Guardar).  
  
## <a name="see-also"></a>Consulte también  
 [Exportar datos &#40;Master Data Services&#41;](overview-exporting-data-master-data-services.md)   
 [Eliminar una vista de suscripciones &#40;Master Data Services&#41;](delete-a-subscription-view-master-data-services.md)   
 [Crear una marca de versión &#40;Master Data Services&#41;](create-a-version-flag-master-data-services.md)  
  
  
