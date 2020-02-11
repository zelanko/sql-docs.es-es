---
title: Crear una estructura de minería de datos relacional | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- dimensions [Analysis Services], data mining
- data mining [Analysis Services], structure
- mining structures [Analysis Services], creating
- relational mining models [Analysis Services]
- OLAP mining models [Analysis Services]
ms.assetid: 5547d639-377d-4ca7-88fc-ce1f9e2babc5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d5dbf64a128cb21c7ac0e3d956a3dbdc6b320317
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66085380"
---
# <a name="create-a-relational-mining-structure"></a>Crear una estructura de minería de datos relacional
  La mayoría de los modelos de minería de datos se basan en orígenes de datos relacionales. Las ventajas de crear un modelo de minería de datos relacional son que puede reunir datos ad hoc y entrenar y actualizar un modelo sin la complejidad que supone crear un cubo.  
  
 Una estructura de minería de datos relacional puede extraer datos de orígenes dispares. Los datos sin procesar se pueden almacenar en tablas, archivos o sistemas de bases de datos relacionales, siempre y cuando los datos puedan definirse como parte de la vista del origen de datos. Por ejemplo, debe utilizar una estructura de minería de datos relacional si los datos están en Excel, en un almacén de datos de SQL Server, en la base de datos de informes de SQL Server o en los orígenes externos a los que se tiene acceso a través de los proveedores OLE DB u ODBC.  
  
 En este tema se proporciona información general sobre cómo utilizar el Asistente para minería de datos para crear una estructura de minería de datos relacional.  
  
 [Requisitos](#BKMK_Relational_Structure)  
  
 [Proceso para crear una estructura de minería de datos relacional](#BKMK_Relational_Structure)  
  
 [Cómo elegir orígenes de datos](#BKMK_ChooseRelData)  
  
 [Cómo especificar el tipo de contenido y el tipo de datos](#bkmk_ContentDataType)  
  
 [Por qué y cómo crear un conjunto de datos de exclusión](#bkmk_Holdout)  
  
 [Por qué y cómo habilitar la obtención de detalles](#BKMK_DrillThru)  
  
## <a name="requirements"></a>Requisitos  
 Primero, debe tener un origen de datos existente. Puede utilizar el Diseñador de origen de datos para configurar un origen de datos, si no existe ninguno. Para más información, vea [Crear un origen de datos &#40;SSAS multidimensional&#41;](../multidimensional-models/create-a-data-source-ssas-multidimensional.md).  
  
 A continuación, use el Asistente para vistas del origen de datos para ensamblar los datos requeridos en una única vista del origen de datos. Para más información sobre cómo seleccionar, transformar, filtrar o administrar datos con vistas del origen de datos, vea [Vistas del origen de datos en modelos multidimensionales](../multidimensional-models/data-source-views-in-multidimensional-models.md).  
  
##  <a name="BKMK_Relational_Structure"></a>Información general del proceso  
 Inicie el Asistente para minería de datos. Para hacerlo, haga clic con el botón derecho en el nodo **Estructuras de minería de datos** del Explorador de soluciones y seleccione **Agregar nueva estructura de minería de datos**. El asistente le guiará por los siguientes pasos para crear la estructura de un nuevo modelo de minería de datos relacional:  
  
1.  **Seleccionar el método de definición**: aquí se selecciona un tipo de origen de datos y se elige **desde la base de datos relacional o el almacenamiento de datos**.  
  
2.  **Crear la estructura de minería de datos**: Determine si va a compilar solo una estructura o una estructura con un modelo de minería de datos.  
  
     También debe elegir un algoritmo apropiado para el modelo inicial. Para obtener información sobre qué algoritmo es el mejor para ciertas tareas, vea [Algoritmos de minería de datos &#40;Analysis Services - Minería de datos&#41;](data-mining-algorithms-analysis-services-data-mining.md).  
  
3.  **Seleccionar vista del origen de datos**: elija una vista de orígenes de datos para utilizarla en el entrenamiento del modelo. La vista del origen de datos también puede contener los datos que se usan para las pruebas o datos no relacionados. Debe elegir qué datos se usan realmente en la estructura y en el modelo. También puede aplicar filtros a los datos después.  
  
4.  **Especificar tipos de tablas**: seleccione la tabla que contiene los casos usados para el análisis. Para algunos conjuntos de datos, especialmente los que se usan para generar modelos de cesta de compras, puede incluir también una tabla relacionada, para usarla como tabla anidada.  
  
     Para cada tabla, debe especificar la clave, de modo que el algoritmo sepa identificar un único registro y los registros relacionados si ha agregado una tabla anidada.  
  
     Para más información, consulte [Mining Structure Columns](mining-structure-columns.md).  
  
5.  **Especifique los datos de aprendizaje**: en esta página, elija como *tabla de casos*, que es la tabla que contiene los datos más importantes para el análisis.  
  
     En algunos conjuntos de datos, especialmente los que se usan para generar modelos de cesta de compras, puede incluir también una tabla relacionada. Los valores de esa tabla anidada se administran como varios valores que se relacionan con una única fila (o caso) en la tabla principal.  
  
6.  **Especificar el contenido y los tipos de datos de las columnas**: para cada columna que use en la estructura, debe elegir un *tipo de datos* y un *tipo de contenido*.  
  
     El asistente detectará automáticamente los posibles tipos de datos, pero no es necesario usar el tipo de datos recomendado por el asistente. Por ejemplo, incluso si los datos contienen números, podrían ser representativos de datos de categorías. A las columnas que especifique como claves se les asigna automáticamente el tipo de datos correcto para el tipo de modelo en concreto. Para más información, vea [Columnas del modelo de minería de datos](mining-model-columns.md) y [Tipos de datos &#40;Minería de datos&#41;](data-types-data-mining.md).  
  
     El *tipo de contenido* que elija para cada columna que use en el modelo indica al algoritmo cómo se deben procesar los datos.  
  
     Por ejemplo, podría decidir discretizar los números, en lugar de usar valores continuos. También puede ordenar el algoritmo para detectar automáticamente el mejor tipo de contenido para la columna. Para obtener más información, vea [Tipos de contenido &#40;minería de datos&#41;](content-types-data-mining.md).  
  
7.  **Crear conjunto de pruebas**: en esta página, puede indicar al asistente cuántos datos se deben reservar para su uso en la prueba del modelo. Si los datos admiten varios modelos, es aconsejable crear un conjunto de exclusión, para poder probar todos los modelos en los mismos datos.  
  
     Para obtener más información, vea [Prueba y validación &#40;minería de datos&#41;](testing-and-validation-data-mining.md).  
  
8.  **Finalización del asistente**: en esta página, asigne un nombre a la nueva estructura de minería de datos y al modelo de minería de datos asociado, y guarde la estructura y el modelo.  
  
     También puede establecer algunas opciones importantes, dependiendo del tipo de modelo. Por ejemplo, puede habilitar la obtención de detalles en la estructura.  
  
     En este momento, la estructura de minería de datos y su modelo son solo metadatos; tendrá que procesar ambos para obtener resultados.  
  
##  <a name="BKMK_ChooseRelData"></a>Cómo elegir datos relacionales  
 Las estructuras de minería de datos relacionales pueden estar basadas en cualquier dato que esté disponible mediante un origen de datos OLE DB. Si los datos del origen se encuentran en varias tablas, puede usar una vista del origen de datos para reunir las tablas y las columnas que necesita en un solo lugar.  
  
 Si las tablas incluyen cualquier relación de uno a varios (por ejemplo, si tiene varios registros de compra para cada cliente que desea analizar), puede Agregar ambas tablas y, a continuación, utilizar una tabla como la tabla de casos, vinculando los datos del lado de varios de la relación como un tabla anidada.  
  
 Los datos de una estructura de minería de datos se derivan de lo que haya en una vista del origen de datos existente. Puede modificar los datos a medida que los necesite en la vista del origen de datos, agregando relaciones o columnas derivadas que podrían no estar presentes en los datos relacionales subyacentes. También puede crear cálculos o agregaciones con nombre en la vista del origen de datos. Estas características son muy prácticas si no tiene el control sobre la disposición de los datos en el origen de datos o si desea experimentar con agregaciones diferentes de los datos para los modelos de minería de datos.  
  
 No tiene que utilizar todos los datos disponibles; puede escoger y elegir qué columnas desea incluir en la estructura de minería de datos. Todos los modelos que están basados en esa estructura se pueden utilizar entonces en esas columnas o se pueden marcar determinadas columnas como `Ignore` para un modelo determinado. Puede permitir a los usuarios de un modelo de minería de datos explorar en profundidad los resultados del modelo para ver columnas adicionales de la estructura de minería de datos que no se incluyeron en el propio modelo de minería de datos.  
  
##  <a name="bkmk_ContentDataType"></a>Cómo especificar el tipo de contenido y el tipo de datos  
 El tipo de datos es más o menos igual que los tipos de datos que se especifican en SQL Server o en otras interfaces de aplicación: fechas y horas, números de diferentes tamaños, valores booleanos, texto y otros datos discretos.  
  
 Sin embargo, los tipos de contenido son importantes para la minería de datos y afectan al resultado del análisis. El tipo de contenido indica al algoritmo lo que debería hacer con los datos: ¿deben tratarse los números en una escala continua o de datos discretos? ¿Cuántos valores posibles hay? ¿Es distinto cada valor? Si el valor es una clave, ¿qué tipo de clave es? indica que se trata de un valor de fecha y hora, una secuencia o algún otro tipo de clave?  
  
 Tenga en cuenta que la opción de tipo de datos puede restringir la opción de tipos de contenido. Por ejemplo, no puede discretizar los valores que no sean numéricos. Si no puede ver el tipo de contenido que desea, puede hacer clic en **Atrás** para volver a la página de tipo de datos y probar un tipo de datos diferente.  
  
 No tiene que preocuparse demasiado de obtener el tipo de contenido incorrecto. Es muy fácil crear un modelo nuevo y cambiar el tipo de contenido del modelo, siempre que el tipo de datos establecido en la estructura de minería de datos admita el tipo de contenido. También es muy común crear varios modelos utilizando varios tipos de contenido, como experimento, o para cumplir los requisitos de un algoritmo diferente.  
  
 Por ejemplo, si los datos contienen una columna de ingresos puede crear diferentes modelos con el algoritmo de árboles de decisión de Microsoft y configurar la columna alternativamente como dos números continuos o como intervalos discretos. Sin embargo, si agregó un modelo utilizando el algoritmo Bayes Naïve de Microsoft, le forzarían a cambiar la columna a valores de datos discretos, solo porque el algoritmo no admite números continuos.  
  
##  <a name="bkmk_Holdout"></a>Por qué y cómo dividir los datos en conjuntos de entrenamiento y de prueba  
 Casi al final del asistente, debe decidir si dividir los datos en conjuntos de entrenamiento y de pruebas. La posibilidad de aprovisionar una parte muestreada al azar de los datos para la prueba resulta muy cómoda, ya que garantiza que un conjunto conjunto de datos de prueba coherente esté disponible para usarse con todos los modelos de minería de datos asociados a la nueva estructura de minería de datos.  
  
> [!WARNING]  
>  Observe que esta opción no está disponible para todos los tipos de modelos. Por ejemplo, si crea un modelo de pronóstico, no podrá usar la exclusión, porque el algoritmo de serie temporal requiere que no haya huecos en los datos. Para consultar una lista de los tipos de modelo compatibles con los conjuntos de datos de exclusión, vea [Conjuntos de datos de entrenamiento y de prueba](training-and-testing-data-sets.md).  
  
 Para crear este conjunto de datos de exclusión, se especifica el porcentaje de los datos que se desea utilizar para las pruebas. El resto de los datos se utilizarán para el entrenamiento. Opcionalmente, puede establecer un número máximo de casos para las pruebas o establecer un valor de inicialización para utilizarlos al iniciar el proceso de selección aleatoria.  
  
 La definición del conjunto de prueba de exclusión se almacena junto con la estructura de minería de datos, para que siempre que cree un nuevo modelo basado en la estructura, el conjunto de datos de pruebas esté disponible para evaluar la precisión del modelo. Si elimina la memoria caché de la estructura de minería de datos, la información acerca de los casos que se utilizaron para el entrenamiento y los que se usaron para las pruebas se eliminará también.  
  
##  <a name="BKMK_DrillThru"></a>Por qué y cómo habilitar la obtención de detalles  
 Casi al final del asistente, tiene la opción de habilitar la *obtención de detalles*. Es fácil pasar por alto esta opción, pero es importante. La obtención de detalles le permite ver los datos de origen en la estructura de minería de datos si consulta el modelo de minería de datos.  
  
 ¿Por qué es esto útil? Supongamos que está viendo los resultados de un modelo de agrupación en clústeres y desea ver los clientes que se colocarán en un clúster concreto. Mediante la obtención de detalles, puede ver detalles como la información de contacto.  
  
> [!WARNING]  
>  Para utilizar la obtención de detalles, debe habilitarla al crear la estructura de minería de datos. Puede habilitar la obtención de detalles en los modelos después, estableciendo una propiedad en el modelo, pero las estructuras de minería de datos requieren que esta opción se establezca al principio. Para obtener más información, vea [Consultas de obtención de detalles &#40;minería de datos&#41;](drillthrough-queries-data-mining.md).  
  
## <a name="see-also"></a>Consulte también  
 [Diseñador de minería de datos](data-mining-designer.md)   
 [Asistente para minería de datos &#40;Analysis Services:&#41;de minería de datos](data-mining-wizard-analysis-services-data-mining.md)   
 [Propiedades del modelo de minería de datos](mining-model-properties.md)   
 [Propiedades de las columnas de estructura y estructura de minería de datos](properties-for-mining-structure-and-structure-columns.md)   
 [Tareas y procedimientos de las estructuras de minería de datos](mining-structure-tasks-and-how-tos.md)  
  
  
