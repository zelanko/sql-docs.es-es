---
title: Agregar atributos a un grupo de seguimiento de cambios (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- change tracking groups [Master Data Services]
- attributes [Master Data Services], change tracking groups
- change tracking groups [Master Data Services], adding attributes
ms.assetid: e153eb5f-70ca-4c6f-89d8-1f937ed3917d
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 8e700942f9cebc08241cf4e159dceedc7d515a94
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65480125"
---
# <a name="add-attributes-to-a-change-tracking-group-master-data-services"></a>Agregar atributos a un grupo de seguimiento de cambios (Master Data Services)
  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], agregue los atributos a un grupo de seguimiento de cambios cuando desee realizar el seguimiento de los cambios de los valores de atributos.  
  
> [!NOTE]  
>  Después de agregar un atributo a un grupo de seguimiento de cambios, cuando los valores del atributo cambian, el atributo se marca como que ha cambiado en la base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . Cree una regla de negocios para realizar una acción según el cambio.  
  
## <a name="prerequisites"></a>Requisitos previos  
 Para realizar este procedimiento:  
  
-   Debe disponer de permiso para tener acceso al área funcional de **Administración del sistema** .  
  
-   Debe ser administrador de modelo. Para obtener más información, vea [Administradores &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
-   Los atributos deben existir para agregarlos al grupo de seguimiento de cambios. Para obtener más información, vea [Create a Text Attribute &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-text-attribute-master-data-services.md).  
  
### <a name="to-add-attributes-to-a-change-tracking-group"></a>Agregar atributos a un grupo de seguimiento de cambios  
  
1.  En [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], haga clic en **Administración del sistema**.  
  
2.  En el **el Explorador de modelos** página, en la barra de menús, seleccione **administrar** y haga clic en **entidades**.  
  
3.  En la página **Mantenimiento de entidades** , en la lista **Modelo** , seleccione un modelo.  
  
4.  Seleccione la fila correspondiente a la entidad para la que desea realizar el seguimiento de los valores de atributos.  
  
5.  Haga clic en **Editar entidad seleccionada**.  
  
6.  En la página **Editar entidad** :  
  
    -   Si el atributo es para miembros hoja, en el **atributos hoja** panel, seleccione el atributo y haga clic en **Editar atributo de hoja**.  
  
    -   Si el atributo es para miembros consolidados, en el **atributos consolidados** panel, seleccione el atributo y haga clic en **Editar atributo consolidado**.  
  
    -   Si el atributo es para colecciones, en el **atributos de colección** panel, seleccione el atributo y haga clic en **Editar atributo de colección**.  
  
7.  Active la casilla **Habilitar seguimiento de cambios** .  
  
8.  En el cuadro **Grupo de seguimiento de cambios** , escriba un número para el grupo.  
  
9. Haga clic en **Guardar atributo**.  
  
10. En la página **Mantenimiento de entidades** , haga clic en **Guardar entidad**.  
  
11. Repita este procedimiento para todos los atributos que desea incluir en el grupo. Utilice el mismo número de grupo de seguimiento de cambios para cada atributo del grupo.  
  
## <a name="next-steps"></a>Pasos siguientes  
  
-   [Iniciar acciones según los cambios de valores de atributos &#40;Master Data Services&#41;](../../2014/master-data-services/initiate-actions-based-on-attribute-value-changes-master-data-services.md)  
  
## <a name="see-also"></a>Vea también  
 [Crear un atributo de texto &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-text-attribute-master-data-services.md)   
 [Crear un atributo basado en dominio &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-domain-based-attribute-master-data-services.md)  
  
  
