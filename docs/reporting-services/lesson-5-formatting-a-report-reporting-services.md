---
title: 'Lección 5: Aplicar formato a un informe (Reporting Services) | Microsoft Docs'
ms.date: 04/29/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: ae46efa9-6e04-48ec-afb4-5a2314dcb05a
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: a8bf8b6814f7989a904507cd89fbea397b8b6930
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "65105926"
---
# <a name="lesson-5-formatting-a-report-reporting-services"></a>Lección 5: Aplicar formato a un informe (Reporting Services)

Ahora que ha agregado una región de datos y algunos campos al informe Sales Orders, puede dar formato a los campos de moneda y de fecha, así como a los encabezados de columna.

## <a name="format-the-date"></a><a name="bkmk_format_date"></a>Dar formato a la fecha

La expresión del campo Date muestra información de fecha y hora de manera predeterminada. Puede darle formato para mostrar solo la fecha.

1. Seleccione la pestaña **Diseño**.
2. Haga clic con el botón derecho en la celda con la expresión de campo `[Date]` y, después, seleccione **Propiedades de cuadro de texto**.
3. Seleccione **Número**y, a continuación, en el campo **Categoría**, seleccione **Fecha**.
4. En el cuadro **Tipo** , seleccione **January 31, 2000**.
5. Seleccione **Aceptar** para aplicar el formato.
6. Obtenga una vista previa del informe para ver el cambio de formato del campo `[Date]` y, después, vuelva a cambiar a la vista de diseño.

## <a name="format-the-currency"></a><a name="bkmk_format_currency"></a>Dar formato a la moneda

La expresión del campo LineTotal muestra un número general. Puede aplicarle formato para mostrar el número como moneda.

1. Haga clic con el botón derecho en la celda con la expresión `[LineTotal]` y, después, seleccione **Propiedades de cuadro de texto**.
2. Seleccione **Número** en el cuadro de lista de la columna del extremo izquierdo, y **Moneda** en el cuadro de lista **Categoría**.
3. Si la configuración regional es Inglés (Estados Unidos), los valores predeterminados del cuadro de lista **Tipo** deberían ser:
    - **Decimales: 2**
    - **Números negativos: ($12345.00)**
    - **Símbolo: $ Inglés (Estados Unidos)**
4. Seleccione **Usar separador de miles (.)** . SI en el texto del ejemplo se muestra **$12,345.00**, la configuración es correcta.
5. Seleccione **Aceptar** para aplicar el formato.
6. Obtenga una vista previa del informe para ver el cambio de la columna de la expresión `[LineTotal]` y, después, vuelva a cambiar a la vista de diseño.  

## <a name="change-text-style-and-column-widths"></a><a name="bkmk_change_textstyle"></a>Cambiar el estilo de texto y los anchos de columna

Puede agregar otro formato al informe; para ello, resalte la fila de encabezado y ajuste los anchos de las columnas de datos.

### <a name="to-format-header-rows-and-table-columns"></a>Para dar formato a las filas de encabezado y las columnas de tabla

1. Seleccione la tabla para que los identificadores de columna y de fila aparezcan encima y al lado de la tabla. Las barras grises situadas en la parte superior y en el lado de la tabla son los identificadores de fila y de columna.

2. Sitúe el cursor en la línea que hay entre los controladores de columna para que cambie a una flecha doble. Arrastre las columnas hasta que tengan el tamaño deseado.
    ![rs_BasicTableDetailsDesign](media/rs-basictabledetailsdesign.png)

3. Seleccione la fila que contiene las etiquetas de los encabezados de columna y, en el menú **Formato**, seleccione **Fuente** > **Negrita**.

4. Obtenga una vista previa del informe. Debe mostrarse como sigue:

    ![Vista previa de la tabla con encabezados de columna en negrita](media/rs-basictabledetailsformattedpreview.png "Vista previa de la tabla con encabezados de columna en negrita")  

5. En el menú **Archivo**, seleccione **Guardar todo** para guardar el informe.

## <a name="next-steps"></a>Pasos siguientes

En esta lección, ha aplicado el formato correcto a los encabezados de columna y a las expresiones de los campos. A continuación, va a agregar grupos y totales al informe. Continúe con la [Lección 6: Agregar grupos y totales &#40;Reporting Services&#41;](lesson-6-adding-grouping-and-totals-reporting-services.md).

## <a name="see-also"></a>Consulte también

[Aplicar formato a números y fechas &#40;Generador de informes y SSRS&#41;](report-design/formatting-numbers-and-dates-report-builder-and-ssrs.md)
[Comportamientos de la representación &#40;Generador de informes y SSRS&#41;](report-design/rendering-behaviors-report-builder-and-ssrs.md)
