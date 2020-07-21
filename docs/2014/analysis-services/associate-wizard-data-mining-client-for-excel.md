---
title: Asistente para Asociación (cliente de minería de datos para Excel) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- nested tables, in association models
- association [data mining]
ms.assetid: 4db6462f-93c7-443f-8ff7-39474dc7029e
author: minewiskan
ms.author: owend
ms.openlocfilehash: 52542ac1b15b59ecebca4ea26ba530298157ed50
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/08/2020
ms.locfileid: "84527948"
---
# <a name="associate-wizard-data-mining-client-for-excel"></a>Asistente para asociación (Cliente de minería de datos para Excel)
  ![Asistente para asociación, cinta de opciones Minería de datos](media/dmc-associate.gif "Asistente para asociación, cinta de opciones Minería de datos")  
  
 El Asistente para asociación le permite crear un modelo de minería de datos mediante el algoritmo de reglas de asociación de [!INCLUDE[msCoName](../includes/msconame-md.md)]. Estos modelos de minería de datos son especialmente útiles para crear *sistemas de recomendaciones*.  
  
 El algoritmo Reglas de asociación de [!INCLUDE[msCoName](../includes/msconame-md.md)] recorre un conjunto de datos compuesto de transacciones o de eventos y busca las combinaciones que suelen aparecen juntas. Puede haber muchos miles de combinaciones pero el algoritmo puede personalizar para buscar más o menos, y para conservar solo las combinaciones más probables.  
  
 Puede aplicar análisis de asociación a varios problemas. La aplicación más popular de este método es el análisis de la cesta de la compra, que busca productos individuales que se suelen comprar juntos a menudo. Puede utilizar esa información para recomendar productos a los clientes basándose en los elementos que han comprado previamente.  
  
## <a name="using-the-associate-wizard"></a>Usar el Asistente para asociación  
  
1.  En la cinta de opciones **minería de datos** , haga clic en **asociar**.  
  
2.  En la página **seleccionar datos de origen** , elija una tabla o un intervalo de datos de Excel y haga clic en **siguiente**.  
  
     El libro de datos de ejemplo contiene un ejemplo, en la pestaña Asociado, de cómo los datos de la transacción se organizan normalmente si, por ejemplo, tiene varios productos en cada transacción o varios registros de compra por cada cliente que desea analizar.  
  
     Si desea utilizar datos externos para crear un modelo de asociación mediante el Asistente para asociar, primero debe agregar los datos a Excel y *aplanar* los datos. Para obtener más información sobre cómo preparar los datos para el modelado de asociaciones, vea [tablas anidadas &#40;Analysis Services-Data Mining&#41;](data-mining/nested-tables-analysis-services-data-mining.md)en libros en pantalla de SQL Server.  
  
3.  En la página **Asociación** , elija la columna que identifica la transacción.  
  
     Para los modelos de cesta de la compra, este identificador representa la unidad que desea modelar. ¿Desea analizar los elementos que clientes particulares han comprado a lo largo del tiempo o desea analizar varias transacciones que implican a varios clientes? En el primer caso, elegirá el identificador del cliente; en el último elegirá el pedido de compra u otro identificador de transacción.  
  
4.  En **elemento**, seleccione la columna que contiene los elementos entre los que necesita buscar asociaciones.  
  
     Por ejemplo, en un modelo de cesta de la compra, elegiría un campo de productos, para analizar qué productos se suelen comprar a menudo. Si hay demasiados productos individuales para correlacionarlos de forma eficaz, puede elegir una categoría de producto o un campo de subcategoría.  
  
5.  En **umbrales**, puede establecer los valores que controlan o afectan a la salida del modelo:  
  
    -   **Compatibilidad mínima.** Especifica cuántas veces debe aparecer un grupo de elementos para que se considere importante. El algoritmo omitirá cualquier combinación de elementos que no cumpla este criterio. Por ejemplo, puede que desee ver solo los conjuntos de elementos en el que los elementos aparecían juntos al menos 10 veces en total.  
  
    -   **Probabilidad de regla mínima**. Especifica el valor de la probabilidad mínima necesaria para que una regla se guarde. Se analiza el conjunto de datos completo para buscar todas las combinaciones y entonces se calcula la probabilidad. Si este umbral es bajo, el asistente podría asociar elementos que sólo están relativamente relacionados. Si este umbral es demasiado alto, podrían omitirse algunas asociaciones por no tener suficientes datos de compatibilidad.  
  
     En general, cambiar estos valores tiene los efectos siguientes:  
  
    -   Si reduce el valor de la compatibilidad, aumenta el número de combinaciones encontradas.  
  
    -   Si reduce la compatibilidad máxima, se filtran elementos que se producen con tanta frecuencia que son poco significativos.  
  
    -   Si reduce la probabilidad de una regla, reduce los requisitos que debe cumplir una combinación para que se considere importante en el contexto del conjunto completo de datos.  
  
     **Sugerencia:** Es una buena idea crear varios modelos de minería de datos mediante combinaciones diferentes de compatibilidad y probabilidad. Para realizar un seguimiento de la configuración utilizada para cada modelo, puede utilizar el Asistente para **documentar modelo** , disponible en el cliente de minería de datos para Excel, y usar la opción de informe **detallado** . Para obtener más información, vea [documentar modelos de minería de datos &#40;complementos de minería de datos para Excel&#41;](documenting-mining-models-data-mining-add-ins-for-excel.md).  
  
6.  Opcionalmente, haga clic en **parámetros** para cambiar los parámetros del algoritmo y personalizar el comportamiento del modelo de minería de datos.  
  
     El cuadro de diálogo Parámetros de algoritmo incluye todos los parámetros que establezca en el asistente, más algunos que son de uso menos frecuente, como MAXIMUM_SUPPORT. Para obtener información sobre cómo usar estos parámetros, consulte [referencia técnica del algoritmo de Asociación de Microsoft](data-mining/microsoft-association-algorithm-technical-reference.md).  
  
7.  En la página **Finalizar** , escriba un nombre único para el conjunto de datos y el modelo.  
  
8.  En **Opciones**, puede definir cómo desea trabajar con el modelo una vez completado:  
  
    -   **Examinar**.  Cuando el modelo está listo, el asistente abre una ventana que muestra las reglas, los conjuntos de elementos y un gráfico de red de dependencias que ilustra las asociaciones.  
  
         Para obtener más información sobre cómo interpretar los datos en el visor de modelos de asociación, vea [examinar un modelo de reglas de asociación](browsing-an-association-rules-model.md).  
  
    -   **Habilitar la obtención de detalles**. Seleccione esta opción para obtener acceso a los datos subyacentes, a través del modelo.  
  
         La obtención de detalles es útil, por ejemplo, si desea hacer clic en un conjunto de elementos determinado y ver los datos de origen.  
  
    -   **Usar modelo temporal**. Seleccione esta opción si no desea que el modelo se guarde en el servidor. Se eliminan los modelos temporales al cerrar Excel.  
  
9. El asistente analiza todas las combinaciones posibles y crea un informe que contiene conjuntos de elementos y reglas.  
  
## <a name="more-about-association-models"></a>Más información sobre los modelos de asociación  
 El algoritmo de reglas de asociación de [!INCLUDE[msCoName](../includes/msconame-md.md)] examina los datos de entrenamiento para encontrar elementos que aparecen juntos en una transacción. Cada grupo de elementos *constituye un conjunto*de elementos. A continuación, el algoritmo cuenta el número de veces que aparece cada conjunto de elementos y calcula importancia relativa de cada uno de ellos en todas las transacciones.  
  
 El algoritmo usa esta información sobre los conjuntos de elementos para generar reglas que se puedan usar para predecir asociaciones o realizar recomendaciones. Por ejemplo, una regla podría ser "si el usuario ha comprado un libro de Autor 1 y un libro de Autor 2, es probable que el usuario compre también un libro de Autor 3". A cada recomendación se le asigna una probabilidad en función de la solidez de las asociaciones.  
  
### <a name="requirements"></a>Requisitos  
 Para usar el Asistente para asociación, debe estar conectado a una base de datos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 Los datos de origen deben estar organizados como una tabla de transacciones. Los datos de origen deben contener una columna con el identificador de la transacción. Esta columna identifica cada grupo de elementos. Esta columna de transacción debe mantener una relación de uno a varios con una segunda columna, el Id. de elemento, que almacena los nombres o números de Id. de los elementos individuales del grupo.  
  
 Conceptualmente, esto puede comprenderse más fácilmente si se recupera el ejemplo de la cesta de la compra. Si a la cesta de la compra se le asigna un identificador, el identificador de cesta de la compra sirve como identificador de la transacción. Cada elemento de la cesta de la compra, como patatas o leche, es un miembro de la transacción. El algoritmo de asociación puede hacer el seguimiento de los elementos entre transacciones: por ejemplo, para determinar cuántas veces aparecen dentro de cada transacción los elementos patatas y leche.  
  
 Los datos de origen se deben ordenar por la columna del identificador de la transacción.  
  
## <a name="see-also"></a>Consulte también  
 [Crear un modelo de minería de datos](creating-a-data-mining-model.md)   
 [Examinar un modelo de reglas de asociación](browsing-an-association-rules-model.md)   
 [Análisis de la cesta de compras &#40;tabla análisis para Excel&#41;](shopping-basket-analysis-table-analysistools-for-excel.md)   
 [Tutorial de diagrama de red de dependencias &#40;complementos de minería de datos&#41;](dependency-network-diagram-walkthrough-data-mining-add-ins.md)  
  
  
