---
title: Crear una entidad (Master Data Services) | Microsoft Docs
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
- entities [Master Data Services], creating
- creating entities [Master Data Services]
ms.assetid: d9a6a51e-7b53-4785-a118-3baeb7ca2d48
caps.latest.revision: 6
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 9e5c53e76330c00dde7b6d14fb0c6592546582bc
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37329845"
---
# <a name="create-an-entity-master-data-services"></a>Crear una entidad (Master Data Services)
  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], cree una entidad para contener los miembros y sus atributos.  
  
## <a name="prerequisites"></a>Requisitos previos  
 Para realizar este procedimiento:  
  
-   Debe disponer de permiso para tener acceso al área funcional de **Administración del sistema** .  
  
-   Debe ser administrador de modelo. Para obtener más información, vea [Administrators &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
-   Debe existir un modelo. Para obtener más información, consulte [Crear un modelo &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-model-master-data-services.md).  
  
### <a name="to-create-an-entity"></a>Crear una entidad  
  
1.  En [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], haga clic en **Administración del sistema**.  
  
2.  En la página **Vista de modelo** , en la barra de menús, seleccione **Administrar** y haga clic en **Entidades**.  
  
3.  En la página **Mantenimiento de entidades** , en la lista **Modelo** , seleccione un modelo.  
  
4.  Haga clic en **Agregar entidad**.  
  
5.  En el **nombre de entidad** , escriba el nombre de la entidad.  
  
6.  En el **nombre de las tablas de ensayo** , escriba un nombre para la tabla de ensayo.  
  
    > [!TIP]  
    >  El nombre del modelo debe formar parte del nombre de la tabla de almacenamiento provisional, por ejemplo *Nombremodelo_Nombreentidad*. Esto hace que resulte más sencillo buscar tablas en la base de datos. Para obtener más información acerca de las tablas de ensayo, consulte [importación de datos &#40;Master Data Services&#41;](overview-importing-data-from-tables-master-data-services.md).  
  
7.  Opcional. Active la casilla **Crear automáticamente valores Code** . Para obtener más información, consulte [Creación automática de código &#40;Master Data Services&#41;](../../2014/master-data-services/automatic-code-creation-master-data-services.md).  
  
8.  Desde el **habilitar jerarquías explícitas y colecciones** lista, seleccione una de las siguientes opciones:  
  
    -   **No**. Seleccione esta opción si no necesita habilitar la entidad para las jerarquías explícitas y las colecciones. Puede cambiar esta opción posteriormente, si es necesario.  
  
    -   **Sí**. Seleccione esta opción si desea habilitar la entidad para las jerarquías explícitas y colecciones. En el **nombre de jerarquía explícita** , escriba un nombre. Si lo desea, seleccione **jerarquía obligatoria (todos los miembros hoja están incluidos** para hacer que la jerarquía explícita obligatoria.  
  
9. Haga clic en **Guardar entidad**.  
  
## <a name="next-steps"></a>Pasos siguientes  
  
-   [Crear un atributo de texto &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-text-attribute-master-data-services.md)  
  
-   [Crear un atributo basado en dominio &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-domain-based-attribute-master-data-services.md)  
  
-   [Crear un atributo de archivo &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-file-attribute-master-data-services.md)  
  
## <a name="see-also"></a>Vea también  
 [Las entidades &#40;Master Data Services&#41;](../../2014/master-data-services/entities-master-data-services.md)   
 [Jerarquías explícitas &#40;Master Data Services&#41;](../../2014/master-data-services/explicit-hierarchies-master-data-services.md)   
 [Cambiar el nombre de una entidad &#40;Master Data Services&#41;](edit-an-entity-master-data-services.md)   
 [Eliminar una entidad &#40;Master Data Services&#41;](../../2014/master-data-services/delete-an-entity-master-data-services.md)  
  
  
