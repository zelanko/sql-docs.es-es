---
title: 'Analysis Services lección del tutorial de 10: Creación de particiones | Microsoft Docs'
ms.date: 08/27/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile"
ms.openlocfilehash: f7b6e5bfd4c533028758f553e5d8c9b2ca21e6f2
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2018
ms.locfileid: "52401148"
---
# <a name="create-partitions"></a>Crear particiones

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

En esta lección, creará particiones dividir la tabla FactInternetSales en partes lógicas más pequeñas que se pueden procesar (actualiza) independientemente de otras particiones. De forma predeterminada, cada tabla que se incluye en el modelo tiene una partición, que incluye toda la tabla columnas y filas. Para la tabla FactInternetSales, queremos dividir los datos por año; una partición para cada uno de cinco años de la tabla. Cada partición se podrá procesar entonces independientemente. Para obtener más información, consulte [Particiones](../tabular-models/partitions-ssas-tabular.md). 
  
Tiempo estimado para completar esta lección: **15 minutos**  
  
## <a name="prerequisites"></a>Requisitos previos  

En este artículo forma parte de un tutorial de modelado tabular, que se debe completar en orden. Antes de realizar las tareas en esta lección, debe haber completado la lección anterior: [Lección 9: Crear jerarquías](../tutorial-tabular-1400/as-lesson-9-create-hierarchies.md).  
  
## <a name="create-partitions"></a>Crear particiones  
  
#### <a name="to-create-partitions-in-the-factinternetsales-table"></a>Para crear particiones en la tabla FactInternetSales  
  
1.  En el Explorador de modelos tabulares, expanda **tablas**y, a continuación, haga clic en **FactInternetSales** > **particiones**.  
  
2.  En el Administrador de particiones, haga clic en **copia**y, a continuación, cambie el nombre a **FactInternetSales2010**.
  
    Porque desea que la partición incluya solamente las filas en un período determinado, para el año 2010, debe modificar la expresión de consulta.
  
4.  Haga clic en **diseño** para abrir el Editor de consultas y, a continuación, haga clic en el **FactInternetSales2010** consulta.

5.  En vista previa, haga clic en la flecha hacia abajo en la **OrderDate** encabezado de columna y, a continuación, haga clic en **filtros de fecha y hora** > **entre**.

    ![como-lesson10--editor de consultas](../tutorial-tabular-1400/media/as-lesson10-query-editor.png)

6.  En el cuadro de diálogo Filtrar filas en **mostrar filas donde: OrderDate**, deje **es posterior o igual a**y, a continuación, en el campo de fecha, escriba **1/1/2010**. Deje el **y** , a continuación, seleccione el operador seleccionado, **antes**, a continuación, en el campo de fecha, escriba **1/1/2011**y, a continuación, haga clic en **Aceptar**.

    ![como-lesson10-filtro de filas](../tutorial-tabular-1400/media/as-lesson10-filter-rows.png)
    
    Tenga en cuenta en el Editor de consultas, en pasos aplicados, verá otro paso llamado filas filtradas. Este filtro consiste en seleccionar solo las fechas de pedidos de 2010.

8.  Haga clic en **Importar**.

    En el Administrador de particiones, observe que ahora la expresión de consulta tiene una cláusula filas filtradas adicional.

    ![consulta como lesson10](../tutorial-tabular-1400/media/as-lesson10-query.png)
  
    Esta instrucción especifica que esta partición debe incluir solo los datos de esas filas donde el valor OrderDate está en el año 2010 tal como se especifica en la cláusula filas filtradas.  
  
  
#### <a name="to-create-a-partition-for-the-2011-year"></a>Para crear una partición para el año 2011  
  
1.  En la lista de particiones, haga clic en el **FactInternetSales2010** de partición que ha creado y, a continuación, haga clic en **copia**.  Cambie el nombre de la partición a **FactInternetSales2011**. 

    No es necesario utilizar el Editor de consultas para crear una nueva cláusula filas filtradas. Dado que ha creado una copia de la consulta para 2010, todo lo que necesita hacer es efectuar un pequeño cambio en la consulta de 2011.
  
2.  En **expresión de consulta**, en orden para que esta partición incluya solamente las filas del año 2011, reemplace los años en la cláusula filas filtradas con **2011** y **2012**, respectivamente, como:  
  
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
  
- Siga los pasos anteriores, la creación de particiones de 2012, 2013 y 2014, el cambio de los años en la cláusula filas filtradas para incluir solo las filas correspondientes a ese año. 
  

## <a name="delete-the-factinternetsales-partition"></a>Eliminar la partición FactInternetSales

Ahora que tiene particiones para cada año, puede eliminar la partición FactInternetSales; al elegir procesar toda al procesar particiones, que impiden que se superponen.

#### <a name="to-delete-the-factinternetsales-partition"></a>Para eliminar la partición FactInternetSales

-  Haga clic en el **FactInternetSales** de partición y, a continuación, haga clic en **eliminar**.



## <a name="process-partitions"></a>Procesar particiones  

En el Administrador de particiones, tenga en cuenta la **procesado por última vez** columna para cada una de las nuevas particiones que ha creado se muestra estas particiones nunca se han procesado. Al crear particiones, debe ejecutar una operación procesar particiones o procesar tabla para actualizar los datos de esas particiones.  
  
#### <a name="to-process-the-factinternetsales-partitions"></a>Para procesar las particiones FactInternetSales  
  
1.  Haga clic en **Aceptar** para cerrar el Administrador de partición.  
  
2.  Haga clic en el **FactInternetSales** de tabla y, después, haga clic en el **modelo** menú > **proceso** > **procesar particiones**.  
  
3.  En el cuadro de diálogo procesar particiones, compruebe **modo** está establecido en **proceso predeterminado**.  
  
4.  Active la casilla de la columna **Procesar** para cada una de las cinco particiones que ha creado y haga clic en **Aceptar**.  

    ![como-lesson10-procesar-particiones](../tutorial-tabular-1400/media/as-lesson10-process-partitions.png)
  
    Si se le pidan las credenciales de suplantación, escriba el nombre de usuario de Windows y la contraseña que especificó en la lección 2.  
  
    Aparece el cuadro de diálogo **Procesamiento de datos** con los detalles del proceso de cada partición. Observe que se ha transferido un número diferente de filas para cada partición. Cada partición incluye solamente las filas del año especificado en la cláusula WHERE en la instrucción SQL. Cuando finalice el procesamiento, continúe y cierre el cuadro de diálogo Procesamiento de datos.  
  
    ![como lesson10-proceso-completo](../tutorial-tabular-1400/media/as-lesson10-process-complete.png)
  
 ## <a name="whats-next"></a>¿Qué sigue?

Vaya a la lección siguiente: [Lección 11: Crear Roles](../tutorial-tabular-1400/as-lesson-11-create-roles.md). 
