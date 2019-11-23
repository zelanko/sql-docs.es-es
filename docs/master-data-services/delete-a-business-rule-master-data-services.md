---
title: Eliminar una regla de negocios
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- deleting business rules [Master Data Services]
- business rules [Master Data Services], deleting
ms.assetid: b97aa4f9-569f-451d-ad62-65b81f980299
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: d6af3aac4ac8e2a1a4026162eb6ab5f6038b5eed
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/07/2019
ms.locfileid: "73729408"
---
# <a name="delete-a-business-rule-master-data-services"></a>Eliminar una regla de negocios (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], elimine una regla de negocios cuando ya no se necesite.  
  
> [!NOTE]  
>  Puede evitar que los datos se validen con una regla de negocios excluyéndola, en lugar de eliminándola. Para obtener más información, consulte [Exclude a Business Rule &#40;Master Data Services&#41;](../master-data-services/exclude-a-business-rule-master-data-services.md).  
  
## <a name="prerequisites"></a>Prerequisites  
 Para realizar este procedimiento:  
  
-   Debe disponer de permiso para tener acceso al área funcional de **Administración del sistema** .  
  
-   Debe ser administrador de modelo. Para obtener más información, vea [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
### <a name="to-delete-a-business-rule"></a>Eliminar una regla de negocios  
  
1.  En [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], haga clic en **Administración del sistema**.  
  
2.  En la barra de menús, seleccione **Administrar** y haga clic en **Reglas de negocios**.  
  
3.  En la página **Reglas de negocios** , en la lista desplegable **Modelo** , seleccione un modelo.  
  
4.  En la lista desplegable **Entidad** , seleccione una entidad.  
  
5.  En la lista desplegable **Member Types** (Tipos de miembros), seleccione un tipo de miembro al que aplicar la regla de negocio.  
  
6.  En la cuadrícula, haga clic en la fila de la regla de negocios que desea eliminar.  
  
7.  Haga clic en **Eliminar**.  
  
8.  En el cuadro de diálogo de confirmación, haga clic en **Aceptar**. El valor de la columna **Business Rule State** (Estado de la regla de negocio) es **Eliminación pendiente**.  
  
9. Haga clic en **Publish All**(Publicar todo).  
  
10. En el cuadro de diálogo de confirmación, haga clic en **Aceptar**. La regla de negocios eliminada ya no aparece en la cuadrícula.  
  
## <a name="see-also"></a>Vea también  
 [Excluir una regla de negocios &#40;Master Data Services&#41;](../master-data-services/exclude-a-business-rule-master-data-services.md)   
 [Crear y publicar una regla de negocios &#40;Master Data Services&#41;](../master-data-services/create-and-publish-a-business-rule-master-data-services.md)   
 [Reglas de negocios &#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)  
  
  
