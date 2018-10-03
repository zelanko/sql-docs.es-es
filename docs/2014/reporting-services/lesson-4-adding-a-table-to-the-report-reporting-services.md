---
title: 'Lección 4: Agregar una tabla al informe (Reporting Services) | Microsoft Docs'
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 5ddf2914-bcdd-427d-8cba-0ccb8342f819
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: d990d18498547434a6f7774dfcee076d2986ee40
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48220815"
---
# <a name="lesson-4-adding-a-table-to-the-report-reporting-services"></a>Lección 4: Agregar una tabla al informe (Reporting Services)
  Después de definir un conjunto de datos, puede comenzar a diseñar el diseño. El diseño del informe se crea arrastrando y colocando en la superficie de diseño regiones de datos, cuadros de texto, imágenes y otros elementos que se desean incluir en el informe.  
  
 Los elementos que contienen filas de datos repetidas procedentes de conjuntos de datos subyacentes se denominan *regiones de datos*. Un informe básico solo contendrá una región de datos, pero puede agregar más si, por ejemplo, desea agregar un gráfico al informe de tabla. Después de agregar una región de datos, puede agregar campos a la misma.  
  
### <a name="to-add-a-table-data-region-and-fields-to-a-report-layout"></a>Para agregar una región de datos de tabla y campos a un diseño de informe  
  
1.  En el **Cuadro de herramientas**, haga clic en **Tabla**y, después, haga clic en la superficie de diseño y arrastre el mouse. El Diseñador de informes dibuja una región de datos de tabla con tres columnas en el centro de la superficie de diseño.  
  
    > [!NOTE]  
    >  El **Cuadro de herramientas** puede aparecer como una pestaña a la izquierda del panel **Datos de informe** . Para abrir el **Cuadro de herramientas**, pase el puntero por encima de la pestaña **Cuadro de herramientas** . Si el **Cuadro de herramientas** no está visible, en el menú **Ver**, haga clic en **Cuadro de herramientas**.  
  
2.  En el **datos de informe** panel, expanda el **AdventureWorksDataset** conjunto de datos para mostrar los campos.  
  
3.  Arrastre el campo Date desde el **datos de informe** panel a la primera columna en la tabla.  
  
     Al colocar el campo en la primera columna, suceden dos cosas. En primer lugar, la celda de datos mostrará el nombre del campo, que se conoce como la *expresión de campo*, entre corchetes: `[Date]`. En segundo lugar, se agrega automáticamente un valor de encabezado de columna a la fila Encabezado, inmediatamente encima de la expresión de campo. De forma predeterminada, la columna tiene el nombre del campo. Puede seleccionar el texto de la fila Encabezado y escribir un nuevo nombre.  
  
4.  Arrastre el campo Order desde el **datos de informe** panel a la segunda columna de la tabla.  
  
5.  Arrastre el campo Product desde el **datos de informe** panel a la tercera columna de la tabla.  
  
6.  Arrastre el campo Qty hasta el borde derecho de la tercera columna hasta que obtenga un cursor vertical y el puntero del mouse tenga un signo más [+]. Cuando suelte el botón, se creará una cuarta columna para `[Qty]`.  
  
7.  Agregue el campo LineTotal de la misma manera, creando una quinta columna.  
  
    > [!NOTE]  
    >  El encabezado de columna es Line Total. El Diseñador de informes crea automáticamente un nombre descriptivo para la columna, para lo cual, divide LineTotal en dos palabras.  
  
     En el diagrama siguiente se muestra una región de datos de tabla rellenada con estos campos: Date, Order, Product, Qty y LineTotal.  
  
     ![Diseño, tabla con fila de encabezado y fila de detalle](../../2014/tutorials/media/rs-basictabledetailsdesign.gif "diseño, tabla con fila de encabezado y fila de detalles")  
  
## <a name="preview-your-report"></a>Obtener una vista previa del informe  
 Al obtener una vista previa de un informe, se puede ver el informe representado sin tener que publicarlo antes en un servidor de informes. Es probable que desee obtener frecuentemente una vista previa de un informe durante su diseño. Al obtener la vista previa del informe, también se ejecutará la validación en el diseño y las conexiones de datos de modo que pueda corregir los errores y los problemas antes de publicar el informe en un servidor de informes.  
  
#### <a name="to-preview-a-report"></a>Para obtener una vista previa de un informe  
  
-   Haga clic en la pestaña **Vista previa** . El Diseñador de informes ejecuta el informe y lo muestra en la Vista previa.  
  
     El diagrama siguiente muestra parte del informe en la Vista previa.  
  
     ![Vista previa, filas de detalle de la tabla con 5 columnas](../../2014/tutorials/media/rs-basictabledetailspreview.gif "Vista previa, filas de detalle de la tabla con 5 columnas")  
  
     Observe que la moneda (en la columna de Line Total) tiene seis posiciones decimales, y que la fecha incluye una marca de tiempo. En la lección siguiente corregirá ese formato.  
  
> [!NOTE]  
>  En el menú **Archivo** , haga clic en **Guardar todo** para guardar el informe.  
  
## <a name="next-steps"></a>Pasos siguientes  
 Ha agregado correctamente una región de datos de tabla al informe, ha agregado campos a la región de datos y ha obtenido una vista previa del informe. A continuación, dará formato a los encabezados de columna y a los valores de fecha y de moneda. Vea [Lección 5: Aplicar formato a un informe &#40;Reporting Services&#41;](../reporting-services/lesson-5-formatting-a-report-reporting-services.md).  
  
## <a name="see-also"></a>Vea también  
 [Tablas &#40;Generador de informes y SSRS&#41;](report-design/tables-report-builder-and-ssrs.md)   
 [Colección Campos del conjunto de datos &#40;Generador de informes y SSRS&#41;](report-data/dataset-fields-collection-report-builder-and-ssrs.md)  
  
  
