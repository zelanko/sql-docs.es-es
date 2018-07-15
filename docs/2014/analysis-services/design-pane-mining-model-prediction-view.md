---
title: (Vista predicción de modelo de minería de datos) del panel de diseño | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.prediction.design.f1
ms.assetid: 17f24c8d-43cd-4f4d-83b3-a41ee8fbe8e8
caps.latest.revision: 26
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8ea979da7db4f0288a01a7bfe9655d1fb34518d6
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37316035"
---
# <a name="design-pane-mining-model-prediction-view"></a>Diseño (panel de la vista Predicción de modelo de minería de datos)
  El panel **Diseño** contiene el Generador de consultas de predicción, que puede utilizar para generar predicciones de minería de datos. Puede diseñar consultas de predicción que usen tablas de datos de entrada de una vista del origen de datos para generar predicciones masivas o puede crear consultas de predicción singleton que permiten proporcionar valores individuales.  
  
 Para ejecutar la consulta y ver los resultados, cambie a la vista de resultado de la consulta.  
  
 La vista **Consulta** muestra la consulta Extensiones de minería de datos (DMX) que crea el Generador de consultas de predicción. Si conoce DMX, puede personalizar esta consulta.  
  
> [!NOTE]  
>  Si hace algún cambio manualmente en la consulta, los cambios se perderán al volver a la vista Diseño. Si desea guardar la consulta DMX, puede copiar la consulta en el Portapapeles de Windows y, a continuación, pegarlo en un archivo de texto.  
  
 **Para obtener más información:** [Consultas de minería de datos](data-mining/data-mining-queries.md)  
  
## <a name="options"></a>Opciones  
 **Cambiar a vista de resultado de consulta**  
 Haga clic para cambiar entre los paneles **Diseño**, **Consulta**y **Resultado** . Al cambiar al panel **Resultado** se ejecuta la consulta.  
  
 **Guardar el resultado de consulta**  
 Abre el cuadro de diálogo **Guardar resultado de consulta de minería de datos** .  
  
 **Consulta singleton**  
 Habilita la creación de una consulta singleton, en la que puede proporcionar valores directamente para la consulta en lugar de proporcionar una tabla como el origen de los datos conocidos. La tabla **Seleccionar tabla(s) de entrada** se reemplaza por una tabla **Entrada de consulta singleton** .  
  
 **Actualizar los resultados de la consulta**  
 Vuelve a procesar la consulta de predicción. Esto solo está habilitado en el panel **Resultado** .  
  
 **Modelo de minería de datos**  
 Muestra el modelo de minería de datos seleccionado en el que desea basar las predicciones.  
  
 **Seleccionar modelo**  
 Abre el cuadro de diálogo **Seleccionar modelo de minería de datos** .  
  
 **Seleccione las tablas de entrada**  
 Muestra las tablas de entrada seleccionadas que contienen datos conocidos en los que se basarán las predicciones.  
  
 **Eliminar tabla**  
 Elimina la tabla seleccionada. Esta botón se deshabilita si no existe o no se ha seleccionado una tabla.  
  
 **Seleccionar tabla de casos**  
 Abre el cuadro de diálogo **Seleccionar tabla** . Este botón solo aparece si no se ha seleccionado una tabla de casos.  
  
 **Seleccionar tabla anidada**  
 Abre el cuadro de diálogo **Seleccionar tabla** . Este botón solo aparece si se ha seleccionado una tabla de casos. Este botón se deshabilita si la estructura de minería de datos asociada no contiene una tabla anidada.  
  
 **Modificar combinación**  
 Abre el cuadro de diálogo **Especificar combinación anidada** . Este botón solo está activo si se ha seleccionado una tabla anidada.  
  
 **Entrada de consulta singleton**  
 Se habilita cuando selecciona el botón **Consulta singleton** . Contiene las columnas siguientes:  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**Columna del modelo de minería de datos**|Muestra las columnas del modelo de minería de datos contenidas en el modelo de minería de datos seleccionado en la tabla **Modelo de minería de datos** .|  
|**Value**|Seleccione un valor de la lista que contiene cada estado posible de la columna del modelo de minería de datos que se ha seleccionado.<br /><br /> Si la columna es una columna de tabla anidada, haga clic en la celda de valor para abrir el cuadro de diálogo **Entrada de tabla anidada** .|  
  
 **Source**  
 Seleccione el origen que contiene el campo que utilizará para la columna. Puede usar el modelo de minería de datos seleccionado en la tabla **Modelo de minería de datos** , la tabla o las tablas seleccionadas en la tabla **Seleccionar tabla(s) de entrada** , una función de predicción o una expresión personalizada.  
  
 Se puede arrastrar las columnas de las tablas que contienen el modelo de minería de datos y las tablas de entrada a la celda.  
  
 **Campo**  
 En la tabla de origen, seleccione una columna de la lista de columnas derivadas. Si ha seleccionado **Función de predicción** en **Origen**, ésta contiene la función de predicción disponible para el modelo de minería de datos seleccionado.  
  
 **Grupo**  
 Use esta opción con la columna **Y/O** para agrupar expresiones. Por ejemplo, `(expr1 Or expr2) And expr3`.  
  
 **Y/O**  
 Utilice esta opción para crear una consulta lógica. Por ejemplo, `(expr1 Or expr2) And expr3`.  
  
 **Criterios o argumento**  
 Especifique una condición o una expresión de usuario que se aplica a la columna. Se puede arrastrar las columnas de las tablas que contienen el modelo de minería de datos y las tablas de entrada a la celda.  
  
## <a name="see-also"></a>Vea también  
 [Extensiones de minería de datos &#40;DMX&#41; referencia de instrucciones](/sql/dmx/data-mining-extensions-dmx-statements)   
 [Interfaces de consultas de minería de datos](data-mining/data-mining-query-tools.md)   
 [Generador de consultas de predicción &#40;minería de datos&#41;](prediction-query-builder-data-mining.md)  
  
  
