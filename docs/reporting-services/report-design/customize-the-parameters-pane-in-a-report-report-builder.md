---
title: Personalizar el panel de parámetros en un informe (Generador de informes) | Microsoft Docs
description: Aprenda a personalizar el panel Parámetros al crear informes paginados con parámetros en el Generador de informes.
ms.date: 06/15/2020
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 4ce9e8d5-911a-4422-928f-a8d005b79fc6
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 29bd397d64280644394077a29a3420dbf43b5e6f
ms.sourcegitcommit: 7d6eb09588ff3477cf39a8fd507d537a603bc60d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/16/2020
ms.locfileid: "84796566"
---
# <a name="customize-the-parameters-pane-in-a-report-report-builder"></a>Customize the Parameters Pane in a Report (Report Builder)
  Al crear informes paginados con parámetros en el Generador de informes, puede personalizar el panel de parámetros. En la vista de diseño de informe, puede arrastrar un parámetro a una columna y fila específicas del panel de parámetros. Puede agregar y quitar columnas para cambiar el diseño del panel.

 Al arrastrar un parámetro a una columna y fila nuevas del panel, el orden de los parámetros cambiará en el panel **Datos de informe** . Al cambiar el orden de los parámetros en el panel **Datos de informe** , cambia la ubicación de los parámetros en el panel. Para más información sobre por qué es importante el orden de los parámetros, vea [Cambiar el orden de un parámetro de informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/change-the-order-of-a-report-parameter-report-builder-and-ssrs.md).

## <a name="to-customize-the-parameters-pane"></a>Para personalizar el panel de parámetros

1.  En la pestaña **Vista** , seleccione la casilla **Parámetros** para mostrar el panel de parámetros.

     ![Acceder al panel de parámetros de la pestaña Vista](../../reporting-services/report-design/media/ssrs-customparameter-accessparameterpanedesignmode.png "Acceder al panel de parámetros de la pestaña Vista")

     El panel aparece en la parte superior de la superficie de diseño.

2.  Para agregar un parámetro al panel, siga unos de los siguientes procedimientos.

    -   Haga clic con el botón derecho en una celda vacía del panel de parámetros y después haga clic en **Agregar parámetro**.

         ![Agregar nuevo parámetro desde el panel de parámetros](../../reporting-services/report-design/media/ssrs-customizeparameter-addnewparameter.png "Agregar nuevo parámetro desde el panel de parámetros")

    -   Haga clic con el botón derecho en **Parámetros** , en el panel **Datos de informe** y después haga clic en **Agregar parámetro**.

3.  Para mover un parámetro a una ubicación nueva del panel de parámetros, arrastre el parámetro a una celda diferente del panel.

     Cuando cambia la ubicación del parámetro en el panel, el orden del parámetro en la lista **Parámetros** del panel **Datos de informe** se cambia automáticamente. Para más información sobre el impacto del orden de los parámetros, vea [Cambiar el orden de un parámetro de informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/change-the-order-of-a-report-parameter-report-builder-and-ssrs.md)

4.  Para acceder a las propiedades de un parámetro, siga unos de los siguientes procedimientos.

    -   Haga clic con el botón derecho en el parámetro del panel de parámetros y después haga clic en **Propiedades del parámetro**.

         ![Acceder a las propiedades del parámetro desde el panel de parámetros](../../reporting-services/report-design/media/ssrs-customizeparameter-accessparameterproperties-composite.png "Acceder a las propiedades del parámetro desde el panel de parámetros")

    -   Haga clic con el botón derecho en el parámetro del panel **Datos de informe** y después haga clic en **Propiedades del parámetro**.

5.  Para agregar columnas y filas nuevas al panel, o eliminar columnas y filas existentes, haga clic con el botón derecho en cualquier lugar del panel de parámetros y después haga clic en un comando del menú que aparece.

     ![Agregar columnas y filas al panel de parámetros](../../reporting-services/report-design/media/ssrs-customparameter-addcolumnsrows.png "Agregar columnas y filas al panel de parámetros")

    > [!IMPORTANT]
    >  Al eliminar una columna o fila que contiene parámetros, estos se eliminan del informe.

6.  Para eliminar un parámetro del panel y del informe, siga uno de los siguientes procedimientos.

    -   Haga clic con el botón derecho en el parámetro del panel de parámetros y después haga clic en  **Eliminar**.

         ![Eliminar parámetros desde el panel de parámetros](../../reporting-services/report-design/media/ssrs-customparameter-deleteparameter.png "Eliminar parámetros desde el panel de parámetros")

    -   Haga clic con el botón derecho en el panel **Datos de informe** y después haga clic en **Eliminar**.

## <a name="hiddeninternal-parameters-during-runtime"></a>Parámetros ocultos o internos durante el tiempo de ejecución
Si tiene un parámetro oculto o interno, la lógica de si se va a representar como espacio vacío durante el tiempo de ejecución es la siguiente:

   - Si una fila o columna contiene solo parámetros ocultos o internos, o celdas vacías, la fila o columna completa no se representará durante el tiempo de ejecución.
   - De lo contrario, el parámetro oculto o interno, o la celda vacía se representará como espacio vacío

Por ejemplo, `ReportParameter1` está oculto mientras el resto de los parámetros son visibles:

![Ejemplo de parámetro oculto 1](../../reporting-services/report-design/media/ssrs-hidden-parameter-rb-1.png "Un parámetro oculto en la cuadrícula de diseño")

Esto resultará en un espacio vacío durante el tiempo de ejecución porque hay parámetros visibles en la primera columna o fila:

![Ejemplo de parámetro oculto 1: tiempo de ejecución](../../reporting-services/report-design/media/ssrs-hidden-parameter-server-1.png "Un parámetro oculto en la cuadrícula de diseño da lugar a espacio vacío en tiempo de ejecución")

Con el mismo ejemplo, si también establece `ReportParameter3` como oculto:

![Ejemplo de parámetro oculto 2](../../reporting-services/report-design/media/ssrs-hidden-parameter-rb-2.png "Dos parámetros ocultos en la misma columna")

Después, la primera columna no se representa durante el tiempo de ejecución porque toda se considera vacía:

![Ejemplo de parámetro oculto 2: tiempo de ejecución](../../reporting-services/report-design/media/ssrs-hidden-parameter-server-2.png "Dos parámetros ocultos en la misma columna en tiempo de ejecución")

## <a name="default-layout"></a>Diseño predeterminado
Para los informes creados antes de SQL Server Reporting Services 2016, se usará una cuadrícula de diseño de parámetros predeterminada de 2 columnas y N filas durante el tiempo de ejecución. Para cambiar el diseño predeterminado, abra el informe en el Generador de informes de Microsoft y guárdelo. Después de guardar el informe, la información de diseño de parámetros personalizados se guardará en el archivo .rdl.


## <a name="see-also"></a>Consulte también
 [Parámetros de informe &#40;Generador de informes y Diseñador de informes&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)


