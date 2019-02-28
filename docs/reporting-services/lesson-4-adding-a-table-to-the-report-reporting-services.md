---
title: 'Lección 4: Agregar una tabla al informe (Reporting Services) | Microsoft Docs'
ms.date: 05/23/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 5ddf2914-bcdd-427d-8cba-0ccb8342f819
author: markingmyname
ms.author: maghan
ms.openlocfilehash: a4df3f6c94ff4aee674721a47421e0696cc8e2c3
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/15/2019
ms.locfileid: "56287243"
---
# <a name="lesson-4-adding-a-table-to-the-report-reporting-services"></a>Lección 4: Agregar una tabla al informe (Reporting Services)
Después de definir un conjunto de datos, puede comenzar a diseñar el diseño. El diseño del informe se crea arrastrando y colocando en la superficie de diseño regiones de datos, cuadros de texto, imágenes y otros elementos que se desean incluir en el informe.  
  
Los elementos que contienen filas de datos repetidas procedentes de conjuntos de datos subyacentes se denominan *regiones de datos*. Un informe básico solo contendrá una región de datos, pero puede agregar más si, por ejemplo, desea agregar un gráfico al informe de tabla. Después de agregar una región de datos, puede agregar campos a la misma.  
  
### <a name="to-add-a-table-data-region-and-fields-to-a-report-layout"></a>Para agregar una región de datos de tabla y campos a un diseño de informe  
  
1.  En el **Cuadro de herramientas**, haga clic en **Tabla**y, después, haga clic en la superficie de diseño y arrastre el mouse. El Diseñador de informes dibuja una región de datos de tabla con tres columnas en el centro de la superficie de diseño. El **Cuadro de herramientas** puede aparecer como una pestaña a la izquierda del panel **Datos de informe** . Para abrir el **Cuadro de herramientas**, pase el puntero por encima de la pestaña **Cuadro de herramientas** . Si el **Cuadro de herramientas** no está visible, en el menú **Ver**, haga clic en **Cuadro de herramientas**.
  
     ![ssrs_ssdt_addtable](../reporting-services/media/ssrs-ssdt-addtable.png) 
  
  También puede agregar una tabla al informe desde la superficie de diseño.  Haga clic con el botón derecho en la superficie de diseño, haga clic en **Insertar** y, después, en **Tabla**.
2.  En el panel **Datos de informe** , expanda el conjunto de datos **AdventureWorksDataset** para mostrar los campos.  
  
3.  Arrastre el campo *Date* desde el panel **Datos de informe** hasta la primera columna de la tabla.  
  
    Al colocar el campo en la primera columna, suceden dos cosas. En primer lugar, la celda de datos mostrará el nombre del campo, que se conoce como la *expresión de campo*, entre corchetes: `[Date]`. En segundo lugar, se agrega automáticamente un valor de encabezado de columna a la fila Encabezado, inmediatamente encima de la expresión de campo. De forma predeterminada, la columna tiene el nombre del campo. Puede seleccionar el texto de la fila Encabezado y escribir un nuevo nombre.  
  
4.  Arrastre el campo *Order* desde el panel **Datos de informe** hasta la segunda columna de la tabla.  
  
5.  Arrastre el campo *Product* desde el panel **Datos de informe** hasta la tercera columna de la tabla.  
  
6.  Arrastre el campo Qty hasta el borde derecho de la tercera columna hasta que obtenga un cursor vertical y el puntero del mouse tenga un signo más [+]. Cuando suelte el botón, se creará una cuarta columna para `[Qty]`.  
![ssrs_tutorial_addcolumn](../reporting-services/media/ssrs-tutorial-addcolumn.png)  
  
7.  Agregue el campo LineTotal de la misma manera, creando una quinta columna. El encabezado de columna es Line Total. El Diseñador de informes crea automáticamente un nombre descriptivo para la columna, para lo cual, divide LineTotal en dos palabras.  
  
  
En el diagrama siguiente se muestra una región de datos de tabla rellenada con estos campos: Date, Order, Product, Qty y Line Total.  
![rs_BasicTableDetailsDesign](../reporting-services/media/rs-basictabledetailsdesign.png)  
  
## <a name="preview-your-report"></a>Obtener una vista previa del informe  
Al obtener una vista previa de un informe, se puede ver el informe representado sin tener que publicarlo antes en un servidor de informes. Es probable que desee obtener frecuentemente una vista previa de un informe durante su diseño. Al obtener la vista previa del informe, también se ejecutará la validación en el diseño y las conexiones de datos de modo que pueda corregir los errores y los problemas antes de publicar el informe en un servidor de informes.  
  
#### <a name="to-preview-a-report"></a>Para obtener una vista previa de un informe  
  
-   Haga clic en la pestaña **Vista previa** . El Diseñador de informes ejecuta el informe y lo muestra en la Vista previa.
![ssrs_ssdt_preview](../reporting-services/media/ssrs-ssdt-preview.png)  
  
    El diagrama siguiente muestra parte del informe en la Vista previa.  
  
    ![Vista previa, filas de detalle de la tabla con 5 columnas](../reporting-services/media/rs-basictabledetailspreview.png "Vista previa, filas de detalle de la tabla con 5 columnas")  
  
    Observe que la moneda (en la columna de Line Total) tiene seis posiciones decimales, y que la fecha incluye una marca de tiempo. En la lección siguiente corregirá ese formato.  
  
> [!NOTE]  
> En el menú **Archivo** , haga clic en **Guardar todo** para guardar el informe.  
  
## <a name="next-steps"></a>Next Steps  
Ha agregado correctamente una región de datos de tabla al informe, ha agregado campos a la región de datos y ha obtenido una vista previa del informe. A continuación, dará formato a los encabezados de columna y a los valores de fecha y de moneda. Consulte [Lección 5: Aplicación de formato a un informe &#40;Reporting Services&#41;](../reporting-services/lesson-5-formatting-a-report-reporting-services.md).  
  
## <a name="see-also"></a>Consulte también  
[Tablas &#40;Generador de informes y SSRS&#41;](../reporting-services/report-design/tables-report-builder-and-ssrs.md)  
[Colección Campos del conjunto de datos &#40;Generador de informes y SSRS&#41;](../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)  
