---
title: Agregar o quitar tablas o vistas de un tipo de datos del origen de vista (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dsvdesigner.tablespane.f1
helpviewer_keywords:
- deleting tables
- tables [Analysis Services]
- removing tables
- adding tables
- data source views [Analysis Services], tables
- tables [Analysis Services], data source views
ms.assetid: 98307d04-6548-4d7d-9244-2371dd165249
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: dc78ad1f8a1f49d1a42c5b2ded45a913cdd7e669
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48117961"
---
# <a name="adding-or-removing-tables-or-views-in-a-data-source-view-analysis-services"></a>Agregar o quitar tablas o vistas en una vista del origen de datos (Analysis Services)
  Después de crear una vista del origen de datos (DSV) en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], puede modificarla en el Diseñador de vistas del origen de datos agregando o quitando tablas y columnas, incluidas las tablas y columnas procedentes de otro origen de datos.  
  
 Para abrir la DSV en el Diseñador de vistas del origen de datos, haga doble clic en la vista en el Explorador de soluciones. Una vez que abra la DSV, puede usar el comando **Agregar o quitar tablas** en la barra de botones o en el menú para modificar o ampliar la DSV. También puede trabajar con objetos del diagrama. Por ejemplo, puede seleccionar un objeto y luego usar la tecla Supr del teclado para quitar el objeto.  
  
> [!WARNING]  
>  Tenga cuidado al quitar una tabla. Al quitar una tabla se eliminan todas las columnas y relaciones asociadas de la DSV y se invalidan todos los objetos enlazados a esa tabla.  
  
## <a name="selecting-tables-or-views-to-add-or-remove"></a>Seleccionar las tablas o vistas que se van a agregar o quitar  
 El cuadro de diálogo **Agregar o quitar tablas** le permite mover tablas o vistas entre las listas **Objetos disponibles** y **Objetos incluidos** . La lista **Objetos disponibles** incluye inicialmente las tablas o vistas del origen de datos principal que no están ya incluidas en la vista del origen de datos. Si el origen de datos principales admite la `OPENROWSET` función, también puede agregar tablas o vistas desde otros orígenes de datos en el proyecto o base de datos.  
  
 Si se agrega o se quita una tabla de una DSV, también se agrega o se quita la tabla del diagrama seleccionado actualmente en la DSV. Para obtener más información sobre los diagramas, vea [Work with Diagrams in Data Source View Designer &#40;Analysis Services&#41;](work-with-diagrams-in-data-source-view-designer-analysis-services.md).  
  
 Después de mover una tabla a la lista **Objetos incluidos** del cuadro de diálogo **Agregar o quitar tablas** , puede agregar todas las tablas relacionadas. Esta operación agrega las tablas según las restricciones de clave externa del origen de datos, si existen. Si no existen restricciones de clave externa, puede usar el `NameMatchingCriteria` propiedad de la vista del origen de datos para determinar las relaciones mediante la especificación de un criterio de coincidencia de nombres de columna en las tablas para generar relaciones probables. Si el `NameMatchingCriteria`propiedad se especifica para la vista del origen de datos, haga clic en **agregar tablas relacionadas** para agregar las tablas del origen de datos que tienen nombres de columna coincidan. Para obtener más información sobre la configuración de la `NameMatchingCriteria` propiedad, vea [vistas del origen de datos en modelos multidimensionales](data-source-views-in-multidimensional-models.md).  
  
> [!NOTE]  
>  Agregar o quitar objetos de una vista del origen de datos no afecta al origen de datos subyacente.  
  
## <a name="see-also"></a>Vea también  
 [Vistas del origen de datos en modelos multidimensionales](data-source-views-in-multidimensional-models.md)   
 [Trabajar con diagramas en el Diseñador de vistas del origen de datos &#40;Analysis Services&#41;](work-with-diagrams-in-data-source-view-designer-analysis-services.md)  
  
  
