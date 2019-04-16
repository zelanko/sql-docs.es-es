---
title: Crear un miembro consolidado (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- creating consolidated members [Master Data Services]
- members [Master Data Services], creating consolidated members
- consolidated members [Master Data Services], creating
ms.assetid: 431ab2d2-5517-4372-9980-142b05427c08
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: cf154f3437ed22be932fa37470f59049aea09850
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/15/2019
ms.locfileid: "59582588"
---
# <a name="create-a-consolidated-member-master-data-services"></a>Crear un miembro consolidado (Master Data Services)
  En [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], cree un miembro consolidado si desea un nodo primario para una jerarquía explícita. Los miembros consolidados pueden tener sus propios atributos. Se utilizan para la agrupación. Tal y como se muestra en el ejemplo siguiente, los miembros consolidados pueden usarse para grupos de cuentas que tienen cuentas en ellos.  
  
 ![Miembros consolidados de MDS](../../2014/master-data-services/media/mds-consolidated-members.png "MDS miembros consolidados")  
  
## <a name="prerequisites"></a>Requisitos previos  
 Para realizar este procedimiento:  
  
-   Debe disponer de permiso de acceso al área funcional **Explorador** .  
  
-   Como mínimo, debe tener el permiso **Actualizar** para el objeto de modelo consolidado en la entidad a la que vaya a agregar un miembro.  
  
### <a name="to-create-a-consolidated-member"></a>Crear un miembro consolidado  
  
1.  En la página principal de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , en la lista **Modelo** , seleccione un modelo.  
  
2.  En la lista **Versión** , seleccione una versión.  
  
3.  Haga clic en **Explorador**.  
  
4.  En la barra de menús, seleccione **Jerarquías** y haga clic en el nombre de la jerarquía a la que desee agregar un miembro consolidado.  
  
5.  Encima de la cuadrícula, seleccione **Miembros consolidados** o **Todos los miembros consolidados de esta jerarquía** .  
  
6.  Haga clic en **Agregar**.  
  
7.  En el panel de la derecha, cumplimente los campos.  
  
8.  Opcional. En el cuadro **Anotaciones** , escriba un comentario sobre los motivos por los que se agregó el miembro. Todos los usuarios que tienen acceso al miembro pueden ver la anotación.  
  
9. Haga clic en **Aceptar**.  
  
## <a name="next-steps"></a>Pasos siguientes  
  
-   [Mover miembros dentro de una jerarquía &#40;Master Data Services&#41;](move-members-within-a-hierarchy-master-data-services.md)  
  
## <a name="see-also"></a>Vea también  
 [Crear una jerarquía explícita &#40;Master Data Services&#41;](../../2014/master-data-services/create-an-explicit-hierarchy-master-data-services.md)   
 [Crear un miembro hoja &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-leaf-member-master-data-services.md)   
 [Cargar o actualizar miembros en Master Data Services mediante el proceso de almacenamiento provisional](add-update-and-delete-data-master-data-services.md)   
 [Miembros &#40;Master Data Services&#41;](../../2014/master-data-services/members-master-data-services.md)   
 [Jerarquías explícitas &#40;Master Data Services&#41;](../../2014/master-data-services/explicit-hierarchies-master-data-services.md)  
  
  
