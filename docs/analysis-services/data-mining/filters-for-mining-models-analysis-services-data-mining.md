---
title: "Filtros para los modelos de minería de datos (Analysis Services: minería de datos) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- attributes [data mining]
- filter syntax [data mining]
- models [Analysis Services], filtering
- filters [data mining]
- filtering data [Analysis Services]
ms.assetid: 0f29c19c-4be3-4bc7-ab60-f4130a10d59c
caps.latest.revision: 27
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: db42f50eca097c58afac1ded71d143f8230fd42d
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="filters-for-mining-models-analysis-services---data-mining"></a>Filtros para modelos de minería (Analysis Services - Minería de datos)
  El filtrado de modelos basado en datos ayuda a crear modelos de minería de datos que usan subconjuntos de datos en una estructura de minería de datos. El filtrado proporciona flexibilidad a la hora de diseñar orígenes de datos y estructuras de minería de datos propios, porque se puede crear una estructura de minería de datos única basándose en una vista del origen de datos completa. A continuación, puede crear filtros para usar solo una parte de esos datos para aprendizaje y probar una variedad de modelos, en lugar de generar una estructura diferente y un modelo relacionado para cada subconjunto de datos.  
  
 Por ejemplo, define la vista del origen de datos en la tabla Customers y las tablas relacionadas. Luego define una estructura de minería de datos única que incluye todos los campos necesarios. Por último, crea un modelo que se filtra en un atributo de cliente determinado, como Región. A continuación, puede realizar fácilmente una copia de ese modelo y cambiar la condición de filtro para generar un nuevo modelo basado en una región diferente.  
  
 Algunos escenarios de uso real donde podría aprovechar las ventajas de esta característica son los siguientes:  
  
-   Creación de modelos independientes para valores discretos como género, regiones, etc. Por ejemplo, un almacén de ropa podría usar los datos demográficos de los clientes para generar modelos independientes por género, aunque los datos de ventas procedan de un origen de datos único para todos los clientes.  
  
-   Experimentación con modelos creando y probando a continuación varias agrupaciones de los mismos datos, como edades de 20 a 30 frente a edades de 20 a 40 y de 20 a 25 años.  
  
-   Especificación de los filtros complejos en el contenido de las tablas anidadas, como requerir que un caso se incluya en el modelo solo si el cliente ha comprado al menos dos artículos de un producto determinado.  
  
 En esta sección se explica cómo generar, usa y administrar filtros en los modelos de minería de datos.  
  
## <a name="creating-model-filters"></a>Crear filtros de modelo  
 Para crear y aplicar filtros puede hacer lo siguiente:  
  
-   Usar la pestaña **Modelos de minería de datos** en el Diseñador de minería de datos para generar condiciones con la ayuda de los cuadros de diálogo del editor de filtros.  
  
-   Escribir una expresión de filtro directamente en la propiedad **Filter** del modelo de minería de datos.  
  
-   Establecer condiciones de filtro en un modelo mediante programación usando AMO.  
  
### <a name="creating-model-filters-using-data-mining-designer"></a>Crear filtros de modelo mediante el Diseñador de minería de datos  
 Primero filtra un modelo en el Diseñador de minería de datos cambiando la propiedad **Filter** del modelo de minería de datos. Puede escribir una expresión de filtro directamente en el panel **Propiedades** o bien, puede abrir un cuadro de diálogo de filtro para generar condiciones.  
  
 Hay dos cuadros de diálogo de filtro. El primero le permite crear condiciones que se aplican a la tabla de casos. Si el origen de datos contiene varias tablas, primero seleccione una tabla y, a continuación, seleccione una columna y especifique los operadores y condiciones que desee que se apliquen a dicha columna. Puede vincular varias condiciones con los operadores **AND**/**OR** . Los operadores disponibles para definir valores dependen de si la columna contiene valores discretos o continuos. Por ejemplo, con valores continuos, puede usar operadores **greater than** y **less than** . Pero, para valores discretos, puede usar los operadores **= (igual a)**, **!= (distinto de)**y **es NULL** .  
  
> [!NOTE]  
>  No se admite la palabra clave **LIKE** . Si desea incluir varios atributos discretos, debe crear condiciones individuales y vincularlas mediante el operador **OR** .  
  
 Si las condiciones son complejas, puede usar el segundo cuadro de diálogo de filtros para trabajar con una tabla cada vez. Cuando se cierra el segundo cuadro de diálogo de filtros, la expresión se evalúa y, a continuación, se combina con las condiciones de filtro que se han establecido en otras columnas de la tabla de casos.  
  
### <a name="creating-filters-on-nested-tables"></a>Crear filtros en tablas anidadas  
 Si la vista del origen de datos contiene tablas anidadas, puede usar el segundo cuadro de diálogo de filtros para generar condiciones en las filas de las tablas anidadas.  
  
 Por ejemplo, si su tabla de casos está relacionada con los clientes y la tabla anidada muestra los productos que ha comprado un cliente, puede crear un filtro para los clientes que han comprado determinados elementos usando la sintaxis siguiente en el filtro de tabla anidada: `[ProductName]=’Water Bottle’ OR ProductName=’Water Bottle Cage'`.  
  
 También puede filtrar por la existencia de un valor determinado en la tabla anidada usando las palabras clave **EXISTS** o **NOT EXISTS** y una subconsulta. Esto le permite crear condiciones como `EXISTS (SELECT * FROM Products WHERE ProductName=’Water Bottle’)`. `EXISTS SELECT(<subquery>)` devuelve **true** si la tabla anidada contiene como mínimo una fila con el valor `Water Bottle`.  
  
 Puede combinar condiciones en la tabla de casos con condiciones en la tabla anidada. Por ejemplo, la sintaxis siguiente incluye una condición en la tabla de casos (`Age > 30` ), una subconsulta en la tabla anidada (`EXISTS (SELECT * FROM Products)`) y varias condiciones en la tabla anidada (`WHERE ProductName=’Milk’  AND Quantity>2`)).  
  
```  
(Age > 30 AND EXISTS (SELECT * FROM Products WHERE ProductName=’Milk’  AND Quantity>2) )  
```  
  
 Cuando se termina de generar el filtro, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]evalúa el texto del mismo, después se traduce a una expresión DMX y por último se guarda con el modelo.  
  
 Para obtener instrucciones sobre cómo usar los cuadros de diálogo de filtros en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], vea [Aplicar un filtro a un modelo de minería de datos](../../analysis-services/data-mining/apply-a-filter-to-a-mining-model.md).  
  
## <a name="managing-mining-model-filters"></a>Administrar filtros de modelo de minería de datos  
 El filtrado de modelos basado en datos simplifica en gran medida la tarea de administrar estructuras y modelos de minería de datos porque permite crear fácilmente varios modelos basados en la misma estructura. También puede realizar rápidamente copias de modelos de minería de datos existentes y, a continuación, cambiar solo la condición de filtro. Sin embargo, los filtros pueden producir cierta confusión.  
  
 He aquí algunas preguntas frecuentes sobre cómo administrar e interpretar filtros en los modelos de minería de datos:  
  
### <a name="how-can-i-tell-whether-a-filter-is-being-used"></a>¿Cómo puedo saber si se está usando un filtro?  
 Hay varias formas de determinar si se está aplicando un filtro a un modelo:  
  
-   En el diseñador, haga clic en la pestaña **Modelos de minería de datos** , abra **Propiedades**y vea la propiedad **Filter** del modelo de minería de datos.  
  
-   La DMV DMSCHEMA_MINING_MODELS muestra una columna que contiene el texto del filtro. Puede usar la consulta siguiente en una DMV para devolver los nombres de los modelos y sus filtros:  
  
    ```  
    SELECT MODEL_NAME, [FILTER]   
    FROM $SYSTEM.DMSCHEMA_MINING_MODELS  
  
    ```  
  
-   Puede obtener el valor de la propiedad Filter del objeto MiningModel en AMO o bien inspeccionar el elemento Filter en XMLA.  
  
 También puede establecer una convención de nomenclatura de los modelos para reflejar el contenido del filtro. Esto facilita indicar los modelos relacionados de manera independiente.  
  
### <a name="how-can-i-save-a-filter"></a>¿Cómo se guarda un filtro?  
 La expresión de filtro se guarda como un script almacenado con la tabla anidada o el modelo de minería de datos asociado. Si elimina el texto del filtro, solo podrá restaurarlo si vuelve a crear manualmente la expresión de filtro. Por consiguiente, si crea expresiones de filtro complejas, debería crear una copia de seguridad del texto del filtro.  
  
### <a name="why-cant-i-see-any-effects-from-the-filter"></a>¿Por qué no veo ningún efecto del filtro?  
 Siempre que cambie o agregue una expresión de filtro, debe volver a procesar la estructura y el modelo para ver los efectos del filtro.  
  
### <a name="why-do-i-see-filtered-attributes-in-prediction-query-results"></a>¿Por qué veo atributos filtrados en los resultados de una consulta de predicción?  
 Al aplicar un filtro a un modelo, solo afecta a la selección de casos empleados para entrenar el modelo. El filtro no afecta a los atributos conocidos para el modelo ni cambia o suprime datos que están presentes en el origen de datos. Por tanto, las consultas realizadas en el modelo pueden devolver predicciones de otros tipos de casos y las listas desplegables de valores usados por el modelo pueden mostrar valores de atributos excluidos por el filtro.  
  
 Por ejemplo, suponga que entrena el modelo [Bike Buyer] usando solo casos relativos a mujeres con edades comprendidas entre 20 y 30 años. Puede ejecutar una consulta de predicción que prediga la probabilidad de que un hombre compre una bicicleta o predecir el resultado en el caso de una mujer de entre 30 y 40 años. Esto se debe a que los atributos y los valores presentes en el origen de datos definen lo que teóricamente es posible, mientras que los casos definen las repeticiones usadas para el entrenamiento. No obstante, estas consultas devolverían probabilidades muy pequeñas, ya que los datos de aprendizaje no contienen ningún caso con los valores de destino.  
  
 Si necesita ocultar completamente o hacer anónimos los valores de atributos del modelo, hay varias opciones:  
  
-   Filtrar los datos entrantes como parte de la definición de la vista del origen de datos o en el origen de datos relacional.  
  
-   Enmascarar o codificar el valor de atributo.  
  
-   Contraer los valores excluidos de una categoría como parte de la definición de la estructura de minería de datos.  
  
## <a name="related-resources"></a>Recursos relacionados  
 Para más información sobre la sintaxis del filtro, así como ejemplos de expresiones de filtros, vea [Sintaxis y ejemplos del filtro de modelos &#40;Analysis Services: Minería de datos&#41;](../../analysis-services/data-mining/model-filter-syntax-and-examples-analysis-services-data-mining.md).  
  
 Para más información sobre cómo usar los filtros de modelo al probar un modelo de minería de datos, vea [Elegir un tipo de gráfico de precisión y establecer las opciones del gráfico](../../analysis-services/data-mining/choose-an-accuracy-chart-type-and-set-chart-options.md).  
  
## <a name="see-also"></a>Vea también  
 [Sintaxis y ejemplos del filtro de modelos &#40;Analysis Services: Minería de datos&#41;](../../analysis-services/data-mining/model-filter-syntax-and-examples-analysis-services-data-mining.md)   
 [Prueba y validación &#40;minería de datos&#41;](../../analysis-services/data-mining/testing-and-validation-data-mining.md)  
  
  

