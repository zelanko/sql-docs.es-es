---
title: Crear una jerarquía explícita (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- master-data-services
ms.topic: conceptual
helpviewer_keywords:
- creating explicit hierarchies [Master Data Services]
- explicit hierarchies, creating
ms.assetid: ba768393-6990-4eda-8cb0-d58cb3cfc2e2
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 71c695a31aacf146bf2e97dd0ad4a38044d6b8b5
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48083585"
---
# <a name="create-an-explicit-hierarchy-master-data-services"></a>Crear una jerarquía explícita (Master Data Services)
  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], cree una jerarquía explícita cuando necesite una jerarquía desigual en la que los miembros puedan existir en cualquier nivel. Las jerarquías explícitas contienen los miembros de una sola entidad.  
  
 Después de crear una jerarquía explícita, puede agregarle miembros en el área funcional de **Explorador** .  
  
## <a name="prerequisites"></a>Requisitos previos  
 Para realizar este procedimiento:  
  
-   Debe disponer de permiso para tener acceso al área funcional de **Administración del sistema** .  
  
-   Debe ser administrador de modelo. Para obtener más información, vea [Administrators &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
-   La entidad debe habilitarse para las jerarquías explícitas y las colecciones. Para obtener más información, consulte [habilitar una entidad para jerarquías explícitas y colecciones &#40;Master Data Services&#41;](../../2014/master-data-services/enable-an-entity-for-explicit-hierarchies-and-collections-master-data-services.md).  
  
### <a name="to-create-an-explicit-hierarchy"></a>Crear una jerarquía explícita  
  
1.  En [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], haga clic en **Administración del sistema**.  
  
2.  En la página **Vista de modelo** , en la barra de menús, seleccione **Administrar** y haga clic en **Entidades**.  
  
3.  En la página **Mantenimiento de entidades** , en la lista **Modelo** , seleccione un modelo.  
  
4.  Seleccione la fila correspondiente a la entidad para la que desea crear una jerarquía explícita.  
  
5.  Haga clic en **Editar entidad seleccionada**.  
  
6.  En el **editar entidad** página, en el **jerarquías explícitas** panel, haga clic en **agregar jerarquía explícita**.  
  
7.  En el **agregar jerarquía explícita** página, en el **nombre de jerarquía explícita** cuadro, escriba un nombre para la jerarquía.  
  
8.  Opcionalmente, desactive la casilla **Mandatory hierarchy** (Jerarquía obligatoria) para crear la jerarquía como no obligatoria. Para obtener más información sobre los tipos de jerarquías, consulte [Explicit Hierarchies &#40;Master Data Services&#41;](../../2014/master-data-services/explicit-hierarchies-master-data-services.md).  
  
9. Haga clic en **guardar jerarquía**.  
  
10. En el **editar entidad** página, haga clic en **guardar entidad**.  
  
## <a name="next-steps"></a>Pasos siguientes  
  
-   [Crear un miembro consolidado &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-consolidated-member-master-data-services.md)  
  
-   [Mover miembros dentro de una jerarquía &#40;Master Data Services&#41;](../../2014/master-data-services/move-members-within-a-hierarchy-master-data-services.md)  
  
## <a name="see-also"></a>Vea también  
 [Jerarquías explícitas &#40;Master Data Services&#41;](../../2014/master-data-services/explicit-hierarchies-master-data-services.md)   
 [Jerarquías derivadas con límites explícitos &#40;Master Data Services&#41;](../../2014/master-data-services/derived-hierarchies-with-explicit-caps-master-data-services.md)   
 [Cambiar el nombre de una jerarquía explícita &#40;Master Data Services&#41;](../../2014/master-data-services/change-an-explicit-hierarchy-name-master-data-services.md)  
  
  
