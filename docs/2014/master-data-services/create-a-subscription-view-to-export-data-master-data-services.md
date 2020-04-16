---
title: Crear una vista de suscripción (Master Data Services) Microsoft Docs
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
manager: craigg
ms.openlocfilehash: c4a2f747192b1cddefeac256d4470a2b345305de
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/15/2020
ms.locfileid: "65479949"
---
# <a name="create-a-subscription-view-master-data-services"></a>Crear una vista de suscripciones (Master Data Services)
  Cree una vista de suscripción cuando desee [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] crear una vista de los datos en la base de datos para que la usen los sistemas de suscripción.  
  
## <a name="prerequisites"></a>Prerrequisitos  
 Para realizar este procedimiento:  
  
-   Debe disponer del permiso para tener acceso al área funcional de **Administración de integraciones** .  
  
-   Debe ser administrador de modelo. Para obtener más información, consulte [Administradores &#40;&#41;de Master Data ServicesMaster Data Services ](administrators-master-data-services.md).  
  
### <a name="to-create-a-subscription-view"></a>Crear una vista de suscripción  
  
1.  En [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], haga clic en **Administración de integraciones**.  
  
2.  En la barra de menús, haga clic en **Crear vistas**.  
  
3.  En la página Vistas de **suscripción,** haga clic en Agregar vista de **suscripción**.  
  
4.  En el panel Crear vista de **suscripción,** en el cuadro Nombre de vista de **suscripción,** escriba un nombre para la vista.  
  
5.  En la lista **Modelo** , seleccione un modelo.  
  
6.  Seleccione la opción **Versión** o Indicador de **versión** y, a continuación, seleccione en la lista correspondiente.  
  
    > [!TIP]  
    >  Cree una vista de suscripción basada en una marca de versión. Al bloquear una versión, puede reasignar la marca a una versión abierta sin actualizar la vista de suscripción.  
  
7.  Seleccione la opción **Entidad** o **Jerarquía derivada** y, a continuación, seleccione en la lista correspondiente.  
  
8.  En la lista **Formato** , seleccione un formato de vista de suscripción.  
  
9. Si elige **Niveles explícitos** o **Niveles derivados** en la lista **Formato** , escriba el número de niveles en la jerarquía que se incluirán en la vista.  
  
10. Haga clic en **Save**(Guardar).  
  
## <a name="see-also"></a>Consulte también  
 [Exportación de datos &#40;servicios de datos maestrosMaster Data Services&#41;](overview-exporting-data-master-data-services.md)   
 [Eliminar una vista de suscripción &#40;&#41;](delete-a-subscription-view-master-data-services.md)   
 [Crear una marca de versión &#40;Master Data Services&#41;](create-a-version-flag-master-data-services.md)  
  
  
