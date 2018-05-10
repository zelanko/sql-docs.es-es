---
title: Agregar, cambiar o eliminar valores predeterminados para un parámetro de informe | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-design
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- "10460"
- sql13.rtp.rptdesigner.reportparameters.defaultvalues.f1
- "10072"
ms.assetid: 6a87e069-b3a9-47b6-bcec-afcdd8aff65f
caps.latest.revision: 11
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 86e726e458454a5f1016b36b5a63f0e4fdaaf542
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="add-change-or-delete-default-values-for-a-report-parameter"></a>Agregar, cambiar o eliminar valores predeterminados para un parámetro de informe
  Después de crear un parámetro de informe, puede proporcionar una lista de valores predeterminados. Si todos los parámetros tienen un valor predeterminado válido, el informe se ejecuta automáticamente al verlo u obtener su previa por primera vez.  
  
 Los parámetros de informe pueden representar uno o varios valores. Para los valores únicos, puede proporcionar un literal o una expresión. Para los valores múltiples, puede proporcionar una lista estática o una lista procedente de un conjunto de datos de informe.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 Después de publicar un informe, puede invalidar los valores predeterminados que define en el informe en la herramienta de creación de informes; para ello, establezca los valores de propiedad de parámetro en el servidor de informes. También puede proporcionar varios conjuntos de valores de parámetros predeterminados creando informes vinculados. Para más información, vea  [Parámetros de informe &#40;Generador de informes y Diseñador de informes&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)  
  
### <a name="to-add-or-change-the-default-values-for-a-report-parameter"></a>Para agregar o cambiar los valores predeterminados para un parámetro de informe  
  
1.  En el panel Datos de informe, expanda el nodo **Parámetros** . Haga clic con el botón derecho en el parámetro y haga clic en **Editar**. Se abrirá el cuadro de diálogo **Propiedades de parámetro de informe** .  
  
    > [!NOTE]  
    >  Si el panel Datos de informe no es visible, haga clic en **Ver** y, después, haga clic en **Datos de informe**.  
  
2.  Haga clic en **Valores predeterminados**.  
  
3.  Seleccione una opción predeterminada:  
  
    -   Para proporcionar manualmente un valor o una lista de valores, haga clic en **Especificar valores**. Haga clic en **Agregar** y, a continuación, especifique el valor en el cuadro de texto **Valor** . Puede escribir una expresión como valor. El tipo de datos debe coincidir con el tipo de datos del parámetro. No se pueden usar nombres de campo en una expresión para un parámetro.  
  
         Para los parámetros de varios valores, repita este paso cada uno de los valores que desea proporcionar. El orden de los elementos en esta lista determina el orden en que los verá el usuario en la lista desplegable. Para cambiar el orden de un elemento en la lista, haga clic en el cuadro de texto **Valor** para seleccionar el elemento y, a continuación, use los botones de flecha arriba y flecha abajo para mover el elemento hacia arriba o hacia abajo en la lista.  
  
    -   Para proporcionar el nombre de un conjunto de datos existente que recupere los valores, haga clic en **Obtener valores a partir de una consulta**. En **Conjunto de datos**, elija el nombre del conjunto de datos.  
  
         En **Campo de valor**, elija el nombre del campo que proporciona los valores de parámetro.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-remove-the-default-values-for-a-report-parameter"></a>Para quitar los valores predeterminados para un parámetro de informe  
  
1.  En el panel Datos de informe, expanda el nodo **Parámetros** . Haga clic con el botón derecho en el parámetro y haga clic en **Editar**. Se abrirá el cuadro de diálogo **Propiedades de parámetro de informe** .  
  
2.  Haga clic en **Valores predeterminados**.  
  
3.  En **Seleccione una de las opciones siguientes**, haga clic en **Ningún valor predeterminado**.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Ver también  
 [Parámetros de informe &#40;Generador de informes y Diseñador de informes&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [Agregar parámetros en cascada a un informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/add-cascading-parameters-to-a-report-report-builder-and-ssrs.md)   
 [Tutorial: Agregar un parámetro a un informe &#40;Generador de informes&#41;](../../reporting-services/tutorial-add-a-parameter-to-your-report-report-builder.md)   
 [Agregar filtros de conjunto de datos, filtros de región de datos y filtros de grupo &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)   
 [Usar referencias a la colección de parámetros &#40;generador de informes y SSRS&#41;](../../reporting-services/report-design/built-in-collections-parameters-collection-references-report-builder.md)   
 [Cambiar el orden de un parámetro de informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/change-the-order-of-a-report-parameter-report-builder-and-ssrs.md)   
 [Agregar, cambiar o eliminar parámetros de informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/add-change-or-delete-a-report-parameter-report-builder-and-ssrs.md)   
 [Expresiones &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  
  
  
