---
title: Cambiar el nombre y el tipo de datos de un atributo
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- attributes [Master Data Services], changing name
ms.assetid: d348f238-f59d-41c7-ad20-3ccd55bfd9e5
author: lrtoyou1223
ms.author: lle
manager: erikre
ms.openlocfilehash: cb7d82f63f41baa88523f97e45a65635e1d49486
ms.sourcegitcommit: 6be9a0ff0717f412ece7f8ede07ef01f66ea2061
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85813469"
---
# <a name="change-an-attribute-name-and-data-type-master-data-services"></a>Cambiar el nombre y el tipo de datos de un atributo (Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], puede cambiar el nombre de un atributo.  
  
## <a name="prerequisites"></a>Requisitos previos  
 Para realizar este procedimiento:  
  
-   Debe disponer de permiso para tener acceso al área funcional de **Administración del sistema** .  
  
-   Debe ser administrador de modelo. Para obtener más información, vea [administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
### <a name="to-change-an-attribute-name-and-type"></a>Cambio del nombre y del tipo de un atributo  
  
1.  En [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], haga clic en **Administración del sistema**.  
  
2.  En la página **administrar modelo** , seleccione un modelo de la cuadrícula y, a continuación, haga clic en **entidades**.  
  
3.  En la página **Manage Entity** (Administrar entidad), seleccione la fila de la entidad para la que desea crear un atributo.  
  
4.  Haga clic en **Atributos**.  
  
5.  En la página **Administrar atributos** , realice una de las siguientes acciones.  
  
    -   Si el atributo es para miembros hoja, seleccione **Hoja** en el cuadro de lista **Member Types** (Tipos de miembro).  
  
    -   Si el atributo es para miembros consolidados, seleccione **Consolidado** en el cuadro de lista **Member Types** (Tipos de miembro).  
  
    -   Si el atributo es para colecciones, seleccione **Colección** en el cuadro de lista **Member Types** (Tipos de miembro).  
  
6.  Seleccione la fila del atributo que desea editar y después haga clic en **Editar**.  
  
7.  En el cuadro **Nombre** , escriba el nombre actualizado del atributo. Para obtener una lista de palabras que no se deben usar como nombres de atributo, consulte [palabras reservadas &#40;Master Data Services&#41;](../master-data-services/reserved-words-master-data-services.md).  
  
8.  En la lista **Tipo de atributo** , seleccione otro tipo.  
  
9. Haga clic en **Save**(Guardar).  
  
## <a name="see-also"></a>Consulte también  
 [Cree un atributo de texto &#40;Master Data Services&#41;](../master-data-services/create-a-text-attribute-master-data-services.md)   
 [Eliminar un atributo &#40;Master Data Services&#41;](../master-data-services/delete-an-attribute-master-data-services.md)   
 [Atributos &#40;Master Data Services&#41;](../master-data-services/attributes-master-data-services.md)  
  
  
