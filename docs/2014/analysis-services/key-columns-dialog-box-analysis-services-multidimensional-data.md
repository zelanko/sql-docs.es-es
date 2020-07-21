---
title: Cuadro de diálogo columnas de clave (Analysis Services-datos multidimensionales) | Microsoft Docs
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
ms.openlocfilehash: 0758c814a7edce134be01ebf766a12832e942a61
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/09/2020
ms.locfileid: "84543708"
---
# <a name="key-columns-dialog-box-analysis-services---multidimensional-data"></a>Cuadro de diálogo Columnas de clave (Analysis Services - Datos multidimensionales)
  Use el cuadro de diálogo **Columnas de clave** para cambiar la propiedad **KeyColumns** de un atributo. Para más información, vea [Modificar la propiedad KeyColumns de un atributo](multidimensional-models/attribute-properties-modify-the-keycolumn-property.md).  
  
 **Para mostrar el cuadro de diálogo Columnas de clave**  
  
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
  
## <a name="see-also"></a>Consulte también  
 [Analysis Services diseñadores y cuadros de diálogo &#40;datos multidimensionales&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)  
  
  
