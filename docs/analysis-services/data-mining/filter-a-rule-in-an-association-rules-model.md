---
title: "Filtrar una regla en un modelo de reglas de asociaci&#243;n | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "filtrar reglas [Analysis Services]"
  - "Visor de modelos de minería de datos [Analysis Services], reglas"
  - "Visor de reglas"
ms.assetid: 26cdba5b-5bf1-439e-80a3-8759774e918b
caps.latest.revision: 28
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 28
---
# Filtrar una regla en un modelo de reglas de asociaci&#243;n
  Puede usar filtros con los modelos de asociación para restringir los resultados a las asociaciones que le interesan. Por ejemplo, puede filtrar las reglas para mostrar solo las que incluyan un producto concreto.  
  
 En el Diseñador de minería de datos, use los controles de la pestaña **Reglas** del Visor de reglas de asociación de [!INCLUDE[msCoName](../../includes/msconame-md.md)] para filtrar las reglas que se muestran.  También puede crear una consulta en el modelo para ver solo el conjunto de elementos que contiene un valor determinado.  
  
> [!NOTE]  
>  Esta opción solo está disponible para los modelos de minería de datos creados usando el algoritmo de asociación de Microsoft.  
  
### Filtrar una regla en un modelo de asociación  
  
1.  Abra el modelo de minería de datos usando el **Visor de reglas de asociación**. Para hacer esto en SQL Server Management Studio, haga clic con el botón secundario en el nombre del modelo y seleccione **Examinar**. Para hacerlo en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], haga doble clic en la estructura de minería de datos que contiene el modelo y, después, haga clic en la pestaña **Visor de modelos de minería de datos** del **Diseñador de minería de datos**.  
  
2.  Haga clic en la pestaña **Reglas** del **Visor de reglas de asociación**.  
  
3.  Escriba una condición de regla en el cuadro **Regla del filtro** . Por ejemplo, una condición de regla podría ser "Bike Stand", que también devuelve "Bike Stands".  
  
     El cuadro de texto **Regla del filtro** admite expresiones regulares según se definan en el lenguaje de .NET. Por consiguiente, puede utilizar expresiones como esta: `((.Helmets.*Fenders.*)|(.*Fenders.*Helmets.*))` Esta expresión devolvería cualquier conjunto de elementos que incluya atributos con las palabras Helmets y Fenders, en cualquier orden.  
  
4.  En **Probabilidad mínima**, aumente el valor de probabilidad para ver menos reglas o disminuya el valor para ver más reglas.  
  
5.  En **Importancia mínima**, aumente el valor de importancia para ver menos reglas o disminuya el valor para ver más reglas.  
  
6.  En **Mostrar**, seleccione una de las opciones siguientes: **Mostrar el valor y el nombre del atributo**, **Mostrar solo el nombre del atributo**o **Mostrar solo el valor del atributo**.  
  
7.  En **Número máximo de filas**, aumente el valor para aumentar el número total de reglas que cumplen las condiciones especificadas o disminuya el valor para limitar el número de reglas devueltas. Las reglas se ordenan por probabilidad, de modo que podría eliminar reglas adicionales que cumplan las condiciones especificadas para la probabilidad o la importancia.  
  
8.  Seleccione o anule la selección de la casilla **Mostrar nombre largo** para alternar la manera en que se muestran los nombres de las reglas.  
  
     Las reglas se filtran ahora para mostrar únicamente las reglas que contengan el elemento indicado. La condición de filtro se aplica a los valores de atributo antes o después del delimitador de la regla, "->".  
  
    > [!NOTE]  
    >  El visor almacena en memoria caché la lista inicial de reglas, según una consulta del modelo de minería de datos, y no actualiza la lista de reglas a menos que cambie las condiciones de la consulta estableciendo las filas máximas, la probabilidad, la importancia o la presentación de nombres largos. Por consiguiente, si escribe una condición y la presentación no se actualiza inmediatamente, puede obligar al visor a que actualice los datos seleccionando y anulando la selección de la casilla **Mostrar nombres largos** .  
  
### Crear una consulta en los conjuntos de elementos en un modelo de asociación  
  
-   [Ejemplos de consultas del modelo de asociación](../../analysis-services/data-mining/association-model-query-examples.md)  
  
## Vea también  
 [Tareas y procedimientos del Visor de modelos de minería de datos](../../analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)   
 [Examinar un modelo usando el Visor de reglas de asociación de Microsoft](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-association-rules-viewer.md)   
 [Lección 3: Generar un escenario de cesta de la compra &#40;Tutorial intermedio de minería de datos&#41;](../Topic/Lesson%203:%20Building%20a%20Market%20Basket%20Scenario%20\(Intermediate%20Data%20Mining%20Tutorial\).md)  
  
  