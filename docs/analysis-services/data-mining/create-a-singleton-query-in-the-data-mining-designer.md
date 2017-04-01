---
title: "Crear una consulta singleton en el Dise&#241;ador de miner&#237;a de datos | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "singleton, consultas [Analysis Services]"
  - "predicción de modelo de minería de datos [Analysis Services], consultas singleton"
ms.assetid: 6cdca8a0-cf16-46eb-a652-0bff820625ab
caps.latest.revision: 38
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 38
---
# Crear una consulta singleton en el Dise&#241;ador de miner&#237;a de datos
  Una consulta singleton es útil para crear una predicción para un único caso. Para obtener más información sobre las consultas singleton, vea [Consultas de minería de datos](../../analysis-services/data-mining/data-mining-queries.md).  
  
 En la pestaña **Predicción de modelo de minería de datos** del Diseñador de minería de datos, puede crear muchos tipos diferentes de consultas. Puede crear una consulta usando el diseñador o escribiendo las instrucciones de Extensiones de minería de datos (DMX). Puede iniciar con el diseñador y modificar la consulta que crea cambiando las instrucciones de DMX o agregando una cláusula WHERE u ORDER BY.  
  
 Para intercambiar entre la vista de diseño de consulta y la vista de texto de consulta, haga clic en el primer botón de la barra de herramientas. En la vista del texto de la consulta es posible ver el código DMX creado por el Generador de consultas de predicción. También puede ejecutar la consulta, modificarla y ejecutar la consulta modificada. No obstante, la consulta modificada no se mantiene si se cambia a la vista de diseño de la consulta.  
  
 El código siguiente muestra un ejemplo de una consulta singleton frente al modelo de correo directo, TM_Decision_Tree.  
  
```  
SELECT [Bike Buyer], PredictProbability([Bike Buyer]) as ProbableBuyer  
FROM [TM_Decision_Tree]  
NATURAL PREDICTION JOIN  
(SELECT '2' AS [Number Children At Home], '45' as [Age])  
AS [t]  
```  
  
 Los pasos siguientes explican cómo crear esta consulta de predicción.  
  
### Para crear una consulta singleton con el Diseñador de minería de datos  
  
1.  Haga clic en la pestaña **Predicción de modelo de minería de datos** del Diseñador de minería de datos.  
  
2.  Haga clic en **Seleccionar modelo** en la tabla **Modelo de minería de datos** .  
  
     Se abre el cuadro de diálogo **Seleccionar modelo de minería de datos** , donde se muestran todas las estructuras de minería de datos que existen en el proyecto actual.  
  
     Seleccione el modelo que desea usar para crear una predicción.  
  
     Por ejemplo, para crear el código de ejemplo mostrado al inicio de este tema, seleccione TM_Decision_Tree y, después, haga clic en **Aceptar**.  
  
3.  Haga clic en **Consulta singleton** en la barra de herramientas de la pestaña **Predicción de modelo de minería de datos** .  
  
     Aparece en la pestaña la tabla **Entrada de consulta singleton** con las columnas automáticamente asignadas a las columnas de la tabla **Modelo de minería de datos** .  
  
4.  En la tabla **Entrada de consulta singleton** , seleccione los valores de la columna **Valor** para describir el caso para el que desea crear una predicción.  
  
     Por ejemplo, seleccione **2** para **Number Children At Home**y, a continuación, escriba **45** para **Age**.  
  
5.  Arrastre una columna de predicción de la tabla **Modelo de minería de datos** hacia la columna **Origen** en la parte inferior de la pestaña. También puede escribir un alias para la columna.  
  
     Por ejemplo, arrastre **Bike Buyer** a la columna **Origen** .  
  
6.  Para agregar funciones adicionales a la consulta, seleccione **Función de predicción** o **Expresión personalizada** en la lista desplegable de la columna **Origen**.  
  
     Por ejemplo, haga clic en **Función de predicción**y seleccione **PredictProbability**.  
  
7.  Haga clic en **Criterios o argumento** en la fila **PredictProbability** y escriba el nombre de la columna que se va a predecir y, opcionalmente, un valor concreto para predecir.  
  
     Por ejemplo, escriba **[Bike Buyer], 1**.  
  
8.  Haga clic en el cuadro **Alias** en la fila **PredictProbability** y escriba un nombre al que hacer referencia a la nueva columna.  
  
     Por ejemplo, escriba **ProbableBuyer**.  
  
9. Haga clic en **Cambiar a vista de resultado de consulta** en la barra de herramientas de la pestaña **Predicción de modelo de minería de datos** .  
  
     Aparece una nueva ventana mostrando el resultado de la consulta. Para ver la instrucción DMX que acaba de crear, haga clic en **SQL**.  
  
## Vea también  
 [Consultas de predicción &#40;minería de datos&#41;](../../analysis-services/data-mining/prediction-queries-data-mining.md)  
  
  