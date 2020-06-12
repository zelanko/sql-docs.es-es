---
title: Cuadro de diálogo crear-editar cálculo con nombre (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dsveditor.createnamedcalculation.f1
helpviewer_keywords:
- Named Calculation dialog box
ms.assetid: 66fb30ae-f5c5-4bfc-80ca-8c8a3a9bb30d
author: minewiskan
ms.author: owend
ms.openlocfilehash: d6a3d94e2e003410bfdeb632d30fc0e5e3f8a0d4
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/08/2020
ms.locfileid: "84526641"
---
# <a name="create-edit-named-calculation-dialog-box-analysis-services"></a>Cuadro de diálogo crear-editar cálculo con nombre (Analysis Services)
  Utilice el cuadro de diálogo **crear/editar cálculo con nombre** en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] para definir o modificar un cálculo con nombre para una tabla en una vista del origen de datos. Para mostrar el cuadro de diálogo **Crear/editar cálculo con nombre**:  
  
-   Haga clic en **Nuevo cálculo con nombre** en el panel de la **barra de herramientas** del **Diseñador de vistas del origen de datos**.  
  
-   Haga clic con el botón derecho en el panel **Tablas** o **Diagrama** del **Diseñador de vistas del origen de datos** y seleccione **Nuevo cálculo con nombre**.  
  
-   Haga clic con el botón derecho en un cálculo con nombre del panel **Diagrama**, en el **Diseñador de vistas del origen de datos**, y seleccione **Editar cálculo con nombre**.  
  
## <a name="options"></a>Opciones  
 **Nombre de columna**  
 Escriba el nombre del cálculo con nombre.  
  
 **Descripción**  
 Escriba la descripción opcional del cálculo con nombre.  
  
 **Expression**  
 Escriba una expresión SQL válida que devuelva un valor escalar. La expresión se envía al proveedor y se valida en la siguiente expresión:  
  
```  
SELECT <Table Name in Data Source>.* , <Expression> AS <Column Name> FROM <Table Name in Data Source>AS <Table Name in Data Source View>  
```  
  
 La expresión puede tener referencias a otras tablas, mediante una instrucción sub-SELECT. Si la expresión requiere el uso de paréntesis en una instrucción SELECT, la expresión que se especifique debe estar entre paréntesis.  
  
## <a name="see-also"></a>Consulte también  
 [Analysis Services diseñadores y cuadros de diálogo &#40;datos multidimensionales&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Diseñador de vistas del origen de datos &#40;Analysis Services - Datos multidimensionales&#41;](data-source-view-designer-analysis-services-multidimensional-data.md)  
  
  
