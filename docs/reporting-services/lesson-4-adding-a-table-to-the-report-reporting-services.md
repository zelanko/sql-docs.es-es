---
title: 'Lección 4: Adición de una tabla al informe | Microsoft Docs'
description: Para crear el diseño de un informe, puede arrastrar y colocar objetos de informe (por ejemplo, una tabla) desde el panel Cuadro de herramientas hasta la superficie de diseño.
ms.date: 12/16/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 5ddf2914-bcdd-427d-8cba-0ccb8342f819
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 0194591ffec572c7d079c70233de45977a38d130
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/28/2020
ms.locfileid: "87246314"
---
# <a name="lesson-4-add-a-table-to-the-report-reporting-services"></a>Lección 4: Adición de una tabla al informe (Reporting Services)

Después de definir el conjunto de datos, puede empezar a diseñar el informe paginado. Cree el diseño de un informe; para ello, arrastre y coloque los *objetos de informe* desde el panel **Cuadro de herramientas** hasta la **superficie de diseño**. Algunos de los tipos de objetos de informe son:

- Tabla
- Cuadro de texto
- Imagen
- Línea
- Rectángulo
- Gráfico
- Map

Los elementos que contienen filas de datos repetidas procedentes de conjuntos de datos subyacentes se denominan *regiones de datos*. Después de agregar una región de datos, puede agregar campos a la misma. Un informe básico tendrá solo una región de datos. Puede agregar más para mostrar información adicional, como un gráfico.

## <a name="add-a-table-data-region-and-fields-to-a-report-layout"></a>Adición de campos y de una región de datos de tabla a un diseño de informe

1. Seleccione la pestaña **Cuadro de herramientas** en el panel izquierdo del Diseñador de informes. Con el mouse, seleccione el objeto **Tabla** y arrástrelo hasta la superficie del diseño de informe. El Diseñador de informes dibuja una región de datos de tabla con tres columnas en el centro de la superficie de diseño. Si no ve la pestaña **Cuadro de herramientas**, seleccione el menú **Ver** > **Cuadro de herramientas**.

    ![ssrs_ssdt_addtable](media/ssrs-ssdt-addtable.png)

    También puede agregar una tabla al informe desde la superficie de diseño. Haga clic con el botón derecho en la superficie de diseño y seleccione **Insertar** > **Tabla**.

2. En el panel **Datos de informe**, expanda AdventureWorksDataset para mostrar los campos.

3. Arrastre el campo `[Date]` desde el panel **Datos de informe** hasta la primera columna de la tabla.

    > [!IMPORTANT]
    > Al colocar el campo en la primera columna, suceden dos cosas. En primer lugar, el Diseñador de informes muestra el nombre del campo, que se conoce como la *expresión de campo*, entre corchetes: `[Date]` en la celda de datos. En segundo lugar, agrega una etiqueta de columna a la fila de encabezado, justo encima de la expresión de campo. De forma predeterminada, la etiqueta de columna tiene el nombre del campo. Puede seleccionar la etiqueta de columna y escribir un nuevo valor, en caso de que desee cambiarlo.

4. Arrastre el campo `[Order]` desde el panel **Datos de informe** hasta la segunda columna de la tabla.

5. Arrastre el campo `[Product]` desde el panel **Datos de informe** hasta la tercera columna de la tabla.

6. Arrastre el campo `[Qty]` hasta el borde derecho de la tercera columna hasta que obtenga un cursor vertical y el puntero del mouse muestre un signo más [+]. Cuando suelte el botón, se creará una cuarta columna para la expresión de campo `[Qty]`.

    ![ssrs_tutorial_addcolumn](media/ssrs-tutorial-addcolumn.png)

7. Agregue el campo `[LineTotal]` de la misma manera, creando una quinta columna. La etiqueta de columna se agrega como "Line Total". El Diseñador de informes crea automáticamente un nombre descriptivo para la columna, para lo cual, divide "LineTotal" en dos palabras.

En el diagrama siguiente se muestra una región de datos de tabla rellenada con estos campos: Date, Order, Product, Qty y Line Total.
![rs_BasicTableDetailsDesign](media/rs-basictabledetailsdesign.png)

## <a name="preview-your-report"></a>Obtener una vista previa del informe

Al obtener una vista previa de un informe, se puede ver el informe representado sin tener que publicarlo antes en un servidor de informes. Obtenga una vista previa del informe con frecuencia mientras lo diseña. Al hacerlo, valida las conexiones de datos y diseño, lo que le permite corregir los errores y problemas a medida que avanza.

### <a name="to-preview-a-report"></a>Para obtener una vista previa de un informe

- Seleccione la pestaña **Vista previa**. El Diseñador de informes ejecuta el informe y lo muestra en la **Vista previa**.

    ![ssrs_ssdt_preview](media/ssrs-ssdt-preview.png)

El diagrama siguiente muestra parte del informe en la **Vista previa**.

   ![Vista previa, filas de detalle de la tabla con 5 columnas](media/rs-basictabledetailspreview.png "Vista previa, filas de detalle de la tabla con 5 columnas")

Examine los valores de Date y Line Total. En la siguiente lección, va a obtener información sobre cómo darles formato para que presenten más nitidez.

> [!NOTE]
> En el menú **Archivo**, seleccione **Guardar todo** para guardar el informe.

## <a name="next-steps"></a>Pasos siguientes

Ha agregado correctamente una región de datos de tabla al informe, ha agregado campos a la región de datos y ha obtenido una vista previa del informe. En la siguiente lección, va a obtener información sobre cómo dar formato a los encabezados de columna y a las expresiones de campo. Luego, continúe con [Lección 5: Aplicación de formato a un informe &#40;Reporting Services&#41;](lesson-5-formatting-a-report-reporting-services.md).
  
## <a name="see-also"></a>Consulte también

[Tablas &#40;Generador de informes y SSRS&#41;](report-design/tables-report-builder-and-ssrs.md)  
[Colección Campos del conjunto de datos &#40;Generador de informes y SSRS&#41;](report-data/dataset-fields-collection-report-builder-and-ssrs.md)  
