---
title: Hacer que un grupo de atributos sea visible para los usuarios (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: b2f6cc27-dbc9-4f3f-961e-e81e76375248
caps.latest.revision: 3
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 70dcc1e8f35f288b4693bd87308d7f2abcff0136
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36196257"
---
# <a name="make-an-attribute-group-visible-to-users-master-data-services"></a>Hacer que un grupo de atributos sea visible para los usuarios (Master Data Services)
  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], haga que un grupo de atributos sea visible para los usuarios o los grupos cuando desee que los usuarios tengan pestañas en la cuadrícula del área funcional de **Explorador** .  
  
 Cuando se crea un grupo de atributos, se oculta automáticamente para todos los usuarios excepto para la persona que lo creó.  
  
## <a name="prerequisites"></a>Requisitos previos  
 Para realizar este procedimiento:  
  
-   Debe disponer de permiso para tener acceso al área funcional de **Administración del sistema** .  
  
-   Debe ser administrador de modelo. Para obtener más información, vea [Administrators &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
-   Por lo menos debe existir un grupo de atributos. Para obtener más información, vea [Create an Attribute Group &#40;Master Data Services&#41;](../../2014/master-data-services/create-an-attribute-group-master-data-services.md).  
  
### <a name="to-make-an-attribute-group-visible-to-users"></a>Para hacer que un grupo de atributos sea visible para los usuarios  
  
1.  En [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], haga clic en **Administración del sistema**.  
  
2.  En el **vista de modelo** página, en la barra de menús, seleccione **administrar** y haga clic en **grupos de atributos**.  
  
3.  En la lista **Modelo** , seleccione un modelo.  
  
4.  En la lista **Entidad** , seleccione una entidad.  
  
5.  Haga clic en el signo más para expandir **grupos hoja**, **grupos consolidados**, o **grupos de colecciones**, según el tipo de grupo que desea hacer visible.  
  
6.  Haga clic en el signo más para expandir el grupo que desea hacer visible.  
  
7.  Haga clic en **usuarios** o **grupos**, dependiendo de si está realizando el grupo es visible para un usuario o un grupo.  
  
8.  Haga clic en **Editar elemento seleccionado**.  
  
9. Haga clic en usuarios o grupos en el **disponible** y haga clic en el **agregar** flecha. Para agregarlos todos, haga clic en la flecha **Agregar todo** .  
  
10. Haga clic en **Guardar**.  
  
## <a name="see-also"></a>Vea también  
 [Grupos de atributos &#40;Master Data Services&#41;](../../2014/master-data-services/attribute-groups-master-data-services.md)   
 [Crear un grupo de atributos &#40;Master Data Services&#41;](../../2014/master-data-services/create-an-attribute-group-master-data-services.md)  
  
  