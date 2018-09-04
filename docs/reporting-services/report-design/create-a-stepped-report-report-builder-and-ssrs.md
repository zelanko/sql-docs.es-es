---
title: Crear un informe escalonado (Generador de informes y SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.suite: pro-bi
ms.topic: conceptual
ms.assetid: 5933c4f0-c713-4ecb-b521-ff46c9c63fff
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 92a07f432bccc41b6f8e6ff301c906227521fb5a
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/30/2018
ms.locfileid: "43271953"
---
# <a name="create-a-stepped-report-report-builder-and-ssrs"></a>Crear un informe escalonado (Generador de informes y SSRS)
Un informe escalonado es un tipo de informe paginado de  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] donde se muestran filas de detalles o grupos secundarios con una sangría debajo de un grupo primario en la misma columna, como se muestra en el ejemplo siguiente:  
  
 ![Informe escalonado representado](../../reporting-services/report-design/media/steppedreportrendered.gif "Informe escalonado representado")  
  
 Los informes de tabla tradicionales sitúan el grupo primario en una columna adyacente del informe. La nueva región de datos tablix permite agregar un grupo y filas de detalles o grupos secundarios a la misma columna. Para diferenciar las filas de grupos de las filas de detalles o grupos secundarios, puede aplicar un formato, como el color de fuente, o puede aplicar una sangría a las filas de detalles.  
  
 Los procedimientos de este tema le muestran cómo crear manualmente un informe escalonado, pero también puede usar el asistente para nuevas tablas y matrices. Proporciona el diseño para los informes escalonados, haciendo fácil crearlos. Después de completar el asistente, puede mejorar aún más el informe.  
  
> [!NOTE]  
>  El asistente solamente está disponible en el Generador de informes.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-create-a-stepped-report"></a>Para crear un informe escalonado  
  
1.  Cree un informe de tabla. Por ejemplo, inserte una región de datos tablix y agregue campos a la fila de datos.  
  
2.  Agregue un grupo primario al informe.  
  
    1.  Haga clic en cualquier lugar de la tabla para seleccionarla. El panel Agrupación muestra el grupo de detalles en el panel Grupos de fila.  
  
    2.  En el panel de agrupación, haga clic con el botón derecho en el grupo de detalles, seleccione **Agregar grupo**y, después, haga clic en **Grupo primario**.  
  
    3.  En el cuadro de diálogo **Grupo de Tablix** , especifique un nombre para el grupo y escriba o seleccione una expresión de grupo en la lista desplegable. La lista desplegable muestra las expresiones de campo simples que están disponibles en el panel Datos de informe. Por ejemplo, [PostalCode] es una expresión de campo simple para el campo PostalCode en un conjunto de datos.  
  
    4.  Seleccione **Agregar encabezado de grupo**. Esta opción agrega una fila estática encima del grupo para la etiqueta y los totales de grupo. Del mismo modo, puede seleccionar **Agregar pie de grupo** para agregar una fila estática debajo del grupo. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Ahora ya tiene un informe tabular básico. Cuando se represente, verá una columna con el valor de instancia de grupo y una o varias columnas con datos de detalles agrupados. En la siguiente ilustración se muestra el aspecto que podría tener la región de datos en la superficie de diseño.  
  
     ![Región de datos de tabla con grupo](../../reporting-services/report-design/media/tabledataregionwithgroup.gif "Región de datos de tabla con grupo")  
  
     En la siguiente ilustración se muestra el aspecto que podría tener la región de datos representada al visualizar el informe.  
  
     ![Informe agrupado representado](../../reporting-services/report-design/media/tablereportrendered.gif "Informe agrupado representado")  
  
3.  En un informe escalonado, no es necesaria la primera columna que muestra la instancia de grupo. En su lugar, copie el valor en la celda de encabezado de grupo, elimine la columna de grupo y pegue el primer cuadro de texto en la fila de encabezado de grupo. Para quitar la columna de grupo, haga clic con el botón derecho en la columna o celda de grupo y, después, haga clic en **Eliminar columnas**. En la siguiente ilustración se muestra el aspecto que podría tener la región de datos en la superficie de diseño.  
  
     ![Región de datos con fila de encabezado de grupo](../../reporting-services/report-design/media/tabledataregiongroupheader.gif "Región de datos con fila de encabezado de grupo")  
  
4.  Para aplicar una sangría a las filas de detalles situadas debajo de la fila de encabezado de grupo en la misma columna, cambie el relleno de la celda de datos de detalles.  
  
    1.  Seleccione la celda con el campo detallado a la que desea aplicar la sangría. Aparecerán las propiedades del cuadro de texto para dicha celda en el panel de propiedades.  
  
    2.  En el panel de propiedades, debajo de **Alineación**, expanda las propiedades para **Relleno**.  
  
    3.  Para **Izquierda**, escriba un nuevo valor de relleno como, por ejemplo, **.5in**. El relleno aplica una sangría al texto de la celda según el valor especificado. El valor de relleno predeterminado es 2 puntos. Los valores válidos para las propiedades de relleno son cero o un número positivo, seguido de un designador de tamaño.  
  
         Los designadores de tamaño son:  
  
        |||  
        |-|-|  
        |**in**|Pulgadas (1 pulgada = 2,54 centímetros)|  
        |**cm**|Centímetros|  
        |**mm**|Milímetros|  
        |**pt**|Puntos (1 punto = 1/72 pulgada)|  
        |**pc**|Picas (1 pica = 12 puntos)|  
  
     La región de datos tendrá un aspecto similar al siguiente:  
  
     ![Región de datos para informe escalonado](../../reporting-services/report-design/media/steppedreportdataregion.gif "Región de datos para informe escalonado")  
  
     **Región de datos para el diseño del informe escalonado**  
  
     En la pestaña **Inicio** , haga clic en **Ejecutar**. El informe muestra el grupo con niveles de sangría para los valores de grupo secundario.  
  
## <a name="to-create-a-stepped-report-with-multiple-groups"></a>Para crear un informe escalonado con varios grupos  
  
1.  Cree un informe tal y como se describe en el procedimiento anterior.  
  
2.  Agregue grupos adicionales al informe.  
  
    1.  En el panel Grupos de filas, haga clic con el botón derecho en el grupo, haga clic en **Agregar grupo**y, después, elija el tipo de grupo que quiera agregar.  
  
        > [!NOTE]  
        >  Existen varias formas de agregar grupos a una región de datos. Para más información, vea [Agregar o eliminar un grupo en una región de datos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md).  
  
    2.  En el cuadro de diálogo **Grupo de Tablix** , escriba un nombre.  
  
    3.  En **Expresión de grupo**, escriba una expresión o seleccione un campo de conjunto de datos por el que realizar la agrupación. Para crear una expresión, haga clic en el botón de expresión (**fx**) para abrir el cuadro de diálogo **Expresión** .  
  
    4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
3.  Cambie el relleno para la celda que muestra los datos del grupo.  
  
## <a name="see-also"></a>Ver también  
 [Encabezados y pies de página &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/page-headers-and-footers-report-builder-and-ssrs.md)   
 [Aplicar formato a los elementos de informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/formatting-report-items-report-builder-and-ssrs.md)   
 [Región de datos Tablix &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/tablix-data-region-report-builder-and-ssrs.md)   
 [Tablas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/tables-report-builder-and-ssrs.md)   
 [Matrices &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/create-a-matrix-report-builder-and-ssrs.md)   
 [Listas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [Tablas, matrices y listas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
