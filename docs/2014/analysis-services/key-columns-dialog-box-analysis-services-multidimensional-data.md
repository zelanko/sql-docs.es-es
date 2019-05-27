---
title: Cuadro de diálogo (Analysis Services - datos multidimensionales) de las columnas de clave | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql.asvs.dimensiondesigner.dbv.dataitemCollection.f1
helpviewer_keywords:
- DataItem Collection dialog box
ms.assetid: 585f27f2-d5eb-4516-b29a-2084010b7d51
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 26eb85c97c970f9fe1cfaf63ca9861c2be0b4695
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66079472"
---
# <a name="key-columns-dialog-box-analysis-services---multidimensional-data"></a>Cuadro de diálogo Columnas de clave (Analysis Services - Datos multidimensionales)
  Use el cuadro de diálogo **Columnas de clave** para cambiar la propiedad **KeyColumns** de un atributo. Para más información, vea [Modificar la propiedad KeyColumns de un atributo](multidimensional-models/attribute-properties-modify-the-keycolumn-property.md).  
  
 **Para mostrar el cuadro de diálogo columnas de clave**  
  
-   En [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] o [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], seleccione un atributo y, en la ventana **Propiedades** , haga clic en el botón de puntos suspensivos (**…**) asociado a la propiedad **KeyColumns** de dicho atributo.  
  
## <a name="options"></a>Opciones  
 **Tabla de origen**  
 Seleccione la tabla de origen para la que desea seleccionar sus columnas de clave. Puede seleccionar la tabla de origen en una lista de todas las tablas en la Vista de origen de datos.  
  
 **Columnas disponibles**  
 Seleccione las columnas que desea usar como columnas de clave. Puede seleccionar las columnas en una lista de columnas en la **Tabla de origen** especificada que no haya seleccionado todavía como columnas de clave.  
  
 Para agregar las columnas seleccionadas a la lista **Columnas de clave** , haga clic en el botón **>** .  
  
 **Columnas de clave**  
 Defina el orden de las columnas de clave seleccionadas. El orden de las columnas de clave es importante para definir la clave compuesta correcta. Para ordenar o cambiar el orden de las columnas de clave, seleccione una columna y, a continuación, haga clic en el botón **Subir** o **Bajar** .  
  
 Para quitar una columna de la lista **Columnas de clave** , seleccione la columna y haga clic en el botón **\<** .  
  
 **Subir**  
 Haga clic para subir una posición la columna seleccionada en **Columnas de clave** .  
  
> [!NOTE]  
>  Esta opción solo está habilitada si la lista contiene más de una columna y está seleccionada una columna.  
  
 **Bajar**  
 Haga clic para bajar una posición la columna seleccionada en **Columnas de clave** .  
  
> [!NOTE]  
>  Esta opción solo está habilitada si la lista contiene más de una columna y está seleccionada una columna.  
  
 **>**  
 Haga clic para agregar una nueva columna al final de las columnas de lista **Columnas de clave**.  
  
 **<**  
 Haga clic para quitar la columna seleccionada de las columnas de la lista **Columnas de clave**.  
  
## <a name="see-also"></a>Vea también  
 [Diseñadores y cuadros de diálogo de Analysis Services &#40;datos multidimensionales&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)  
  
  
