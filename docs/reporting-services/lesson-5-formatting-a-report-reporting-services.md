---
title: 'Lección 5: Aplicación de formato a un informe (Reporting Services) | Microsoft Docs'
ms.date: 05/23/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: ae46efa9-6e04-48ec-afb4-5a2314dcb05a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 1c5a41b39b5c22c05ac4b13a9e57606110b60a2b
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/15/2019
ms.locfileid: "56291113"
---
# <a name="lesson-5-formatting-a-report-reporting-services"></a>Lección 5: Aplicación de formato a un informe (Reporting Services)
Ahora que ha agregado una región de datos y algunos campos al informe Sales Orders, puede dar formato a los campos de moneda y de fecha, así como a los encabezados de columna.  
  
## <a name="bkmk_format_date"></a>Dar formato a la fecha  
En el campo Date, se muestra información de fecha y hora de manera predeterminada. Puede darle formato para mostrar solo la fecha.  
  
#### <a name="to-format-a-date-field"></a>Para dar formato a un campo de fecha  
  
1.  Haga clic en la pestaña **Diseño** .  
  
2.  Haga clic con el botón derecho en la celda con la expresión de campo `[Date]` y, después, haga clic en **Propiedades de cuadro de texto**.  
  
3.  Haga clic en **Número**y luego, en el campo **Categoría** , haga clic en **Fecha**.  
  
4.  En el cuadro **Tipo** , seleccione **January 31, 2000**.  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  Obtenga una vista previa del informe para ver el cambio en el campo `[Date]` y, después, vuelva a cambiar a la vista de diseño.  
  
## <a name="bkmk_format_currency"></a>Dar formato a la moneda  
El campo **LineTotal** muestra un número general. Aplíquele el formato adecuado para mostrar el número como moneda.  
  
#### <a name="to-format-a-currency-field"></a>Para dar formato a un campo de moneda  
  
1.  Haga clic con el botón derecho en la celda con la expresión de campo `[LineTotal]` y, después, haga clic en **Propiedades de cuadro de texto**.  
  
2.  Haga clic en **Número**y, en el campo **Categoría** , seleccione **Moneda**.  
  
3.  Si la configuración regional es Inglés (Estados Unidos), los valores predeterminados deberían ser:  
  
    -   **Decimales: 2**  
  
    -   **Números negativos: ($12345.00)**  
  
    -   **Símbolo: $ Inglés (Estados Unidos)**  
  
4.  Seleccione **Usar separador de miles (.)**.  
  
    Si el texto de ejemplo es:**$12,345.00**, la configuración es correcta.  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  Obtenga una vista previa del informe para ver el cambio en el campo `[LineTotal]` y, después, vuelva a cambiar a la vista de diseño.  
  
## <a name="bkmk_change_textstyle"></a>Cambiar el estilo de texto y los anchos de columna  
También puede cambiar el formato de la fila de encabezado para diferenciarlo de las filas de datos del informe. Por último, ajustará el ancho de las columnas.  
  
#### <a name="to-format-header-rows-and-table-columns"></a>Para dar formato a las filas de encabezado y las columnas de tabla  
  
1.  Haga clic en la tabla para que los identificadores de columna y de fila aparezcan encima y al lado de la tabla. Las barras grises situadas en la parte superior y en el lado de la tabla son los identificadores de fila y de columna.  
       
  
2.  Sitúe el cursor en la línea que hay entre los controladores de columna para que cambie a una flecha doble. Arrastre las columnas hasta que tengan el tamaño deseado.
 ![rs_BasicTableDetailsDesign](../reporting-services/media/rs-basictabledetailsdesign.png)   
  
3.  Seleccione la fila que contiene las etiquetas de los encabezados de columna y, en el menú **Formato** , seleccione **Fuente** y, a continuación, haga clic en **Negrita**.  
  
4.  Haga clic en la pestaña **Vista previa** para obtener la vista previa del informe. Debe tener el siguiente aspecto:  
  
    ![Vista previa de la tabla con encabezados de columna en negrita](../reporting-services/media/rs-basictabledetailsformattedpreview.png "Vista previa de la tabla con encabezados de columna en negrita")  
  
5.  En el menú **Archivo** , haga clic en **Guardar todo** para guardar el informe.  
  
## <a name="next-steps"></a>Next Steps  
Ha aplicado formato correctamente a los encabezados de columna y los valores de moneda y fecha. A continuación, agregará características de agrupación y totales al informe. Consulte [Lección 6: Agregar grupos y totales &#40;Reporting Services&#41;](../reporting-services/lesson-6-adding-grouping-and-totals-reporting-services.md)  
  
## <a name="see-also"></a>Consulte también  
[Aplicar formato a números y fechas &#40;Generador de informes y SSRS&#41;](../reporting-services/report-design/formatting-numbers-and-dates-report-builder-and-ssrs.md)  
[Comportamientos de la representación &#40;Generador de informes y SSRS&#41;](../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)  
  
  
  

