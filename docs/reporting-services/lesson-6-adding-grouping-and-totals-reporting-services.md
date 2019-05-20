---
title: 'Lección 6: Agregar grupos y totales (Reporting Services) | Microsoft Docs'
ms.date: 04/18/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: e3d61228-2aa4-42cc-955e-602dbf3406a7
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b5b9846a20615cf613dd50752ac63f2669b1e399
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 05/06/2019
ms.locfileid: "65089659"
---
# <a name="lesson-6-adding-grouping-and-totals-reporting-services"></a>Lesson 6: Adding Grouping and Totals (Reporting Services)

En la última lección del tutorial, agregará grupos y totales al informe de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] para organizar y resumir los datos.  

## <a name="to-group-data-in-a-report"></a>Para agrupar datos en un informe

1. Seleccione la pestaña **Diseño**.
2. Si no ve el panel **Grupos de filas**, haga clic con el botón derecho en la superficie de diseño y seleccione **Ver** >**Agrupar**.
3. En el panel **Datos de informe**, arrastre el campo `[Date]` al panel **Grupos de filas**. Sitúelo encima de la fila que se muestra como **= (Detalles)**.

    > [!NOTE]
    > Observe que el identificador de fila ahora tiene un corchete para indicar que se trata de un grupo. La tabla también tiene ahora dos columnas de expresión `[Date]`, una a ambos lados de una línea de puntos vertical.
    >
    >![Grupo de fecha agregado](media/rs-basictablegroups1design.png "Grupo de fecha agregado")
4. En el panel **Datos de informe**, arrastre el campo `[Order]` hasta el panel **Grupos de filas**. Sitúelo debajo de **Date** y encima de **= (Detalles)**.

    ![ssrs_ssdt_addorderfield](media/ssrs-ssdt-addorderfield.png)

    > [!NOTE]
    > Observe que el identificador de fila ahora tiene dos corchetes, ![ssrs_ssdt_rowgroupdoublehandles](media/ssrs-ssdt-rowgroupdoublehandles.png), para indicar dos grupos. La tabla también tiene ahora dos columnas de expresión `[Order]`.

5. Elimine las columnas de expresión `[Date]` y `[Order]` originales situadas a la derecha de la línea doble. Seleccione los identificadores de las dos columnas, haga clic con el botón derecho en la opción **Eliminar columnas** y selecciónela. El Diseñador de informes quita las expresiones de filas individuales, por lo que se muestran solo las expresiones de grupo.

    ![Seleccionar columnas para eliminar](media/rs-basictablegroupsdeletecols.gif "Seleccionar columnas para eliminar")

6. Para dar formato a la nueva columna `[Date]`, haga clic en la celda de la región de datos que contiene la expresión `[Date]` y seleccione **Propiedades del cuadro de texto**.
7. Seleccione **Número** en el cuadro de lista de la columna del extremo izquierdo, y **Fecha** en el cuadro de lista **Categoría**.
8. En el cuadro de lista **Tipo**, seleccione **January 31, 2000**.
9. Seleccione **Aceptar** para aplicar el formato.
10. Vuelva a obtener una vista previa del informe. El aspecto debe ser similar al siguiente:

    ![rs_BasicTableGroupsPreview](media/rs-basictablegroupspreview.png)

## <a name="adding-totals-to-a-report"></a>Adición de totales a un informe

1. Cambie a la vista **Diseño**.
2. Haga clic con el botón derecho en la celda de la región de datos que contiene la expresión `[LineTotal]` y seleccione **Agregar total**. El Diseñador de informes agrega una fila con la suma del importe de cada pedido en dólares.
3. Haga clic con el botón derecho en la celda que contiene el campo `[Qty]`y seleccione **Agregar total**. El Diseñador de informes agrega una suma de la cantidad de cada pedido a la fila de totales.
4. En la celda vacía situada a la izquierda de la celda `Sum[Qty]`, escriba la cadena "Order Total".
5. Puede agregar un color de fondo a la fila de totales. Seleccione las dos celdas que contienen las sumas y la celda con la etiqueta.  
6. En el menú **Formato**, seleccione el cuadrado **Color de fondo** > **Gris claro**.
7. Seleccione **Aceptar** para aplicar el formato.

   ![Vista Diseño: tabla básica con total de pedidos](media/rs-basictablesumlinetotaldesign.gif "Vista Diseño: tabla básica con total de pedidos")

## <a name="add-the-daily-total-to-the-report"></a>Agregar el total diario al informe

1. Haga clic con el botón derecho en la celda de la expresión `[Order]` y seleccione **Agregar total** > **Después**. El Diseñador de informes agrega una nueva fila que contiene las sumas de los valores `[Qty]` y `[Linetotal]` para cada día y la cadena "Total" en la parte inferior de la columna de la expresión `[Order]`.
2. Escriba la palabra “Daily” delante de la palabra "Total" en la misma celda, de modo que se lea "Daily Total".
3. Seleccione la celda y las dos celdas de total adyacentes de la derecha y la celda vacía que se encuentra entre ellas.
4. En el menú **Formato**, seleccione el cuadrado **Color de fondo** > **Naranja**.
5. Seleccione **Aceptar** para aplicar el formato.

   ![Establece el color de fondo en anaranjado](media/rs-basictablesumdaytotaldesign.gif "rs_BasicTableSumDayTotalDesign")

## <a name="add-the-grand-total-to-the-report"></a>Agregar el total general al informe

1. Haga clic con el botón derecho en la celda de la expresión `[Date]` y seleccione **Agregar total** > **Después**. El Diseñador de informes agrega una nueva fila que contiene las sumas de los valores `[Qty]` y `[LineTotal]` para el informe completo y la cadena "Total" en la parte inferior de la columna de la expresión `[Date]`.
2. Escriba la palabra "Grand" delante de la palabra "Total" en la misma celda, de modo que se lea "Grand Total".
3. Seleccione la celda que contiene "Grand Total", las dos celdas de la expresión `Sum()` y las celdas vacías que están entre ellas.
4. En el menú **Formato**, seleccione el cuadrado **Color de fondo** > **Azul claro**.
5. Seleccione **Aceptar** para aplicar el formato.

    ![Vista Diseño: total general en tabla básica](media/rs-basictablesumgrandtotaldesign.gif "Vista Diseño: total general en tabla básica")

## <a name="preview-the-report"></a>Vista previa del informe

Para obtener una vista previa de los cambios de formato, seleccione la pestaña **Vista previa**. En la barra de herramientas **Vista previa**, seleccione el botón **Última página**, que presenta un aspecto similar a ![ssrs_ssdt_viewertoolbar_lastpage](media/ssrs-ssdt-viewertoolbar-lastpage.png). Los resultados deberían mostrarse como sigue:

   ![Vista previa: tabla básica con total general](media/rs-basictablesumgrandtotalpreview.gif "Vista previa: tabla básica con total general")

## <a name="publishing-the-report-to-the-report-server-optional"></a>Publicación del informe en el *servidor de informes* (opcional)

Un paso opcional consiste en publicar el informe completado en el servidor de informes para poder verlo en el portal web.

1. Seleccione el menú **Proyecto** > **Propiedades del tutorial...**
2. En **TargetServerURL**, escriba el nombre del servidor de informes, por ejemplo:
    - `http:/<servername>/reportserver` o
    - `https://localhost/reportserver` funciona si está diseñando el informe en el servidor de informes.

3. Tenga en cuenta que **TargetReportFolder** se llama Tutorial en el nombre del proyecto. El Diseñador de informes implementa el informe en esta carpeta.
4. Seleccione **Aceptar**.
5. Seleccione el menú **Compilar** > **Implementar tutorial**.

    Si ve un mensaje similar al siguiente en la ventana **Salida**, indica que la implementación se realiza correctamente.

    > ------ Compilación iniciada: proyecto: tutorial, configuración: depurar ------  
    > Omitiendo 'Sales Orders.rdl'. El elemento está actualizado.  
    > Generación completa -- 0 errores, 0 advertencias  
    > ------ Operación Implementar iniciada: proyecto: tutorial, configuración: depurar ------  
    > Implementando en `https://[server name]/reportserver`  
    > Implementando el informe '/tutorial/Sales Orders'.  
    > Implementación completa -- 0 errores, 0 advertencias  
    > ========== Compilar: 1 correctos o actualizados, 0 incorrectos, 0 omitidos==========  
    > ========== Implementar: 1 correctos, 0 incorrectos, 0 omitidos==========  

    Si aparece un mensaje de error similar al siguiente, compruebe que dispone de los permisos apropiados en el servidor de informes y que ha iniciado [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] con privilegios de administrador.
    >
    > "Los permisos concedidos al usuario 'XXXXXXXX\\[su nombre de usuario]" no son suficientes para realizar esta operación"

6. Abra un explorador con privilegios de administrador. Por ejemplo, haga clic con el botón derecho en el icono de Internet Explorer y seleccione **Ejecutar como administrador**.
7. Vaya a la dirección URL del portal web.
   - Columnas en la tabla de origen capturadas`https://<server name>/reports`
   - `https://localhost/reports` funciona si está diseñando el informe en el servidor de informes.

8. Seleccione la carpeta Tutorial y, a continuación, seleccione el informe "Sales Orders" para verlo.

    ![ssrs_tutorial_tutorialfolder](media/ssrs-tutorial-tutorialfolder.png)  

Ha completado correctamente el **tutorial Crear un informe de tabla básico**.

## <a name="see-also"></a>Vea también

[Filtrar, agrupar y ordenar datos &#40;Generador de informes y SSRS&#41;](report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)
