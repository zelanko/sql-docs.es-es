---
title: "Crear una consulta de predicción mediante el generador de consultas de predicción | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- prediction queries [Analysis Services]
- Mining Model Prediction [Analysis Services], prediction queries
ms.assetid: e02836e5-dd8c-4c97-a078-840ae79d3660
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3a61c0e05e427ef4d4e693e1594598dafe85f3c2
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="create-a-prediction-query-using-the-prediction-query-builder"></a>Crear una consulta de predicción con el Generador de consultas de predicción
  Puede crear consultas de predicción mientras está generando una solución de minería de datos en BI Development Studio o al hacer clic con el botón derecho en un modelo de minería de datos existente en SQL Server Management Studio y, después, elegir la opción **Generar consulta de predicción**.  
  
 El **Generador de consultas de predicción** tiene los tres modos de diseño siguientes, entre los que puede cambiar haciendo clic en los iconos en la esquina superior izquierda.  
  
-   **Design**  
  
-   **Consulta**  
  
-   **Resultado**  
  
 El modo**Diseño** permite generar una consulta de predicción eligiendo los datos de entrada, asignando los datos al modelo y, después, agregando funciones de predicción en instrucciones que se generan utilizando la cuadrícula. La cuadrícula de diseño contiene estos bloques de creación:  
  
 **Source**  
 Elija el origen de la nueva columna. Puede utilizar columnas del modelo de minería de datos, las tablas de entrada incluidas en la vista del origen de datos, una función de predicción o una expresión personalizada.  
  
 **Campo**  
 Determina la columna o función específica asociada con la selección de la columna **Origen** .  
  
 **Alias**  
 Determina cuál será el nombre de la columna en el conjunto de resultados.  
  
 **Mostrar**  
 Determina si la selección de la columna **Origen** aparecerá en los resultados.  
  
 **Grupo**  
 Funciona con la columna **Y/O** para agrupar expresiones mediante paréntesis. Por ejemplo, (expr1 o expr2) y expr3.  
  
 **Y/O**  
 Crea lógica en la consulta. Por ejemplo, (expr1 o expr2) y expr3.  
  
 **Criterios o argumento**  
 Especifica una condición o expresión de usuario que se aplica a la columna. Puede arrastrar columnas desde las tablas a la celda.  
  
 El modo**Consulta** proporciona un editor de texto que le da acceso directo al lenguaje de extensiones de minería de datos (DMX), junto con una vista de los datos de entrada y las columnas del modelo. Cuando selecciona el modo **Consulta** , la cuadrícula que ha usado para definir la consulta se reemplaza por un editor de texto básico. Puede utilizar este editor para copiar y guardar las consultas que haya creado o para pegar las consultas DMX existentes y desde el Portapapeles y ejecutarlas después.  
  
 La vista**Resultado** ejecuta la consulta actual y muestra los resultados en una cuadrícula. Si los datos subyacentes han cambiado y desea volver a ejecutar la consulta, haga clic en el botón Reproducir en la barra de estado.  
  
 Puede diseñar una consulta de minería de datos mediante una combinación de las herramientas visuales y el editor de texto. Si escribe los cambios de la consulta en el editor de texto y vuelve a la vista **Diseño** , todos los cambios se perderán y la consulta revierte a la original que se creó en el Generador de consultas de predicción. Este tema le dirige en el uso del generador de consultas gráfico.  
  
### <a name="to-create-a-prediction-query"></a>Para crear una consulta de predicción  
  
1.  Haga clic en la pestaña **Predicción de modelo de minería de datos** del Diseñador de minería de datos.  
  
2.  Haga clic en **Seleccionar modelo** en la tabla **Modelo de minería de datos** .  
  
     Se abre el cuadro de diálogo **Seleccionar modelo de minería de datos** , donde se muestran todas las estructuras de minería de datos que existen en el proyecto actual.  
  
3.  Seleccione el modelo en el que desee crear una predicción y haga clic en **Aceptar**.  
  
4.  En la tabla **Seleccionar tabla(s) de entrada** , haga clic en **Seleccionar tabla de casos**.  
  
     Se abrirá el cuadro de diálogo **Seleccionar tabla** .  
  
5.  En la lista **Origen de datos** , seleccione el origen de datos que contenga los datos sobre los que se va a crear la predicción.  
  
6.  En el cuadro **Nombre de tabla o vista** , seleccione la tabla que contenga los datos sobre los que se vaya a crear una predicción y, después, haga clic en **Aceptar**.  
  
     Después de seleccionar la tabla de entrada, el Generador de consultas de predicción crea una asignación predeterminada entre el modelo de minería de datos y la tabla de entrada, en función de los nombres de las columnas. Para eliminar una asignación, seleccione la línea que vincula la columna de la tabla **Modelo de minería de datos** con la columna asignada de la tabla **Seleccionar tabla(s) de entrada** y presione ELIMINAR. También puede crear asignaciones manualmente haciendo clic en una columna de la tabla **Seleccionar tabla(s) de entrada** y arrastrándola hasta la columna correspondiente de la tabla **Modelo de minería de datos** .  
  
7.  Agregue cualquier combinación de los tres tipos siguientes de información a la cuadrícula del Generador de consultas de predicción:  
  
    -   Columnas de predicción del cuadro **Modelo de minería de datos** .  
  
    -   Cualquier combinación de columnas de entrada del cuadro **Seleccionar tabla(s) de entrada** .  
  
    -   Funciones de predicción  
  
8.  Ejecute la consulta haciendo clic en el primer botón de la barra de herramientas de la pestaña **Predicción de modelo de minería de datos** y seleccione **Resultado**.  
  
## <a name="see-also"></a>Vea también  
 [Crear una consulta singleton en el Diseñador de minería de datos](../../analysis-services/data-mining/create-a-singleton-query-in-the-data-mining-designer.md)   
 [Consultas de minería de datos](../../analysis-services/data-mining/data-mining-queries.md)  
  
  

