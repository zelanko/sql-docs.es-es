---
title: Crear una entidad (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- entities [Master Data Services], creating
- creating entities [Master Data Services]
ms.assetid: d9a6a51e-7b53-4785-a118-3baeb7ca2d48
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: d85fc4c21f200bcdc5a489cfcee6b50bc9f4b98e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "65479912"
---
# <a name="create-an-entity-master-data-services"></a>Crear una entidad (Master Data Services)
  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], cree una entidad para contener los miembros y sus atributos.  
  
## <a name="prerequisites"></a>Requisitos previos  
 Para realizar este procedimiento:  
  
-   Debe disponer de permiso para tener acceso al área funcional de **Administración del sistema** .  
  
-   Debe ser administrador de modelo. Para obtener más información, vea [administradores &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
-   Debe existir un modelo. Para obtener más información, consulte [Crear un modelo &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-model-master-data-services.md).  
  
### <a name="to-create-an-entity"></a>Crear una entidad  
  
1.  En [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], haga clic en **Administración del sistema**.  
  
2.  En la página **Vista de modelo** , en la barra de menús, seleccione **Administrar** y haga clic en **Entidades**.  
  
3.  En la página **Mantenimiento de entidades** , en la lista **Modelo** , seleccione un modelo.  
  
4.  Haga clic en **Agregar entidad**.  
  
5.  En el cuadro **nombre de entidad** , escriba el nombre de la entidad.  
  
6.  En el cuadro **nombre de las tablas de ensayo** , escriba un nombre para la tabla de ensayo.  
  
    > [!TIP]  
    >  El nombre del modelo debe formar parte del nombre de la tabla de almacenamiento provisional, por ejemplo *Nombremodelo_Nombreentidad*. Esto hace que resulte más sencillo buscar tablas en la base de datos. Para obtener más información sobre las tablas de almacenamiento provisional, vea [importación de datos &#40;Master Data Services&#41;](overview-importing-data-from-tables-master-data-services.md).  
  
7.  Opcional. Active la casilla **Crear automáticamente valores Code** . Para obtener más información, consulte [creación automática de código &#40;Master Data Services&#41;](../../2014/master-data-services/automatic-code-creation-master-data-services.md).  
  
8.  En la lista **Habilitar jerarquías explícitas y colecciones** , seleccione una de las siguientes opciones:  
  
    -   **No**. Seleccione esta opción si no necesita habilitar la entidad para las jerarquías explícitas y las colecciones. Puede cambiar esta opción posteriormente, si es necesario.  
  
    -   **Sí**. Seleccione esta opción si desea habilitar la entidad para las jerarquías explícitas y colecciones. En el cuadro **nombre de jerarquía explícita** , escriba un nombre. Opcionalmente, seleccione **jerarquía obligatoria (todos los miembros hoja se incluyen** para convertir la jerarquía explícita en una jerarquía obligatoria.  
  
9. Haga clic en **Guardar entidad**.  
  
## <a name="next-steps"></a>Pasos a seguir  
  
-   [Crear un atributo de texto &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-text-attribute-master-data-services.md)  
  
-   [Crear un atributo basado en dominio &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-domain-based-attribute-master-data-services.md)  
  
-   [Crear un atributo de archivo &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-file-attribute-master-data-services.md)  
  
## <a name="see-also"></a>Consulte también  
 [Entidades &#40;Master Data Services&#41;](../../2014/master-data-services/entities-master-data-services.md)   
 [Jerarquías explícitas &#40;Master Data Services&#41;](../../2014/master-data-services/explicit-hierarchies-master-data-services.md)   
 [Cambiar el nombre de una entidad &#40;Master Data Services&#41;](edit-an-entity-master-data-services.md)   
 [Eliminar una entidad &#40;Master Data Services&#41;](../../2014/master-data-services/delete-an-entity-master-data-services.md)  
  
  
