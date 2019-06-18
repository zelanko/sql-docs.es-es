---
title: Ocultar un elemento (Generador de informes y SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-builder
ms.topic: conceptual
f1_keywords:
- sql13.rtp.rptdesigner.shared.visibility.f1
- "10503"
ms.assetid: 9d78f8de-959b-456f-8947-687fa6e2ba91
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 2a6e57c1e4326f2c8a0f04a515aab7c699778f39
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65580704"
---
# <a name="hide-an-item-report-builder-and-ssrs"></a>Ocultar un elemento (Generador de informes y SSRS)
  Establezca la visibilidad de un elemento de informe cuando desee ocultar condicionalmente un elemento basándose en un parámetro de informe o en alguna otra expresión que especifique.  
  
 También puede diseñar un informe que permita al usuario cambiar la visibilidad de los elementos de informe haciendo clic en los cuadros de texto del informe, por ejemplo, para un informe detallado. Para obtener más información, vea [Agregar una acción de expandir y contraer a un elemento &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/add-an-expand-or-collapse-action-to-an-item-report-builder-and-ssrs.md).  
  
 Los procedimientos siguientes describen cómo mostrar u ocultar un elemento de informe en un informe representado en una constante o en una expresión.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-hide-a-report-item"></a>Ocultar un elemento de informe  
  
1.  En la vista de diseño de informe, haga clic con el botón derecho en el elemento de informe y, después, abra la página **Propiedades** .  
  
    > [!NOTE]  
    >  Para seleccionar una tabla entera o una región de datos de la matriz, haga clic en la región de datos para seleccionarla, haga clic con el botón derecho en un identificador de fila, de columna o de tabla y, después, haga clic en **Propiedades de Tablix**.  
  
2.  Haga clic en **Visibilidad**.  
  
3.  En **Cuando se ejecute inicialmente el informe**, especifique si desea ocultar el elemento la primera vez que se ve el informe:  
  
    -   Para mostrar el elemento, haga clic en **Mostrar**.  
  
    -   Para ocultar el elemento, haga clic en **Ocultar**.  
  
    -   Para especificar una expresión que se evalúa en tiempo de ejecución, haga clic en **Mostrar u ocultar en función de una expresión**. Escriba la expresión o haga clic en el botón de expresión (**fx**) para crearla en el cuadro de diálogo **Expresión** .  
  
        > [!NOTE]  
        >  Al especificar una expresión para la visibilidad, está estableciendo la propiedad Hidden del elemento de informe, tal como se muestra en la siguiente imagen. La expresión evaluada muestra el elemento de informe cuando el valor es False, y lo oculta cuando el valor es True.   
        > ![Cuadro de diálogo Properties_Visibility y propiedad Hidden](../../reporting-services/report-builder/media/hiddenproperty-propertiesvisibility.png "Cuadro de diálogo Properties_Visibility y propiedad Hidden")  
  
4.  Haga clic en **Aceptar** dos veces.  
  
### <a name="to-hide-static-rows-in-a-table-matrix-or-list"></a>Ocultar las filas estáticas de una tabla, matriz o lista  
  
1.  En la vista de diseño de informe, haga clic en la tabla, matriz o lista para mostrar los controladores de fila y de columna.  
  
2.  Haga clic con el botón derecho en el identificador de fila y, después, haga clic en **Visibilidad de fila**. Se abrirá el cuadro de diálogo **Visibilidad de fila** .  
  
3.  Para establecer la visibilidad, siga los pasos 3 y 4 del primer procedimiento.  
  
### <a name="to-hide-static-columns-in-a-table-matrix-or-list"></a>Para ocultar las columnas estáticas de una tabla, matriz o lista  
  
1.  En la vista Diseño, seleccione la tabla, matriz o lista para mostrar los identificadores de fila y de columna.  
  
2.  Haga clic con el botón derecho en el identificador de columna y, después, haga clic en **Visibilidad de columna**.  
  
3.  En el cuadro de diálogo **Visibilidad de columna** , siga los pasos 3 y 4 del primer procedimiento.  
  
## <a name="see-also"></a>Consulte también  
 [Acción de obtención de detalles &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/drilldown-action-report-builder-and-ssrs.md)   
 [Agregar una acción de expandir y contraer a un elemento &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/add-an-expand-or-collapse-action-to-an-item-report-builder-and-ssrs.md)   
 [Ejemplos de expresiones &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)  
  
  
