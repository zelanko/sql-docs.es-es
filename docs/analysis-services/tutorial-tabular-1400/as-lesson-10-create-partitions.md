---
title: 'Lección tutorial de Analysis Services 10: crear particiones | Documentos de Microsoft'
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile"
ms.openlocfilehash: 8dc8e91271451d3f24df95846f32af8dbd9ca346
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="create-partitions"></a>Crear particiones

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

En esta lección, creará particiones dividir la tabla FactInternetSales en piezas lógicas más pequeñas que se pueden procesar (actualiza) independientemente de otras particiones. De forma predeterminada, cada tabla que se incluye en el modelo tiene una partición, que incluye columnas y filas de la de la tabla. Para la tabla FactInternetSales, queremos dividir los datos por año; una partición para cada uno de los cinco años de la tabla. Cada partición se podrá procesar entonces independientemente. Para obtener más información, consulte [particiones](../tabular-models/partitions-ssas-tabular.md). 
  
Tiempo estimado para completar esta lección: **15 minutos**  
  
## <a name="prerequisites"></a>Requisitos previos  

Este artículo forma parte de un tutorial de modelado tabular, que se debe completar en orden. Antes de realizar las tareas en esta lección, debe haber completado la lección anterior: [lección 9: crear jerarquías](../tutorial-tabular-1400/as-lesson-9-create-hierarchies.md).  
  
## <a name="create-partitions"></a>Crear particiones  
  
#### <a name="to-create-partitions-in-the-factinternetsales-table"></a>Para crear particiones en la tabla FactInternetSales  
  
1.  En el Explorador de modelos tabulares, expanda **tablas**y, a continuación, haga clic en **FactInternetSales** > **particiones**.  
  
2.  En el Administrador de particiones, haga clic en **copia**y, a continuación, cambie el nombre a **FactInternetSales2010**.
  
    Ya que desea que la partición incluya sólo aquellas filas en un período determinado, para el año 2010, debe modificar la expresión de consulta.
  
4.  Haga clic en **diseño** para abrir el Editor de consultas y, a continuación, haga clic en el **FactInternetSales2010** consulta.

5.  En la vista previa, haga clic en la flecha hacia abajo en la **OrderDate** encabezado de columna y, a continuación, haga clic en **filtros de fecha y hora** > **entre**.

    ![como-lesson10--editor de consultas](../tutorial-tabular-1400/media/as-lesson10-query-editor.png)

6.  En el cuadro de diálogo Filtrar filas en **mostrar filas donde: OrderDate**, deje **es posterior o igual a**y, a continuación, en el campo de fecha, escriba **1/1/2010**. Deje el **y** operador seleccionado, a continuación, seleccione **antes**, a continuación, en el campo de fecha, escriba **/1/1/2011**y, a continuación, haga clic en **Aceptar**.

    ![como lesson10-filtro de filas](../tutorial-tabular-1400/media/as-lesson10-filter-rows.png)
    
    Observe en el Editor de consultas, en los pasos aplicados, verá otro paso filtra las filas con nombre. Este filtro consiste en seleccionar sólo las fechas de pedidos de 2010.

8.  Haga clic en **Importar**.

    En el Administrador de particiones, tenga en cuenta que la expresión de consulta ahora tiene una cláusula de filtrado de filas adicional.

    ![consulta como lesson10](../tutorial-tabular-1400/media/as-lesson10-query.png)
  
    Esta instrucción especifica que esta partición debe incluir solo los datos en las filas donde el valor de OrderDate es en el año 2010 tal como se especifica en la cláusula de filtrado de filas.  
  
  
#### <a name="to-create-a-partition-for-the-2011-year"></a>Para crear una partición para el año 2011  
  
1.  En la lista de particiones, haga clic en el **FactInternetSales2010** de partición que creó y, a continuación, haga clic en **copia**.  Cambie el nombre de partición a **FactInternetSales2011**. 

    No es necesario usar el Editor de consultas para crear una nueva cláusula de filtrado de filas. Como ha creado una copia de la consulta para 2010, todo lo que necesita hacer es poner un pequeño cambio en la consulta de 2011.
  
2.  En **expresión de consulta**, en orden para esta partición incluir solo las filas para el año 2011, reemplace los años en la cláusula de filtrado de filas con **2011** y **2012**, respectivamente, al igual que:  
  
    ```  
    let
        Source = #"SQL/localhost;AdventureWorksDW2014",
        dbo_FactInternetSales = Source{[Schema="dbo",Item="FactInternetSales"]}[Data],
        #"Removed Columns" = Table.RemoveColumns(dbo_FactInternetSales,{"OrderDateKey", "DueDateKey", "ShipDateKey"}),
        #"Filtered Rows" = Table.SelectRows(#"Removed Columns", each [OrderDate] >= #datetime(2011, 1, 1, 0, 0, 0) and [OrderDate] < #datetime(2012, 1, 1, 0, 0, 0))
    in
        #"Filtered Rows"
   
    ```  
  
#### <a name="to-create-partitions-for-2012-2013-and-2014"></a>Para crear particiones de 2012, 2013 y 2014.  
  
- Siga los pasos anteriores, la creación de particiones de 2012, 2013 y 2014, cambiar los años en la cláusula de filtrado de filas para incluir sólo las filas correspondientes a ese año. 
  

## <a name="delete-the-factinternetsales-partition"></a>Eliminar la partición FactInternetSales

Ahora que tiene particiones para cada año, puede eliminar la partición FactInternetSales; al elegir todos los procesos cuando el procesamiento de particiones, que impiden que se superponen.

#### <a name="to-delete-the-factinternetsales-partition"></a>Para eliminar la partición FactInternetSales

-  Haga clic en el **FactInternetSales** de partición y, a continuación, haga clic en **eliminar**.



## <a name="process-partitions"></a>Procesar particiones  

En el Administrador de particiones, tenga en cuenta el **procesa última** columna para cada una de las nuevas particiones que ha creado muestra estas particiones nunca se han procesado. Al crear particiones, debe ejecutar una operación procesar particiones o procesar tabla para actualizar los datos de esas particiones.  
  
#### <a name="to-process-the-factinternetsales-partitions"></a>Para procesar las particiones FactInternetSales  
  
1.  Haga clic en **Aceptar** para cerrar el Administrador de partición.  
  
2.  Haga clic en el **FactInternetSales** de tabla, a continuación, haga clic en el **modelo** menú > **proceso** > **procesar particiones**.  
  
3.  En el cuadro de diálogo procesar particiones, compruebe **modo** está establecido en **proceso predeterminado**.  
  
4.  Active la casilla de la columna **Procesar** para cada una de las cinco particiones que ha creado y haga clic en **Aceptar**.  

    ![como-lesson10-proceso-particiones](../tutorial-tabular-1400/media/as-lesson10-process-partitions.png)
  
    Si se le pide las credenciales de suplantación, escriba el nombre de usuario de Windows y la contraseña que especificó en la lección 2.  
  
    Aparece el cuadro de diálogo **Procesamiento de datos** con los detalles del proceso de cada partición. Observe que se ha transferido un número diferente de filas para cada partición. Cada partición incluye solamente las filas del año especificado en la cláusula WHERE en la instrucción SQL. Cuando finalice el procesamiento, continúe y cierre el cuadro de diálogo Procesamiento de datos.  
  
    ![como lesson10-proceso-completo](../tutorial-tabular-1400/media/as-lesson10-process-complete.png)
  
 ## <a name="whats-next"></a>¿Qué sigue?

Vaya a la siguiente lección: [lección 11: crear Roles](../tutorial-tabular-1400/as-lesson-11-create-roles.md). 
