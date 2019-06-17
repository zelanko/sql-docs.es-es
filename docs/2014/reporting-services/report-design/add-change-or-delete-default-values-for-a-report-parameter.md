---
title: Agregar, cambiar o eliminar valores predeterminados para un parámetro de informe (generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10460"
- sql12.rtp.rptdesigner.reportparameters.defaultvalues.f1
- "10072"
ms.assetid: 6a87e069-b3a9-47b6-bcec-afcdd8aff65f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c973f249a60b8a6180d5233604a9c372928d0a48
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66106669"
---
# <a name="add-change-or-delete-default-values-for-a-report-parameter-report-builder-and-ssrs"></a>Agregar, cambiar o eliminar valores predeterminados para un parámetro de informe (Generador de informes y SSRS)
  Después de crear un parámetro de informe, puede proporcionar una lista de valores predeterminados. Si todos los parámetros tienen un valor predeterminado válido, el informe se ejecuta automáticamente al verlo u obtener su previa por primera vez.  
  
 Los parámetros de informe pueden representar uno o varios valores. Para los valores únicos, puede proporcionar un literal o una expresión. Para los valores múltiples, puede proporcionar una lista estática o una lista procedente de un conjunto de datos de informe.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 Después de publicar un informe, puede invalidar los valores predeterminados que define en el informe en la herramienta de creación de informes; para ello, establezca los valores de propiedad de parámetro en el servidor de informes. También puede proporcionar varios conjuntos de valores de parámetros predeterminados creando informes vinculados. Para más información, vea  [Parámetros de informe &#40;Generador de informes y Diseñador de informes&#41;](report-parameters-report-builder-and-report-designer.md)  
  
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
  
## <a name="see-also"></a>Vea también  
 [Parámetros de informe &#40;Generador de informes y Diseñador de informes&#41;](report-parameters-report-builder-and-report-designer.md)   
 [Agregar parámetros en cascada a un informe &#40;Generador de informes y SSRS&#41;](add-cascading-parameters-to-a-report-report-builder-and-ssrs.md)   
 [Tutorial: Agregar un parámetro a un informe &#40;Generador de informes&#41;](../tutorial-add-a-parameter-to-your-report-report-builder.md)   
 [Agregar filtros de conjunto de datos, filtros de región de datos y filtros de grupo &#40;Generador de informes y SSRS&#41;](add-dataset-filters-data-region-filters-and-group-filters.md)   
 [Usar referencias a la colección de parámetros &#40;generador de informes y SSRS&#41;](built-in-collections-parameters-collection-references-report-builder.md)   
 [Cambiar el orden de un parámetro de informe &#40;Generador de informes y SSRS&#41;](change-the-order-of-a-report-parameter-report-builder-and-ssrs.md)   
 [Agregar, cambiar o eliminar parámetros de informe &#40;Generador de informes y SSRS&#41;](add-change-or-delete-a-report-parameter-report-builder-and-ssrs.md)   
 [Expresiones &#40;Generador de informes y SSRS&#41;](expressions-report-builder-and-ssrs.md)  
  
  
