---
title: 'Asistente para minería de datos (Analysis Services: minería de datos) | Documentos de Microsoft'
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- dimensions [Analysis Services], data mining
- OLAP [Analysis Services], mining models
- Data Mining Wizard
- relational mining models [Analysis Services]
ms.assetid: d5fea90f-5f38-4639-8851-7707f6606a12
caps.latest.revision: 56
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 49b3ecb1f8cc1bb63344b201145f9d6639aace89
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36199790"
---
# <a name="data-mining-wizard-analysis-services---data-mining"></a>Asistente para minería de datos (Analysis Services - Minería de datos)
  El Asistente para minería de datos de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] se ejecuta cada vez que se agrega una nueva estructura de minería de datos a un proyecto de minería de datos. El asistente le ayuda a elegir un origen de datos y a configurar una vista del origen de datos que defina los datos que se van a utilizar para el análisis, y luego le ayuda a crear un modelo inicial.  
  
 En la fase final del asistente, si lo desea puede dividir los datos en conjuntos de entrenamiento y de prueba, y habilitar características como la obtención de detalles.  
  
## <a name="what-to-know-before-you-start"></a>Qué hay que saber antes de empezar  
 Esto es lo que necesita saber antes de iniciar el asistente.  
  
-   Si va a generar los modelos y la estructura de minería de datos desde una base de datos relacional o desde un cubo existente de una base de datos OLAP.  
  
-   ¿Qué columnas contienen las claves que identifican de forma exclusiva un registro de caso?  
  
-   ¿Qué columnas o atributos desea utilizar para la predicción? ¿Qué columnas o atributos es apropiado utilizar como entrada para el análisis?  
  
-   ¿Qué algoritmo debe utilizar? Los algoritmos proporcionados en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tienen características diferentes y generan resultados distintos. Por suerte, no está limitado a un modelo para cada conjunto de datos, de modo que puede experimentar agregando modelos diferentes.  
  
-   ¿Necesita poder probar sus modelos en un conjunto de datos unificado? Si es así, se recomienda utilizar la opción de apartar algunos datos para realizar pruebas. Puede elegir un porcentaje y limitarlo con un número especificado de filas, si lo desea.  
  
##  <a name="BKMK_Using_DM_Wizard"></a> Iniciar el Asistente para minería de datos  
 Para utilizar el Asistente para minería de datos, debe haber iniciado una solución en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] que contenga al menos un proyecto OLAP o de minería de datos.  
  
-   Si la solución está lista para la minería de datos, basta con que haga clic con el botón derecho en el nodo **Estructuras de minería de datos** en el explorador de soluciones y seleccione **Nueva estructura de minería de datos** para iniciar el asistente.  
  
-   Si la solución no contiene ningún proyecto existente, puede agregar un nuevo proyecto de minería de datos. En el menú **Archivo** , seleccione **Nuevo**y haga clic en **Proyecto**. Asegúrese de elegir la plantilla **Proyecto multidimensional y de minería de datos de Analysis Services**.  
  
-   También puede utilizar el Asistente para la importación de Analysis Services para obtener los metadatos de una solución de minería de datos existente. Sin embargo, no puede seleccionar objetos individuales para importarlos; se importa toda la base de datos, incluidos los cubos, las vistas del origen de datos, etc.). Observe también que la nueva solución que se crea mediante la importación se configura automáticamente para usar la base de datos predeterminada local. Deberá cambiar esto por otra instancia para poder procesar o examinar los objetos, y si va a importar desde una versión anterior de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], puede que tenga que actualizar las referencias a los proveedores.  
  
 A continuación, creará un modelo de minería de datos asociado y la estructura de minería de datos. También puede crear solo la estructura de minería de datos y agregar modelos después, pero normalmente es más fácil crear un modelo de prueba primero.  
  
###  <a name="BKMK_Relational"></a> Soluciones relacionales y. modelos OLAP de minería de datos  
 La siguiente opción importante que tiene es si se debe usar un origen de datos relacional o basar el modelo en los datos multidimensionales (OLAP).  
  
 El Asistente para minería de datos se bifurca en dos caminos en este momento, en función de si el origen de datos es relacional o está en un cubo. Todo lo demás excepto el proceso de selección de los datos es igual: la elección de los algoritmo, la capacidad agregar un conjunto de exclusión, etc. Pero la selección de los datos del cubo es un poco más compleja que con los datos relacionales. (También obtiene algunas opciones adicionales al final si crea un modelo basado en un cubo).  
  
 Vea los siguientes temas para obtener un tutorial de cada opción con más detalle:  
  
 [Crear una estructura de minería de datos relacional](create-a-relational-mining-structure.md)  
 Le dirige a través de las decisiones que toma al generar un modelo de minería de datos relacional.  
  
 [Crear una estructura de minería de datos OLAP](create-an-olap-mining-structure.md)  
 Describe las opciones y las selecciones adicionales que debe realizar al elegir los datos de un cubo OLAP.  
  
> [!NOTE]  
>  No necesita tener un cubo o una base de datos OLAP para realizar minería de datos. A menos que los datos ya estén almacenados en un cubo o desee minar las dimensiones OLAP o los resultados de agregaciones o cálculos OLAP, se recomienda usar una tabla relacional o un origen de datos para la minería de datos.  
  
### <a name="choosing-an-algorithm"></a>Elegir un algoritmo  
 A continuación, debe decidir qué algoritmo utilizar en el procesamiento de los datos. Esta decisión puede ser difícil de tomar. Cada algoritmo proporcionado en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tiene características diferentes y produce resultados distintos, de modo que puede experimentar y probar varios modelos antes de determinar cuál es el más adecuado para sus datos y su problema empresarial. Vea el tema siguiente para obtener una explicación de las tareas en las que cada algoritmo es más adecuado:  
  
 [Algoritmos de minería de datos &#40;Analysis Services: minería de datos&#41;](data-mining-algorithms-analysis-services-data-mining.md)  
  
 De nuevo, puede crear varios modelos utilizando algoritmos diferentes o cambiar los parámetros de los algoritmos para crear modelos distintos. No está limitado en su elección de algoritmo y es recomendable crear varios modelos con los mismos datos.  
  
### <a name="define-the-data-used-for-modeling"></a>Definir los datos utilizados para el modelado  
 Además de elegir los datos de un origen, debe especificar cuál de la tabla de la vista del origen de datos contiene los *datos de caso*. La tabla de casos se utilizará para entrenar el modelo de minería de datos y, por tanto, debe contener las entidades que desea analizar: por ejemplo, clientes y su información demográfica. Cada caso debe ser único y debe ser identificable mediante una *clave de caso*.  
  
 Además de especificar la tabla de casos, puede incluir *tablas anidadas* en los datos. Normalmente, una tabla anidada contiene información adicional sobre las entidades de la tabla de casos, como las transacciones realizadas por el cliente o los atributos que tienen una relación de varios a uno con la entidad. Por ejemplo, una tabla anidada combinada con la tabla de casos **Customers** puede incluir una lista de los productos comprados por cada cliente. En un modelo que analiza el tráfico a un sitio Web, la tabla anidada podría incluir scripts de páginas que el usuario visitó. Para más información, vea [Tablas anidadas &#40;Analysis Services - Minería de datos&#41;](nested-tables-analysis-services-data-mining.md).  
  
### <a name="additional-features"></a>Características adicionales  
 Para ayudarle a elegir los datos correctos y a configurar los orígenes de datos correctamente, el Asistente para minería de datos proporciona estas características adicionales:  
  
-   **Detección automática de tipos de datos**: el asistente examinará la exclusividad y la distribución de los valores de columna y después recomendará el mejor tipo de datos, y sugerirá un tipo de uso para estos. Puede invalidar estas sugerencias seleccionando los valores de una lista.  
  
-   **Sugerencias para las variables**: puede hacer clic en un cuadro de diálogo e iniciar un analizador que calcule las correlaciones entre las columnas incluidas en el modelo y determine si las columnas son predicciones probables del atributo de resultados, dado el modelo hasta el momento. Puede invalidar estas sugerencias escribiendo valores diferentes.  
  
-   **Selección de características**: la mayoría de los algoritmos detectarán automáticamente las columnas que son adecuadas para la predicción y usará esas de forma preferente. En las columnas que contienen demasiados valores, se aplicará la *selección de características* para reducir la cardinalidad de los datos y mejorar las posibilidades de buscar un patrón significativo. Puede modificar el comportamiento de la selección de características mediante parámetros del modelo.  
  
-   **Segmentación automática del cubo**: si el modelo de minería de datos se basa en un origen de datos OLAP, la capacidad para segmentar el modelo utilizando atributos de cubo se proporciona automáticamente. Es recomendable para los modelos de empaquetamiento basados en los subconjuntos de datos de cubo.  
  
### <a name="completing-the-wizard"></a>Finalizar el Asistente  
 El último paso del asistente es dar nombre a la estructura de minería de datos y al modelo asociado. Según el tipo de modelo que creó, podría tener las siguientes opciones importantes:  
  
-   Si selecciona **Permitir obtención de detalles**, la funcionalidad de *obtención de detalles* se habilita en el modelo. Con la obtención de detalles, los usuarios que tengan los permisos adecuados podrán explorar los datos de origen que se utilizan para generar el modelo.  
  
-   Si crea un modelo de OLAP, puede seleccionar las opciones **Crear un cubo de minería de datos**o **Crear una dimensión de minería de datos**. Ambas opciones facilitan el examen del modelo completo y la obtención de detalles en los datos subyacentes.  
  
 Después de completar el Asistente para minería de datos, puede utilizar el Diseñador de minería de datos para modificar la estructura y los modelos de minería de datos, ver la precisión del modelo, ver las características de la estructura y de los modelos, o realizar predicciones utilizando los modelos.  
  
 [Volver al principio](#BKMK_Using_DM_Wizard)  
  
## <a name="related-content"></a>Contenido relacionado  
 Para obtener más información sobre las decisiones que debe tomar al crear un modelo de minería de datos, vea los vínculos siguientes:  
  
 [Algoritmos de minería de datos &#40;Analysis Services: minería de datos&#41;](data-mining-algorithms-analysis-services-data-mining.md)  
  
 [Tipos de contenido &#40;minería de datos&#41;](content-types-data-mining.md)  
  
 [Tipos de datos &#40;minería de datos&#41;](data-types-data-mining.md)  
  
 [Selección de características &#40;minería de datos&#41;](feature-selection-data-mining.md)  
  
 [Los valores que faltan &#40;Analysis Services: minería de datos&#41;](missing-values-analysis-services-data-mining.md)  
  
 [Obtención de detalles en modelos de minería de datos](drillthrough-on-mining-models.md)  
  
## <a name="see-also"></a>Vea también  
 [Herramientas de minería de datos](data-mining-tools.md)   
 [Soluciones de minería de datos](data-mining-solutions.md)  
  
  