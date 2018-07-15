---
title: Crear un atributo basado en dominio (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- domain-based attributes [Master Data Services], creating
- creating domain-based attributes [Master Data Services]
- attributes [Master Data Services], creating domain-based attributes
ms.assetid: 11c31c9f-e6cc-47b7-b76a-d691f84c93c6
caps.latest.revision: 5
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: fd6e0a992dd4f23b6da24ed70cb884025c969537
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37320455"
---
# <a name="create-a-domain-based-attribute-master-data-services"></a>Crear un atributo basado en dominio (Master Data Services)
  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], cree un atributo basado en dominios para rellenar los valores de un atributo con los miembros de una entidad.  
  
## <a name="prerequisites"></a>Requisitos previos  
 Para realizar este procedimiento:  
  
-   Debe disponer de permiso para tener acceso al área funcional de **Administración del sistema** .  
  
-   Debe ser administrador de modelo. Para obtener más información, vea [Administrators &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
-   Debe existir una entidad para utilizarse como origen de los valores de atributo. Por ejemplo, para crear un atributo basado en dominio en la entidad Color, primero debe crear esta. Para obtener más información, consulte [Crear una entidad &#40;Master Data Services&#41;](../../2014/master-data-services/create-an-entity-master-data-services.md).  
  
-   Debe existir una entidad para la que crear el atributo. Para obtener más información, consulte [Crear una entidad &#40;Master Data Services&#41;](../../2014/master-data-services/create-an-entity-master-data-services.md).  
  
### <a name="to-create-a-domain-based-attribute"></a>Crear un atributo basado en dominio  
  
1.  En [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], haga clic en **Administración del sistema**.  
  
2.  En la página **Vista de modelo** , en la barra de menús, seleccione **Administrar** y haga clic en **Entidades**.  
  
3.  En la página **Mantenimiento de entidades** , en la lista **Modelo** , seleccione un modelo.  
  
4.  Seleccione la fila para la entidad para la que desea crear un atributo.  
  
5.  Haga clic en **Editar entidad seleccionada**.  
  
6.  En la página **Editar entidad** :  
  
    -   Si el atributo es para miembros hoja, en el panel **Atributos de miembro hoja** , haga clic en **Agregar atributo hoja**.  
  
    -   Si el atributo es para miembros consolidados, en el panel **Atributos de miembro consolidados** , haga clic en **Agregar atributo consolidado**.  
  
    -   Si el atributo es para colecciones, en el panel **Atributos de colección** , haga clic en **Agregar atributo de colección**.  
  
7.  En el **Agregar atributo** página, seleccione el **basado en dominio** opción.  
  
8.  En el cuadro **Nombre** , escriba un nombre para el atributo. No tiene que ser el mismo nombre que la entidad que utiliza para el origen de los valores de atributo.  
  
9. En el cuadro **Ancho de píxel de la pantalla** , escriba el ancho de la columna de atributo que se va a mostrar en la cuadrícula del **Explorador** .  
  
10. Desde el **entidad** lista, elija la entidad que se usará para rellenar los valores de atributo.  
  
11. Opcional. Seleccione **Enable change tracking** para realizar el seguimiento de los cambios en los grupos de atributos. Para obtener más información, consulte [Agregar atributos a un grupo de seguimiento de cambios &#40;Master Data Services&#41;](../../2014/master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md).  
  
12. Haga clic en **Guardar atributo**.  
  
13. En la página **Mantenimiento de entidades** , haga clic en **Guardar entidad**.  
  
## <a name="see-also"></a>Vea también  
 [Atributos basados en dominio &#40;Master Data Services&#41;](../../2014/master-data-services/domain-based-attributes-master-data-services.md)   
 [Crear una jerarquía derivada &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-derived-hierarchy-master-data-services.md)   
 [Cambiar un nombre de atributo &#40;Master Data Services&#41;](change-an-attribute-name-and-data-type-master-data-services.md)   
 [Eliminar un atributo &#40;Master Data Services&#41;](../../2014/master-data-services/delete-an-attribute-master-data-services.md)  
  
  
