---
title: Elegir y asignar datos de entrada para una consulta de predicción | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- tables [Analysis Services], prediction queries
- Mining Model Prediction [Analysis Services], input tables
ms.assetid: 00d330a0-879d-4da0-9f29-53c288116f4d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 89eaf3b59f6d779a01168b00d51acbee1e96ca7e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66085846"
---
# <a name="choose-and-map-input-data-for-a-prediction-query"></a>Elegir y asignar datos de entrada para una consulta de predicción
  Generalmente, la creación de predicciones a partir de un modelo de minería de datos se realiza proporcionando datos nuevos al modelo. (La excepción son los modelos de serie temporal, que pueden realizar predicciones basadas únicamente en datos históricos). Para proporcionar nuevos datos al modelo, debe asegurarse de que los datos están disponibles como parte de una vista del origen de datos. Si conoce de antemano los datos que va a usar para la predicción, puede incluirlos en la vista del origen de datos usada para crear el modelo. De lo contrario, es posible que tenga que crear una nueva vista del origen de datos. Para más información, vea [Vistas del origen de datos en modelos multidimensionales](../multidimensional-models/data-source-views-in-multidimensional-models.md).  
  
 Algunas veces, los datos que necesita se encuentran en varias tablas en una combinación de uno a varios. Es el caso de los datos usados para los modelos de asociación o los modelos de clústeres de secuencia, que usan una tabla de casos vinculada a una tabla anidada que contiene detalles sobre productos o transacciones. Si el modelo usa una estructura de tabla de casos anidados, los datos usados para la predicción también deben tener dicha estructura.  
  
> [!WARNING]  
>  No puede agregar columnas nuevas ni asignar columnas que se encuentren en una vista del origen de datos diferente. La vista del origen de datos que seleccione debe contener todas las columnas que necesite para la consulta de predicción.  
  
 Una vez identificadas las tablas que contienen los datos que va a usar para las predicciones, deberá asignar las columnas de los datos externos a las columnas del modelo de minería de datos. Por ejemplo, si el modelo predice los hábitos de compra de los clientes basándose en datos demográficos y respuestas de encuestas, los datos de entrada deben contener información que se corresponda generalmente con lo que se encuentra en el modelo. No es necesario que haya datos coincidentes para todas y cada una de las columnas, pero a cuántas más columnas pueda asignar datos, mejor. Si intenta asignar columnas que tienen tipos de datos diferentes, es posible que obtenga un error. En ese caso, podría definir un cálculo con nombre en la vista del origen de datos para convertir los nuevos datos de las columnas al tipo de datos requerido por el modelo. Para obtener más información, vea [definir cálculos con nombre en una vista del origen de datos &#40;Analysis Services&#41;](../multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md).  
  
 Al elegir los datos que se van a usar para la predicción, es posible que algunas de las columnas del origen de datos seleccionado se asignen automáticamente a las columnas del modelo de minería de datos, basándose en la similitud de los nombres y el tipo de datos coincidentes. Puede usar el cuadro de diálogo **Modificar asignación** de la pestaña **Predicción de modelo de minería de datos** para cambiar las columnas que se han asignado, eliminar las asignaciones inapropiadas o crear nuevas asignaciones para las columnas existentes. La superficie de diseño **Predicción de modelo de minería de datos** también admite la edición de tipo arrastrar y colocar para las conexiones.  
  
-   Para crear una conexión, seleccione una columna de la tabla **Modelo de minería de datos** y arrástrela hasta la columna correspondiente en la tabla **Seleccionar tabla(s) de entrada** .  
  
-   Para quitar una conexión, seleccione la línea de conexión y presione la tecla Supr.  
  
 En el procedimiento siguiente se describe cómo modificar las combinaciones que se han creado entre la tabla de casos y una tabla anidada que se usan como entradas de una consulta de predicción mediante el cuadro de diálogo **Especificar combinación anidada** .  
  
### <a name="select-an-input-table"></a>Seleccionar una tabla de entrada  
  
1.  En la tabla **Seleccionar tabla(s) de entrada** de la pestaña **Gráfico de precisión de minería de datos** del Diseñador de minería de datos de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], haga clic en **Seleccionar tabla de casos**.  
  
     Aparece el cuadro de diálogo **Seleccionar tablas** , en el que puede seleccionar la tabla que contiene los datos sobre los que basará sus consultas.  
  
2.  En el cuadro de diálogo **Seleccionar tablas** , seleccione un origen de datos de la lista **Origen de datos** .  
  
3.  En **Nombre de tabla o vista**, seleccione la tabla que contiene los datos que quiere usar para probar los modelos.  
  
4.  Haga clic en **OK**.  
  
     Las columnas de la estructura de minería de datos se asignarán automáticamente a las columnas que tengan el mismo nombre en la tabla de entrada.  
  
### <a name="change-the-way-that-input-data-is-mapped-to-the-model"></a>Cambiar la forma en la que los datos de entrada se asignan al modelo  
  
1.  En el Diseñador de minería de datos de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], seleccione la pestaña **Predicción de modelo de minería de datos** .  
  
2.  En el menú **Modelo de minería de datos** , seleccione **Modificar conexiones**.  
  
     Se abre el cuadro de diálogo **Modificar asignación** . En este cuadro de diálogo, la **Columna del modelo de minería de datos** muestra las columnas de la estructura de minería de datos seleccionada. En la columna **Columna de la tabla** se muestran las columnas del origen de datos externo que ha elegido en el cuadro de diálogo **Seleccionar tabla(s) de entrada** . Las columnas del origen de datos externo se asignan a las columnas del modelo de minería de datos.  
  
3.  En **Columna de la tabla**, seleccione la fila que corresponda a la columna del modelo de minería de datos a la que desee asignarla.  
  
4.  Seleccione una columna nueva en la lista de columnas disponibles del origen de datos externo. Seleccione el elemento en blanco en la lista para eliminar la asignación de columnas.  
  
5.  Haga clic en **OK**.  
  
     Las nuevas asignaciones de columnas se muestran en el diseñador.  
  
### <a name="remove-a-relationship-between-input-tables"></a>Quitar una relación entre tablas de entrada  
  
1.  En la tabla **Seleccionar tabla(s) de entrada** de la pestaña **Predicción de modelo de minería** de datos del Diseñador de minería de datos de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], haga clic en **Modificar combinación**.  
  
     Se abre el cuadro de diálogo **Especificar combinación anidada** .  
  
2.  Seleccione una relación.  
  
3.  Haga clic en **Quitar relación**.  
  
4.  Haga clic en **OK**.  
  
     La relación entre la tabla de casos y la tabla anidada se ha eliminado.  
  
### <a name="create-a-new-relationship-between-input-tables"></a>Crear una nueva relación entre tablas de entrada  
  
1.  En la tabla **Seleccionar tabla(s) de entrada** de la pestaña **Predicción de modelo de minería de datos** del Diseñador de minería de datos, haga clic en **Modificar combinación**.  
  
     Se abre el cuadro de diálogo **Especificar combinación anidada** .  
  
2.  Haga clic en **Agregar relación**.  
  
     Se abrirá el cuadro de diálogo **Crear relación** .  
  
3.  Seleccione la clave de la tabla anidada en **Columnas de origen**.  
  
4.  Seleccione la clave de la tabla de casos en **Columnas de destino**.  
  
5.  Haga clic en **Aceptar** en el cuadro de diálogo **Crear relación** .  
  
6.  Haga clic en **Aceptar** en el cuadro de diálogo **Especificar combinación anidada** .  
  
     Se crea una nueva relación entre la tabla de casos y la tabla anidada.  
  
### <a name="add-a-nested-table-to-the-input-tables-of-a-prediction-query"></a>Agregar una tabla anidada a las tablas de entrada de una consulta de predicción  
  
1.  En la pestaña **Predicción de modelo de minería de datos** del Diseñador de minería de datos, haga clic en **Seleccionar tabla de casos** para abrir el cuadro de diálogo **Seleccionar tabla** .  
  
    > [!NOTE]  
    >  No podrá agregar una tabla anidada a las entradas a menos que haya especificado una tabla de casos. El uso de una tabla anidada requiere que el modelo de minería de datos que se usa para la predicción también haga uso de este tipo de tabla.  
  
2.  En el cuadro de diálogo **Seleccionar tabla** , seleccione un origen de datos en la lista **Origen de datos** y seleccione la tabla en la vista del origen de datos que contiene los datos de los casos. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
3.  Haga clic en **Seleccionar tabla anidada** para abrir el cuadro de diálogo **Seleccionar tabla** .  
  
4.  En el cuadro de diálogo **Seleccionar tabla** , seleccione un origen de datos en la lista **Origen de datos** y seleccione la tabla en la vista del origen de datos que contiene los datos anidados. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Si ya existe una relación, las columnas del modelo de minería de datos se asignan automáticamente a las columnas que tienen el mismo nombre en la tabla de entrada. Puede modificar la relación entre la tabla anidada y la tabla de casos haciendo clic en **Modificar combinación**, que abre el cuadro de diálogo **Crear relación** .  
  
## <a name="see-also"></a>Consulte también  
 [Consultas de predicción &#40;minería de datos&#41;](prediction-queries-data-mining.md)  
  
  
