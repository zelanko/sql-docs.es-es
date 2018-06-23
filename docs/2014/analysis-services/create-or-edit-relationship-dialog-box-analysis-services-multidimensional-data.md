---
title: Crear o editar el cuadro de diálogo de relación (Analysis Services - datos multidimensionales) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.asvs.dsvdesigner.createrelationship.f1
helpviewer_keywords:
- Create Relationship dialog box
ms.assetid: da3c7074-623e-4ddf-a707-d3276a47cf1c
caps.latest.revision: 19
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: c205a2f7c78345d77dd3080b9ef33fe87f87ba35
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36198072"
---
# <a name="create-or-edit-relationship-dialog-box-analysis-services---multidimensional-data"></a>Cuadro de diálogo Crear o Editar relación (Analysis Services - Datos multidimensionales)
  Use el cuadro de diálogo **Crear/Editar relación** en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] para definir o modificar una relación en una vista del origen de datos. Puede mostrar el cuadro de diálogo **Crear relación/Editar relación** de las siguientes maneras:  
  
-   Haciendo clic en **Nueva relación** en el panel **Barra de herramientas** del **Diseñador de vistas del origen de datos**.  
  
-   Haciendo clic con el botón derecho en una tabla de los paneles **Tablas** o **Diagrama** del **Diseñador de vistas del origen de datos** y seleccionando **Nueva relación**.  
  
-   Haciendo clic con el botón derecho en el panel **Diagrama** del **Diseñador de vistas del origen de datos** y seleccionando **Editar relación**.  
  
> [!NOTE]  
>  Puede crear relaciones en el **Diseñador de vistas del origen de datos** que no existen en el origen de datos subyacente y eliminar relaciones creadas mediante el **Diseñador de vistas del origen de datos** a partir de relaciones de clave externa en el origen de datos subyacente.  
  
## <a name="options"></a>Opciones  
 **Tabla de origen (clave externa)**  
 Seleccione la tabla o consulta con nombre que contiene la referencia a una o varias columnas de la tabla de destino.  
  
 **Tabla de destino (clave principal)**  
 Seleccione la tabla que contiene una o varias columnas a las que la tabla de origen hace referencia. Para autocombinaciones, seleccione la misma tabla seleccionada en la **Tabla de origen (de clave externa)**.  
  
 **Columnas de origen**  
 Seleccione las columnas que hacen referencia a columnas de la tabla de destino.  
  
 **Columnas de destino**  
 Seleccione las columnas a las que hacen referencia las columnas de la tabla de origen.  
  
 **Invertir**  
 Haga clic para invertir la dirección de la relación.  
  
 **Descripción**  
 Escriba una descripción opcional para la relación.  
  
## <a name="see-also"></a>Vea también  
 [Diseñadores y cuadros de diálogo de Analysis Services &#40;datos multidimensionales&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Diseñador de vistas del origen de datos &#40;Analysis Services - datos multidimensionales&#41;](data-source-view-designer-analysis-services-multidimensional-data.md)  
  
  