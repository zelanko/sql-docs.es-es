---
title: 'Tutorial: Agregar un gráfico de barras a un informe (Generador de informes) | Microsoft Docs'
ms.custom: ''
ms.date: 06/15/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.component: reporting-services
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 6956ebd6-0217-4087-a4fa-5cc1c3804691
caps.latest.revision: 14
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 8ef72373f91b9104c8ff83f6d1d9b012b283df3d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "33036252"
---
# <a name="tutorial-add-a-bar-chart-to-your-report-report-builder"></a>Tutorial: Agregar un gráfico de barras a un informe (Generador de informes)
En este tutorial, usará un asistente en [!INCLUDE[ssRBnoversion_md](../includes/ssrbnoversion-md.md)] para crear un gráfico de barras en un informe paginado de [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] . Después, agregará un filtro y mejorará el gráfico. 

Un gráfico de barras muestra los datos de categoría horizontalmente. Esto puede ayudar a:  
  
-   Mejorar la legibilidad de los nombres de categoría largos.  
-   Mejorar la comprensión de las fechas u horas representadas mediante valores.   
-   Comparar el valor relativo de varias series.  
  
La siguiente ilustración muestra el gráfico de barras que creará, con ventas para 2014 y 2015, para los cinco mejores vendedores, de más a menos ventas en 2015.  
  
![generador-informes-gráfico-de-barras](../reporting-services/media/report-builder-bar-chart.png) 
  
 
> [!NOTE]  
> En este tutorial, los pasos del asistente se encuentran reunidos en un único procedimiento. Para obtener instrucciones paso a paso sobre cómo ir hasta un servidor de informes, crear un conjunto de datos y elegir un origen de datos, vea el primer tutorial de esta serie: [Tutorial: Crear un informe de tabla básico &#40;Generador de informes&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md).  
  
Tiempo estimado para completar este tutorial: 15 minutos.  
  
## <a name="requirements"></a>Requisitos  
Para obtener más información sobre los requisitos, consulte [Requisitos previos para los tutoriales &#40;Generador de informes&#41;](../reporting-services/prerequisites-for-tutorials-report-builder.md).  
  
## <a name="Chart"></a>1. Crear un informe de gráfico a partir del Asistente para gráficos  
En el que puede crear un conjunto de datos incrustado, elegir un origen de datos compartido y crear un gráfico de barras con el Asistente para gráficos.  
  
> [!NOTE]  
> En este tutorial, la consulta contiene los valores de datos, de forma que no necesita un origen de datos externo. Esto hace que la consulta requiera bastante tiempo. En un entorno empresarial, la consulta no contendría los datos. Esto es solo con fines de aprendizaje.  
  
1.  [Inicie el Generador de informes](../reporting-services/report-builder/start-report-builder.md) desde el portal web de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] o el servidor de informes en modo integrado de SharePoint o bien desde su equipo.  
  
     Aparecerá el cuadro de diálogo **Introducción** .  
  
     ![Introducción al Generador de informes](../reporting-services/media/rb-getstarted.png "Introducción al Generador de informes")  
  
     Si no ve el cuadro de diálogo **Introducción** , haga clic en **Archivo** >**Nuevo**. El cuadro de diálogo **Nuevo informe o conjunto de datos** tiene prácticamente el mismo contenido que el cuadro de diálogo **Introducción** . 
      
2.  En el panel de la izquierda, compruebe que está seleccionada la opción **Nuevo informe** .  
  
3.  En el panel derecho, haga clic en **Asistente para gráficos**.  
  
4.  En la página **Elegir un conjunto de datos** , haga clic en **Crear un conjunto de datos**y, después, haga clic en **Siguiente**.  
  
5.  En la página **Elegir una conexión a un origen de datos** , seleccione un origen de datos existente o vaya al servidor de informes y seleccione un origen de datos, y después haga clic en **Siguiente**. Puede que necesite escribir un nombre de usuario y contraseña.  
  
    > [!NOTE]  
    > El origen de datos que elija no importa, con tal de que tenga los permisos adecuados. No está recibiendo datos del origen de datos. Para obtener más información, consulte [Maneras alternativas de obtener una conexión de datos &#40;Generador de informes&#41;](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md).  
  
6.  En la página **Diseñar una consulta** , haga clic en **Editar como texto**.  
  
7.  Pegue la siguiente consulta en el panel de consulta:  
  
    ```  
    SELECT 'Luis' as FirstName, 'Alverca' as LastName, CAST(170000.00 AS money) AS SalesYear2015, CAST(150000. AS money) AS SalesYear2014  
    UNION SELECT 'Jeffrey' as FirstName, 'Zeng' as LastName, CAST(210000. AS money) AS SalesYear2015, CAST(190000. AS money) AS SalesYear2014  
    UNION SELECT 'Houman' as FirstName, 'Pournasseh' as LastName, CAST(150000. AS money) AS SalesYear2015, CAST(180000. AS money) AS SalesYear2014  
    UNION SELECT 'Robin' as FirstName, 'Wood' as LastName, CAST(75000. AS money) AS SalesYear2015, CAST(175000. AS money) AS SalesYear2014  
    UNION SELECT 'Daniela' as FirstName, 'Guaita' as LastName,  CAST(170000. AS money) AS SalesYear2015, CAST(175000. AS money) AS SalesYear2014  
    UNION SELECT 'John' as FirstName, 'Yokim' as LastName, CAST(160000. AS money) AS SalesYear2015, CAST(195000. AS money) AS SalesYear2014  
    UNION SELECT 'Delphine' as FirstName, 'Ribaute' as LastName, CAST(180000. AS money) AS SalesYear2015, CAST(205000. AS money) AS SalesYear2014  
    UNION SELECT 'Robert' as FirstName, 'Hernady' as LastName, CAST(140000. AS money) AS SalesYear2015, CAST(180000. AS money) AS SalesYear2014  
    UNION SELECT 'Tanja' as FirstName, 'Plate' as LastName, CAST(150000. AS money) AS SalesYear2015, CAST(160000. AS money) AS SalesYear2014  
    UNION SELECT 'David' as FirstName, 'Bradley' as LastName, CAST(210000. AS money) AS SalesYear2015, CAST(180000. AS money) AS SalesYear2014  
    UNION SELECT 'Michal' as FirstName, 'Jaworski' as LastName, CAST(175000. AS money) AS SalesYear2015, CAST(220000. AS money) AS SalesYear2014  
    UNION SELECT 'Chris' as FirstName, 'Ashton' as LastName, CAST(195000. AS money) AS SalesYear2015, CAST(205000. AS money) AS SalesYear2014  
    UNION SELECT 'Pongsiri' as FirstName, 'Hirunyanitiwatna' as LastName, CAST(175000. AS money) AS SalesYear2015, CAST(215000. AS money) AS SalesYear2014  
    UNION SELECT 'Brian' as FirstName, 'Burke' as LastName, CAST(187000. AS money) AS SalesYear2015, CAST(207000. AS money) AS SalesYear2014  
    ```  
  
8.  (Opcional) Haga clic en el botón Ejecutar (**!**) para ver los datos en los que se basará su gráfico.  
  
9. Haga clic en **Siguiente**.  
  
## <a name="ChartType"></a>2. Crear un gráfico de barras  
 
1.  En la página **Elegir un tipo de gráfico** , el gráfico de columnas es el tipo de gráfico predeterminado.  
  
2.  Haga clic en **Barras**y después en **Siguiente**.  
  
    En la página **Organizar campos del gráfico** , hay cuatro campos en el panel **Campos disponibles** : FirstName, LastName, SalesYear2015 y SalesYear2014.  
  
3.  Arrastre LastName hasta el panel Categorías.  
  
4.  Arrastre SalesYear2015 hasta el panel Valores. SalesYear2015 representa la cantidad de ventas de cada vendedor durante el año 2015. El panel Valores muestra `[Sum(SalesYear2015)]` porque el gráfico muestra al agregado para cada producto.  
  
5.  Arrastre SalesYear2014 hasta el panel Valores, debajo de SalesYear2015. SalesYear2014 representa la cantidad de ventas de cada vendedor durante el año 2014.  
  
6.  Haga clic en **Siguiente**.  
  
7.  Haga clic en **Finalizar**.  
  
    El gráfico se agrega a la superficie de diseño. Tenga en cuenta que el nuevo gráfico de barras solo muestra los datos de representación. La leyenda muestra Apellido A, Apellido B, etc., en lugar de nombres de personas, para que se haga idea de qué aspecto tendrá el informe. 
  
9. Haga clic en el gráfico para mostrar las asas del gráfico. Arrastre la esquina inferior derecha del gráfico para aumentar su tamaño. Observe que la superficie de diseño aumenta a medida que realiza la acción de arrastrar. 
  
10. Haga clic en **Ejecutar** para obtener la vista previa del informe.  
  
El gráfico de barras muestras las ventas correspondientes a cada vendedor para los años 2014 y 2015. La longitud de la barra corresponde al total de ventas.  
  
## <a name="AllValues"></a>3. Mostrar todos los nombres en el eje vertical  
De forma predeterminada, solo aparecen algunos de los valores del eje vertical. Puede cambiar el gráfico para mostrar todas las categorías.  
  
1.  Cambie a la vista de diseño del informe.  
  
2.  Haga clic con el botón secundario en el eje vertical y, después, haga clic en **Propiedades del eje vertical**.  
  
3.  En **Rango e intervalo del eje**, en el cuadro **Intervalo** , escriba **1**.  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  Haga clic en **Ejecutar** para obtener la vista previa del informe.  
  
> [!NOTE]  
> Si no se leen los nombres de vendedor en el eje vertical, puede hacer más alto el gráfico o cambiar las opciones de formato para las etiquetas del eje.  
  
### <a name="CategoryExpression"></a>Mostrar Last Name y First Name en el eje vertical  
Puede cambiar la expresión de categoría para incluir para cada vendedor el apellido seguido por el nombre.  
  
1.  Cambie a la vista de diseño del informe.  
  
2.  Haga doble clic en el gráfico para mostrar el panel **Datos del gráfico** .  
  
3.  En el área **Grupos de categorías** , haga clic con el botón secundario en [LastName] y, después, haga clic en **Propiedades del grupo de categorías**.  
  
4.  En Etiqueta, haga clic en el botón de expresión (Fx).  
  
5.  Escriba la siguiente expresión: `=Fields!LastName.Value & ", " & Fields!FirstName.Value`  
  
    Esta expresión concatena el apellido, una coma y el nombre.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  Haga clic en **Ejecutar** para obtener la vista previa del informe.  
  
Si los nombres no aparecen al ejecutar el informe, puede actualizar los datos manualmente. Estando todavía en modo de vista previa, en la pestaña **Ejecutar** en el grupo **Navegación** , haga clic en **Actualizar**.  
  
> [!NOTE]  
> Si no se leen los nombres de vendedor en el eje vertical, puede hacer más alto el gráfico o cambiar las opciones de formato para las etiquetas del eje.  
  
## <a name="Sort"></a>4. Cambiar el criterio de ordenación en el eje vertical  
Al ordenar los datos en un gráfico, está cambiando el orden de valores en el eje de categoría.  
  
1.  Cambie a la vista de diseño del informe.  
  
2.  Haga doble clic en el gráfico para mostrar el panel **Datos del gráfico** .  
  
3.  En el área **Grupos de categorías** , haga clic con el botón secundario en [LastName] y, después, haga clic en **Propiedades del grupo de categorías**.  
  
4.  Haga clic en **Ordenar**. La página **Cambiar opciones de ordenación** muestra una lista de expresiones de ordenación. De forma predeterminada, esta lista tiene una expresión de ordenación que es igual que la expresión de grupo de categorías original.  
  
5.  En **Ordenar por**, haga clic en **[SalesYear2015]**.  
  
6.  en la lista **Ordenar** , seleccione **A a Z** para que los nombres aparezcan en orden de mayor a menor venta de 2015.
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
10. Haga clic en **Ejecutar** para obtener la vista previa del informe.  
  
Los nombres en el eje horizontal están ordenados por ventas de 2015, de mayor a menor, con **Zeng** en la parte superior.  
  
## <a name="Legend"></a>5. Mover la leyenda  
Para mejorar la legibilidad de los valores del gráfico, es posible que le interese mover la leyenda correspondiente. Por ejemplo, en un gráfico de barras, donde las barras se muestran horizontalmente, puede cambiar la posición de la leyenda para que aparezca debajo o encima del área de gráfico. Esto proporciona más espacio horizontal para las barras.  
  
#### <a name="to-display-the-legend-below-the-chart-area-of-a-bar-chart"></a>Para mostrar la leyenda debajo del área de gráfico de un gráfico de barras  
  
1.  Cambie a la vista de diseño del informe.  
  
2.  Haga clic con el botón secundario en la leyenda del gráfico.  
  
3.  Seleccione **Propiedades de la leyenda**.  
  
4.  Para **Posición de la leyenda**, seleccione una posición diferente. Por ejemplo, sitúe la leyenda centrada en la parte inferior.  
  
    Cuando la leyenda se coloca en la parte superior o inferior de un gráfico, su diseño cambia de vertical a horizontal. Puede seleccionar un diseño diferente en la lista desplegable **Diseño** .  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  Haga clic en **Ejecutar** para obtener la vista previa del informe.  
  
## <a name="ChartTitle"></a>6. Titular el gráfico  
  
1.  Cambie a la vista de diseño del informe.  
  
2.  Seleccione las palabras **Título del gráfico** en la parte superior del gráfico y después escriba **Ventas para 2014 y 2015**.  
  
3.  Con el título seleccionado, en el panel Propiedades, cambie **Color** a **Negro** y **Fuente** a **12 pt**. 
  
4.  Haga clic en **Ejecutar** para obtener la vista previa del informe.  
  
## <a name="Horizontal"></a>7. Dar formato al eje horizontal y etiquetarlo  
De forma predeterminada, el eje horizontal muestra los valores en un formato general que se escala automáticamente para ajustarse al tamaño del gráfico. Puede cambiarlo al formato de moneda.  
   
1.  Cambie a la vista de diseño del informe.  
  
2.  Haga clic en el eje horizontal a lo largo de la parte inferior del gráfico para seleccionarlo.  
  
3.  En la pestaña **Inicio** > grupo **Número** > **Moneda**. Las etiquetas del eje horizontal cambian al formato de moneda.  
  
3.  (Opcional) Quite los dígitos decimales. Cerca del botón **Moneda** , haga clic dos veces en el botón **Disminuir decimales** .  
  
4.  Haga clic con el botón secundario en el eje horizontal y, después, haga clic en **Propiedades del eje horizontal**.  
  
5.  En la pestaña **Número** , seleccione **Mostrar valores en miles**.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  

8.  Haga clic con el botón secundario en el eje horizontal y seleccione **Mostrar título del eje**.
  
7.  En el cuadro **Título del eje** , escriba **Ventas en miles** y presione Entrar.  

    >**Nota:** mientras escribe, el cuadro Título del eje aparece en el eje vertical. Pero cuando presione Entrar, pasa al eje horizontal.
  
9. Haga clic en **Ejecutar** para obtener la vista previa del informe.  
  
El informe muestra el importe de ventas en el eje horizontal como moneda en miles, sin dígitos decimales.  
  
## <a name="Filter"></a>8. Agregar un filtro para mostrar cinco valores superiores  
Puede agregar un filtro al gráfico para especificar qué datos del conjunto de datos se van a incluir o excluir del gráfico.   
  
1.  Cambie a la vista de diseño del informe.  
  
2.  Haga doble clic en el gráfico para mostrar el panel **Datos del gráfico** .  
  
3.  En el área **Grupos de categorías** , haga clic con el botón secundario en el campo [LastName] y, después, haga clic en **Propiedades del grupo de categorías**.  
  
4.  Haga clic en **Filtros**. La página **Cambiar filtros** puede mostrar una lista de expresiones de filtro. Esta lista aparece vacía de forma predeterminada.  
  
5.  Haga clic en **Agregar**. Aparece un nuevo filtro en blanco.  
  
6.  En **Expresión**, escriba **[Sum(SalesYear2015)]**. Esto crea la expresión subyacente `=Sum(Fields!SalesYear2015.Value)`, que puede ver si hace clic en el botón **fx** .  
  
7.  Compruebe que el tipo de datos es **Texto**.  
  
8.  En **Operador**, seleccione **Superior N** en la lista desplegable.  
  
9. En **Valor**, escriba la siguiente expresión: **=5**  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
11. Haga clic en **Ejecutar** para obtener la vista previa del informe.  
  
Si no se filtran los resultados al ejecutar el informe, puede actualizar los datos manualmente. En la pestaña **Ejecutar** , en el grupo **Navegación** , haga clic en **Actualizar**.  
  
El gráfico muestra los nombres de los cinco primeros vendedores de los datos de ventas de 2015.  
  
## <a name="Title"></a>9. Agregar un título de informe  
  
1.  En la superficie de diseño, haga clic en **Haga clic para agregar título**.  
  
2.  Escriba **Gráfico de barras de ventas**, presione ENTRAR y después escriba **Cinco primeros vendedores de 2015**, de modo que tenga este aspecto:  
  
    **Gráfico de barras de ventas**  
  
    **Cinco primeros vendedores de 2015**  
  
3.  Seleccione **Gráfico de barras de ventas**y haga clic en el botón **Negrita** .  
  
4.  Seleccione **Cinco primeros vendedores de 2015**y, en la sección **Fuente** de la pestaña **Inicio** , establezca el tamaño de fuente en **10**.  
  
5.  (Opcional) Es posible que necesite hacer más alto el cuadro de texto Título y bajar la parte superior del gráfico de barras, para que quepan las dos líneas de texto.  
  
    Este título aparecerá en la parte superior del informe. Cuando no hay ningún encabezado de página definido, los elementos de la parte superior del cuerpo del informe son equivalentes a un encabezado de informe.  
  
6.  Haga clic en **Ejecutar** para obtener la vista previa del informe.  
  
## <a name="Save"></a>10. Guardar el informe  
  
1.  Cambie a la vista de diseño del informe.  
  
2.  Haga clic en **Archivo** > **Guardar como**.  
  
3.  En **Nombre**, escriba **Gráfico de barras de ventas**.  

    Puede guardarlo en el equipo o en el servidor de informes.
  
4.  Haga clic en **Guardar**.   
  
## <a name="next-steps"></a>Next Steps  
Ha completado correctamente el tutorial Agregar un gráfico de barras al informe. Para obtener más información sobre gráficos, consulte [Gráficos](../reporting-services/report-design/charts-report-builder-and-ssrs.md) y [Gráficos de barras](../reporting-services/report-design/bar-charts-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Ver también  
[Tutoriales del Generador de informes](../reporting-services/report-builder-tutorials.md)  
[Generador de informes en SQL Server 2016](../reporting-services/report-builder/report-builder-in-sql-server-2016.md)  
  

