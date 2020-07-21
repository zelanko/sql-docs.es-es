---
title: Dar formato al texto en un cuadro de texto (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: df0794b5-96b0-4034-bd17-1be7f31e29db
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 976130697e759fa4231ad73113d0970e345dbb3a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66105865"
---
# <a name="format-text-in-a-text-box-report-builder-and-ssrs"></a>Dar formato al texto en un cuadro de texto (Generador de informes y SSRS)
  Puede dar formato por separado a cualquier parte del texto de un cuadro de texto, y usar texto de marcador de posición y texto estático en un mismo cuadro de texto. Esta capacidad de mezclar formatos y agregar texto de marcador de posición permite crear combinaciones de correspondencia o plantillas para el texto del informe. Podrá definir y dar formato a cualquier expresión de forma independiente mediante un marcador de posición.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-combine-multiple-formats-in-a-text-box"></a>Para combinar varios formatos en un cuadro de texto  
  
1.  En la pestaña **Insertar** , haga clic en **Cuadro de texto**. Haga clic en la superficie de diseño y, a continuación, arrastre para crear un cuadro que tenga el tamaño que desee.  
  
2.  Dentro del cuadro de texto, seleccione el texto al que desea dar formato.  
  
3.  Haga clic con el botón derecho en el texto y, después, haga clic en **Propiedades de texto**.  
  
4.  Establezca las opciones de formato. Por ejemplo, en la pestaña **General** :  
  
    -   **Información sobre herramientas** Escriba un texto o una expresión que se evalúe como una información sobre herramientas. La información sobre herramientas aparece cuando el usuario pausa el puntero sobre el elemento en un informe.  
  
    -   **Tipo de marcado** Seleccione una opción para indicar cómo se representará el texto seleccionado.  
  
         **Texto sin formato** : muestra el texto seleccionado como texto simple. El código HTML se tratará como texto literal.  
  
         **HTML**  : muestra el texto seleccionado como HTML. Si el valor de expresión del marcador de posición contiene etiquetas HTML válidas, estas etiquetas se representarán como HTML. Para más información, vea [Importar HTML en un informe &#40;Generador de informes y SSRS&#41;](importing-html-into-a-report-report-builder-and-ssrs.md).  
  
5.  Haga clic en **OK**.  
  
6.  Repita los pasos del 2 al 5 para el texto restante al que desea dar formato.  
  
### <a name="to-format-text-and-placeholders-differently-in-the-same-text-box"></a>Para dar formato de manera diferente al texto y a los marcadores de posición en el mismo cuadro de texto  
  
1.  En la pestaña **Insertar** , haga clic en **Lista**. Haga clic en la superficie de diseño y, a continuación, arrastre para crear un cuadro que tenga el tamaño que desee. Se abre el cuadro de diálogo **Propiedades del conjunto de datos** . En el informe, podrá utilizar un conjunto de datos compartido o un conjunto de datos incrustado. Para más información, haga clic en [Propiedades del conjunto de datos (cuadro de diálogo), Consulta &#40;Generador de informes&#41;](../report-data/dataset-properties-dialog-box-query-report-builder.md) o [Propiedades del conjunto de datos (cuadro de diálogo), Consulta](../dataset-properties-dialog-box-query.md).  
  
2.  En la pestaña **Insertar** , haga clic en **Cuadro de texto**. Haga clic en la lista y, a continuación, arrastre para crear un cuadro que tenga el tamaño que desee.  
  
3.  Escriba una etiqueta en el cuadro de texto, por ejemplo, **Mi campo**:.  
  
4.  Arrastre un campo desde el conjunto de datos hasta el cuadro de texto. Se crea un marcador de posición para el campo.  
  
5.  Para el formato básico, seleccione el texto del marcador de posición y, a continuación, haga clic en una de las opciones de formato del grupo **Fuente** de la pestaña **Inicio** . Por ejemplo, haga clic en el botón **Negrita**.  
  
     Para obtener más opciones de formato, haga clic con el botón derecho en el texto del marcador de posición y, después, haga clic en **Propiedades del marcador de posición**.  
  
6.  Haga clic en **OK**. En la vista de diseño de informe, el cuadro de texto debe contener "**Mi campo**: [*FieldName*]", donde *FieldName* es el nombre del campo.  
  
7.  Haga clic en **Ejecutar**.  
  
 La lista se repite una vez por cada valor del campo y el marcador de posición *FieldName* se reemplaza cada vez por el valor de ese campo en el conjunto de datos.  
  
## <a name="see-also"></a>Consulte también  
 [Cuadros de texto &#40;Generador de informes y SSRS&#41;](text-boxes-report-builder-and-ssrs.md)   
 [Aplicar formato a texto y a marcadores de posición &#40;Generador de informes y SSRS&#41;](formatting-text-and-placeholders-report-builder-and-ssrs.md)   
 [Usar expresiones en informes &#40;Generador de informes y SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Ejemplos de expresiones &#40;Generador de informes y SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [Agregar HTML a un informe &#40;Generador de informes y SSRS&#41;](add-html-into-a-report-report-builder-and-ssrs.md)   
 [Enumera &#40;Generador de informes y SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [Aplicar formato a números y fechas &#40;Generador de informes y SSRS&#41;](formatting-numbers-and-dates-report-builder-and-ssrs.md)   
 [Cuadro de diálogo Propiedades del marcador de posición, General &#40;Generador de informes y SSRS&#41;](../placeholder-properties-dialog-box-general-report-builder-and-ssrs.md)  
  
  
