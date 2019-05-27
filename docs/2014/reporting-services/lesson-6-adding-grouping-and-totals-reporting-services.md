---
title: 'Lección 6: Agregar grupos y totales (Reporting Services) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: e3d61228-2aa4-42cc-955e-602dbf3406a7
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 5607dfb046e7f50eb3a015e1f4f13711256435a8
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66108411"
---
# <a name="lesson-6-adding-grouping-and-totals-reporting-services"></a>Lección 6: Agregar grupos y totales (Reporting Services)
  Agregue grupos y totales al informe para organizar y resumir los datos.  
  
 Para obtener información sobre cómo agregar totales acumulativos a informes, vea: [Agregar totales a los informes de Reporting Services (SSRS)](https://www.tutorialgateway.org/add-total-and-subtotal-to-ssrs-report/).  
  
 **En este tema:**  
  
-   [Para agrupar los datos en un informe](#bkmk_groupdata)  
  
-   [Para agregar totales a un informe](#bkmk_addtotals)  
  
-   [Para agregar un total diario a un informe](#bkmk_adddailytotal)  
  
-   [Para agregar un total general a un informe](#bkmk_addgrandtotal)  
  
-   [Para publicar el informe en el servidor de informes (opcional)](#bkmk_publishreport)  
  
##  <a name="bkmk_groupdata"></a> Para agrupar los datos en un informe  
  
1.  Haga clic en la pestaña **Diseño** .  
  
2.  Si no ve el panel **Grupos de filas** , haga clic con el botón secundario en la superficie de diseño y haga clic en **ver** y en **Agrupar**.  
  
3.  En el panel **Datos de informe**, arrastre el campo `Date` hasta el panel **Grupos de filas**. Sitúelo encima de la fila denominada **(Details)**.  
  
     Observe que el identificador de fila ahora tiene un corchete para mostrar un grupo. Ahora, la tabla también tiene dos columnas Date, una de ellas en uno de los dos extremos de una línea de puntos vertical.  
  
     ![](../../2014/tutorials/media/rs-basictablegroups1design.gif "rs_BasicTableGroups1Design")  
  
4.  En el panel **Datos de informe**, arrastre el campo `Order` hasta el panel **Grupos de filas**. Sitúelo debajo de Date y encima de **(Details)**.  
  
     Observe que el identificador de fila ahora tiene dos corchetes para mostrar dos grupos. La tabla tiene ahora dos `Order` columnas, demasiado.  
  
5.  Eliminar las columnas de fecha y pedido originales a la **derecho** de la línea doble. Esta acción quita los valores de este registro para que solo se muestre el valor de grupo. Seleccione los identificadores de las dos columnas y haga clic con el botón derecho en **Eliminar columnas**.  
  
     ![Seleccionar columnas para eliminar](../../2014/tutorials/media/rs-basictablegroupsdeletecols.gif "Seleccionar columnas para eliminar")  
  
     Puede volver a dar formato a los encabezados de columna y a la fecha.  
  
6.  Cambie a la pestaña **Vista previa** para obtener la vista previa del informe. El aspecto deberá ser parecido al de la ilustración siguiente:  
  
     ![Tabla agrupada por fecha y después por pedido](../../2014/tutorials/media/rs-basictablegroupspreview.gif "Tabla agrupada por fecha y después por pedido")  
  
##  <a name="bkmk_addtotals"></a> Para agregar totales a un informe  
  
1.  Cambie a la vista de diseño.  
  
2.  Haga clic con el botón derecho en la celda de la región de datos que contiene el campo `[LineTotal]`y haga clic en **Agregar total**.  
  
     Esto agrega una fila con la suma de los importes de los pedidos.  
  
3.  Haga clic con el botón derecho en la celda que contiene el campo `[Qty]`y haga clic en **Agregar total**.  
  
     Esto agrega la suma de los importes de los pedidos a la fila de totales.  
  
4.  En la celda vacía situada a la izquierda de `Sum[Qty]`, escriba la etiqueta "**Order Total**".  
  
5.  Puede agregar un color de fondo a la fila de totales. Seleccione las dos celdas que contienen las sumas y la celda con la etiqueta.  
  
6.  En el menú **Formato** , haga clic en **Color de fondo**y, a continuación, haga clic en **Gris claro**y en **Aceptar**.  
  
     ![Vista de diseño: tabla básica con total de pedidos](../../2014/tutorials/media/rs-basictablesumlinetotaldesign.gif "Vista de diseño: tabla básica con total general")  
  
##  <a name="bkmk_adddailytotal"></a> Para agregar un total diario a un informe  
  
1.  Haga clic en la celda Order, apunte a **agregar Total**y haga clic en **después**.  
  
     Esto agrega una nueva fila que contiene las sumas de la cantidad y los importes diarios, así como la etiqueta "**Total**" en la columna Order.  
  
2.  Escriba la palabra **Daily** delante de la palabra **Total** en la misma celda, de modo que se lea **Daily Total**.  
  
3.  Seleccione la celda **Daily Total** , las dos celdas **Sum** y la celda que queda vacía entre ellas.  
  
4.  En el menú **Formato** , haga clic en **Color de fondo**, en **Anaranjado**y en **Aceptar**.  
  
     ![](../../2014/tutorials/media/rs-basictablesumdaytotaldesign.gif "rs_BasicTableSumDayTotalDesign")  
  
##  <a name="bkmk_addgrandtotal"></a> Para agregar un total general a un informe  
  
1.  Haga clic con el botón derecho en la celda Date, seleccione **Agregar total**y, luego, haga clic en **Después**.  
  
     Esto agrega una nueva fila que contiene las sumas de las cantidades y dólares para todo el informe y el **Total** etiquetar en el `Date` columna.  
  
2.  Escriba la palabra **Grand** delante de la palabra **Total** en la misma celda, de modo que se lea **Grand Total**.  
  
3.  Seleccione la celda **Grand Total** , las dos celdas **Sum** y las celdas que quedan vacías entre ellas.  
  
4.  En el menú **Formato** , haga clic en **Color de fondo**y, a continuación, haga clic en **Azul claro**y en **Aceptar**.  
  
     ![Vista de diseño: total general en tabla básica](../../2014/tutorials/media/rs-basictablesumgrandtotaldesign.gif "Vista de diseño: total general en la tabla básica")  
  
5.  Haga clic en Vista previa.  
  
     La última página debe tener un aspecto similar a este:  
  
     ![Vista previa: tabla básica con total general](../../2014/tutorials/media/rs-basictablesumgrandtotalpreview.gif "Vista previa: tabla básica con total general")  
  
##  <a name="bkmk_publishreport"></a> Para publicar el informe en el servidor de informes (opcional)  
  
1.  Un paso opcional es publicar el informe completado en el servidor de informes en modo nativo de modo que pueda ver el informe en el Administrador de informes.  
  
2.  En la barra de herramientas, haga clic en **Proyecto** y, a continuación, haga clic en **tutorial Propiedades...**.  
  
3.  En el **TargetServerURL** escriba el nombre del nombre del servidor de informes, por ejemplo **http://\<servername > / reportserver**  
  
4.  Haga clic en **Aceptar**.  
  
5.  En la barra de herramientas, haga clic en **Generar** y, a continuación, haga clic en **Tutorial de implementación**.  
  
     Si ve un mensaje similar al siguiente en la ventana de salida, indica que la implementación se realiza correctamente.  
  
    > ---Compilación iniciada: Proyecto: tutorial, configuración: Depurar---omitiendo 'Sales Orders.rdl'. Elemento está actualizado. Compilación completa--0 errores, 0 advertencias---implementar iniciada: Proyecto: tutorial, configuración: Depuración---implementar a http://\<nombre del servidor > / /reportserverdeploying report '/ tutorial/Sales Orders'. Implementación completa--0 errores, 0 advertencias === compilar: 1 correctos o actualizados, 0 incorrectos, 0 omitidos === implementar: 1 correctos, 0 incorrectos, 0 omitidos ===  
  
     Si aparece un mensaje de error similar al siguiente, compruebe que dispone de permisos en el servidor de informes y que ha iniciado [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] con privilegios de administrador.  
  
    > "Los permisos concedidos al usuario ' XXXXXXXX\\< su nombre de usuario\>' son insuficientes para realizar esta operación"  
  
6.  Inicie el Administrador de informes con privilegios de administrador, por ejemplo, haga clic con el botón secundario en el icono para Internet Explorer y haga clic en **Ejecutar como administrador**.  
  
     Busque la dirección URL del Administrador de informes, por ejemplo: `http://<server name>/reports`.  
  
7.  Busque la carpeta que contiene el informe y haga clic en el nombre del informe `Sales Orders` para verlo representado en el explorador.  
  
## <a name="next-steps"></a>Pasos siguientes  
 Ha completado correctamente el tutorial Crear un informe de tabla básico.  
  
## <a name="see-also"></a>Vea también  
 [Filtrar, agrupar y ordenar datos &#40;Generador de informes y SSRS&#41;](report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)  
  
  
