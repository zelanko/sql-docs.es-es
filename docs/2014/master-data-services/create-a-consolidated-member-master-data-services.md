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
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 588295d0705ec9c556c85eb5bef1d96d8128b580
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "78176074"
---
# <a name="create-a-consolidated-member-master-data-services"></a>Crear un miembro consolidado (Master Data Services)
  En [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], cree un miembro consolidado si desea un nodo primario para una jerarquía explícita. Los miembros consolidados pueden tener sus propios atributos. Se utilizan para la agrupación. Tal y como se muestra en el ejemplo siguiente, los miembros consolidados pueden usarse para grupos de cuentas que tienen cuentas en ellos.

 ![Miembros consolidados de MDS](../../2014/master-data-services/media/mds-consolidated-members.png "Miembros consolidados de MDS")

## <a name="prerequisites"></a>Prerrequisitos
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

9. Haga clic en **OK**.

## <a name="next-steps"></a>Pasos a seguir

-   [Movimiento de miembros dentro de una jerarquía &#40;Master Data Services&#41;](move-members-within-a-hierarchy-master-data-services.md)

## <a name="see-also"></a>Consulte también
 [Cree una jerarquía explícita &#40;Master Data Services&#41;](../../2014/master-data-services/create-an-explicit-hierarchy-master-data-services.md) [crear un miembro hoja &#40;Master Data Services](../../2014/master-data-services/create-a-leaf-member-master-data-services.md)&#41;[cargar o actualizar miembros en Master Data Services mediante el uso de los miembros del proceso de almacenamiento provisional](add-update-and-delete-data-master-data-services.md) [Members &#40;Master Data Services&#41;](../../2014/master-data-services/members-master-data-services.md) &#40;Master Data Services&#41;las [jerarquías explícitas](../../2014/master-data-services/explicit-hierarchies-master-data-services.md) &#40;Master Data Services&#41;


