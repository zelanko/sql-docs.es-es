---
title: Crear una estructura de minería de datos OLAP | Documentos de Microsoft
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2a4721bf42a3c223905d982e8be6a470983beb06
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="create-an-olap-mining-structure"></a>Crear una estructura de minería de datos OLAP
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  La creación de un modelo de minería de datos basado en un cubo OLAP o en otro almacén de datos multidimensionales presenta numerosas ventajas. Una solución OLAP ya contiene enormes cantidades de datos que han sido bien organizados, limpiados y con un formato correcto; sin embargo, su complejidad es tal que es poco probable que los usuarios encuentren patrones significativos para la exploración ad hoc. La minería de datos permite detectar nuevas correlaciones y proporcionar una visión general práctica.  
  
 En este tema se describe cómo crear una estructura de minería de datos OLAP, en función de una dimensión y de las medidas relacionadas en una solución MDX existente.  
  
 [Requisitos](#bkmk_Reqs)  
  
 [Información general sobre el proceso de minería de datos OLAP](#bkmk_Overview)  
  
 [Escenarios para utilizar minería de datos en soluciones OLAP](#bkmk_OLAP_Scenarios)  
  
 [Filtros](#bkmk_Filters)  
  
 [Usae tablas anidadas](#bkmk_Nested)  
  
 [Dimensiones de minería de datos](#bkmk_DMDimension)  
  
##  <a name="bkmk_Reqs"></a> Requisitos para los modelos y la estructura de minería de datos OLAP  
 Si va a diseñar un modelo de minería de datos OLAP, el origen de datos ya existe en la base de datos que se usó para generar el cubo. No puede conectarse a un cubo remoto y generar objetos de minería de datos; los objetos del cubo deben estar disponibles dentro de la misma solución que la base de datos con la estructura de minería de datos que se creará.  
  
 Si no tiene los archivos de proyecto originales o no quiere modificarlos, puede usar la opción de Visual Studio **Importar del servidor (multidimensional y minería de datos)** para obtener una copia de los metadatos y los objetos de la solución. Puede modificar el destino de la implementación, modificar los orígenes de datos y trabajar con los objetos de cubo sin afectar a los objetos existentes.  
  
 Para obtener más información, vea [Importar un proyecto de minería de datos mediante el Asistente para la importación de Analysis Services](../../analysis-services/data-mining/import-a-data-mining-project-using-the-analysis-services-import-wizard.md).  
  
##  <a name="bkmk_Overview"></a> Información general sobre el proceso de minería de datos OLAP  
 Inicie el Asistente para minería de datos haciendo clic con el botón derecho en el nodo **Estructuras de minería de datos** del Explorador de soluciones y seleccionando  **Nueva estructura de minería de datos**. El asistente le guiará por los siguientes pasos para crear la estructura de una nueva estructura y modelo:  
  
1.  **Seleccionar el método de definición**: aquí se selecciona un tipo de origen de datos. Elija **A partir de un cubo existente**.  
  
    > [!NOTE]  
    >  El cubo OLAP que se utiliza como origen debe existir en la misma base de datos que la estructura de minería de datos, como se ha descrito anteriormente. Además, no puede usar un cubo creado con el complemento de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para Excel como origen de la minería de datos.  
  
2.  **Crear la estructura de minería de datos**: determina si se creará solo una estructura o una estructura con un modelo de minería de datos.  
  
     También debe elegir un algoritmo apropiado para analizar los datos. Para obtener instrucciones sobre qué algoritmo es más idóneo para determinadas tareas, consulte HYPERLINK "ms-help://SQL111033/as_1devconc/html/ed1fc83b-b98c-437e-bf53-4ff001b92d64.htm" Algoritmos de minería de datos (Analysis Services: Minería de datos).  
  
3.  **Seleccionar la dimensión de cubo de origen**: este paso es igual que la selección de un origen de datos. Debe elegir una sola dimensión que contenga los datos más importantes usados para entrenar el modelo. Puede agregar datos de otras dimensiones más adelante o filtrar la dimensión.  
  
4.  **Seleccionar la clave de caso**: en la dimensión recién seleccionada, elija un atributo (columna) para que sirva como el identificador único de los datos del caso.  
  
     Generalmente, se seleccionará una columna automáticamente pero puede cambiarla si de hecho hay varias claves.  
  
5.  **Seleccionar columnas de nivel de caso**: aquí se eligen los atributos de la dimensión seleccionada y otras medidas relacionadas, que son pertinentes para el análisis. Este paso es equivalente a seleccionar columnas de una tabla.  
  
     El asistente incluye automáticamente cualquier medida que se creara usando los atributos de la dimensión seleccionada para que los revise y seleccione.  
  
     Por ejemplo, si un cubo contiene una medida que calcula el costo de carga según la ubicación geográfica del cliente y elige la dimensión Customer como origen de datos principal para el modelado, la medida se propondrá como candidata para agregar al modelo. Tenga cuidado de no agregar demasiadas medidas que ya se basen directamente en atributos, ya que hay una relación implícita entre las columnas, según se defina en la fórmula de la medida, y el nivel de esta correlación esperada puede ocultar otras relaciones que podría detectar de otro modo.  
  
6.  **Especificar el uso de las columnas del modelo de minería**: para cada atributo o medida que haya agregado a la estructura, debe especificar si el atributo se debe utilizar para la predicción o utilizar como entrada. Si no selecciona alguna de estas opciones, los datos se procesarán pero no se usarán para el análisis; sin embargo, estarán disponibles como datos de fondo en el caso de que habilite más tarde la obtención de detalles.  
  
7.  **Agregar tablas anidadas**: haga clic aquí para agregar tablas relacionadas. En el cuadro de diálogo **Seleccionar una dimensión de grupo de medida** , puede elegir una sola dimensión entre las dimensiones relacionadas con la actual.  
  
     A continuación, use el cuadro de diálogo **Seleccionar una columna de clave de tabla anidada** para definir el modo en que la nueva dimensión se relaciona con la dimensión que contiene los datos de caso.  
  
     Utilice el cuadro de diálogo **Seleccionar las columnas de la tabla anidada** para elegir los atributos y las medidas de la nueva dimensión que desea usar en el análisis. También debe especificar si el atributo anidado se utilizará para la predicción.  
  
     Después de agregar todos los atributos anidados que podría necesitar, vuelva a la página **Especificar el uso de las columnas del modelo de minería**y haga clic **Siguiente**.  
  
8.  **Especificar el contenido de las columnas y el tipo de datos**: hasta este momento, ha agregado todos los datos que se utilizarán para el análisis y debe especificar el *tipo de datos* y el *tipo de contenido* de cada atributo.  
  
     En un modelo OLAP, no tiene la opción de detectar automáticamente los tipos de datos, porque el tipo de datos ya está definido por la solución multidimensional y no se puede cambiar. Las claves también se identifican de modo automático. Para obtener más información, vea [Tipos de datos &#40;minería de datos&#41;](../../analysis-services/data-mining/data-types-data-mining.md).  
  
     El *tipo de contenido* que elija para cada columna que use en el modelo indica al algoritmo cómo se deben procesar los datos. Para obtener más información, vea [Tipos de contenido &#40;minería de datos&#41;](../../analysis-services/data-mining/content-types-data-mining.md).  
  
9. **Segmentar el cubo de origen**: aquí puede definir filtros en un cubo para seleccionar solo un subconjunto de los datos y para entrenar los modelos que sean más apropiados.  
  
     Para filtrar un cubo, elija la dimensión que desea filtrar, seleccione el nivel de la jerarquía que contiene los criterios que desea utilizar y después escriba la condición que se usará como filtro.  
  
10. **Crear conjunto de pruebas**: en esta página, puede indicar al asistente cuántos datos deben guardarse para usarse en la prueba del modelo. Si los datos admiten varios modelos, es aconsejable crear un conjunto de exclusión, para poder probar todos los modelos en los mismos datos.  
  
     Para obtener más información, vea [Prueba y validación &#40;minería de datos&#41;](../../analysis-services/data-mining/testing-and-validation-data-mining.md).  
  
11. **Finalización del asistente**: en esta página, proporcione un nombre a la estructura de minería de datos y al modelo de minería de datos asociado, y guarde la estructura y el modelo.  
  
     En esta página también puede establecer las siguientes opciones:  
  
    -   **Permitir la obtención de detalles**  
  
    -   **Crear dimensión de modelo de minería de datos**  
  
    -   **Crear el cubo con la dimensión del modelo de minería de datos**  
  
     Para obtener más información acerca de estas opciones, vea la sección más adelante en este tema, [Descripción de las dimensiones de minería de datos y obtención de detalles](#bkmk_DMDimension).  
  
 En este momento, la estructura de minería de datos y su modelo son solo metadatos; tendrá que procesar ambos para obtener resultados.  
  
##  <a name="bkmk_OLAP_Scenarios"></a> Escenarios para usar minería de datos con datos OLAP  
 Los cubos OLAP suelen contener tantos miembros y dimensiones que puede resultar complicado saber dónde comenzar con la minería de datos. Para ayudar a identificar los patrones que contienen los cubos, normalmente se identifica una única dimensión de interés y, a continuación, se empieza a explorar patrones relacionados con dicha dimensión. En la siguiente tabla se enumeran varias tareas de minería de datos OLAP habituales, se describen casos de ejemplo en los que podría aplicar cada tarea y se identifica el algoritmo de minería de datos que se debe utilizar para cada tarea.  
  
|Tarea|Caso de ejemplo|Algoritmo|  
|----------|---------------------|---------------|  
|Agrupar miembros en clústeres|Segmentar una dimensión de cliente en función de las propiedades de miembro del cliente, los productos que éste adquiere cliente y la cantidad de dinero que gastan los clientes.|Algoritmo de clústeres de [!INCLUDE[msCoName](../../includes/msconame-md.md)]|  
|Buscar miembros interesantes o anómalos|Identificar tiendas interesantes o anómalas en una dimensión de tiendas basada en ventas, beneficios, ubicación de la tiendas y tamaño.|Algoritmo de árboles de decisión de [!INCLUDE[msCoName](../../includes/msconame-md.md)]|  
|Buscar celdas interesantes o anómalas|Identificar ventas en tiendas que no siguen las tendencias habituales en un período de tiempo.|[!INCLUDE[msCoName](../../includes/msconame-md.md)]Algoritmo de serie temporal|  
|Buscar correlaciones|Identifique los factores que están relacionados con el tiempo de inactividad del servidor, como la región, el tipo de equipo, el sistema operativo o la fecha de compra.|[!INCLUDE[msCoName](../../includes/msconame-md.md)]Algoritmo Naïve Bayes|  
  
##  <a name="bkmk_Filters"></a>Segmentar un cubo frente a. Modelos de filtrado  
 Segmentar el cubo mientras crea un modelo es igual que crear un filtro en un modelo de minería de datos relacional. En un modelo relacional, el filtro en el origen de datos se define como una cláusula WHERE en una instrucción SQL; en un cubo, se usa el editor para crear instrucciones de filtro mediante MDX.  
  
 Por ejemplo, un cubo podría contener información sobre la compra de productos en todo el mundo pero, para su campaña de marketing, desea crear un modelo basado en el análisis de clientes femeninos de 30 años que viven en el Reino Unido.  
  
 En este escenario, creará dos filtros:  
  
-   Para el primer filtro, elegiría la dimensión Geography, la jerarquía Region y, luego, usaría la lista **Expresión de filtro** para elegir "Reino Unido" entre los valores posibles.  
  
-   Para el segundo filtro, elegiría la dimensión Customer, seleccionaría el atributo Gender y seleccionaría "Female" en la lista de valores de atributo.  
  
 Después de crear la estructura de minería de datos, puede modificar la definición del cubo y los criterios de filtro. Para obtener más información, consulte [filtros para los modelos de minería de datos](~/analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md).  
  
 Tanto la pestaña **Estructura de minería de datos** como la pestaña **Modelo de minería de datos** proporcionan una opción para agregar un filtro a una estructura de minería de datos existente; basta con hacer clic en **Definir un segmento de cubo**. El cuadro de diálogo **Crear segmento de cubo** le ayuda a generar una expresión de filtro MDX válida eligiendo el valor de las listas desplegables.  
  
> [!WARNING]  
>  Observe que la interfaz para diseñar y examinar los cubos se ha cambiado en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Para obtener más información, vea [Examinar los datos y metadatos de un cubo](../../analysis-services/multidimensional-models/browse-data-and-metadata-in-cube.md).  
  
 Puede agregar tantos filtros en el cubo como sea necesario para devolver los datos que necesite para el modelo de minería de datos. También puede definir segmentos en segmentos de cubo individuales. Por ejemplo, si su estructura contiene dos tablas anidadas que están basadas en productos, podría dividir una tabla para marzo de 2004 y la otra tabla para abril de 2004. El modelo resultante se podría utilizar para predecir las compras realizadas en abril según las compras que se realizaron en marzo.  
  
##  <a name="bkmk_Nested"></a> Usar tablas anidadas en un modelo de minería de datos OLAP  
 Si utiliza el Asistente para minería de datos para crear un modelo basado en los datos del cubo, puede agregar tablas anidadas especificando los nombres de las dimensiones relacionadas y eligiendo después los atributos o las medidas que se agregarán al modelo  
  
 Por ejemplo, si la dimensión principal usada para los datos de caso es Customer, puede agregar como dimensión relacionada la dimensión Products, ya que es de prever que un cliente pueda haber pedido varios productos a lo largo del tiempo y el cubo ya vincula cada cliente con los diversos productos a través de las tablas de información de pedidos.  
  
 Para agregar tablas anidadas en la página **Especificar el uso de las columnas del modelo de minería** del asistente, haga clic en **Agregar tablas anidadas**. Se abre un cuadro de diálogo que le guía a través del proceso de elección de una dimensión relacionada y de las medidas. El caso y las dimensiones anidadas se deben relacionar mediante una clave externa, y las medidas deben utilizar uno de los atributos que ya están incluidos en el caso o en las tablas anidadas. Desafortunadamente, en realidad estas restricciones no limitan demasiado el ámbito, por lo que debe tener cuidado de seleccionar solo los atributos útiles para el modelado.  
  
 Para cada atributo o medida que agregue a la tabla anidada, debe especificar si el atributo anidado se va a usar para las predicciones o no, seleccionando **Predicción** o **Entrada** en el cuadro de diálogo **Seleccionar las columnas de la tabla anidada** . Si no selecciona ninguna de estas opciones, los datos se agregarán a la estructura de minería de datos pero no se usarán para el análisis.  
  
 Para cada atributo y medida, también debe especificar si el atributo es discreto, de datos discretos o continuo. El asistente seleccionará de antemano un valor predeterminado según el tipo de datos del atributo, pero puede que tenga que cambiarlo en función de los requisitos del algoritmo. Si elige un tipo de contenido que no es compatible con el algoritmo que ha elegido (por ejemplo, utiliza un tipo numérico continuo con un modelo Bayes Naïve), no obtendrá un mensaje de error hasta que intente procesar el modelo.  
  
 Cuando termine de configurar estas opciones, el asistente agregará la tabla anidada a la tabla de casos. El nombre predeterminado de la tabla anidada es el nombre de la dimensión anidada, pero puede dar otro nombre a esta tabla y a sus columnas. Puede repetir este proceso para agregar varias tablas anidadas a la estructura de minería de datos.  
  
 La capacidad de utilizar así los datos de la tabla anidada es una característica de la minería de datos de SQL Server que resulta muy eficaz y, en un cubo, hay casi infinitas posibilidades para usar los subconjuntos relacionados de datos.  
  
##  <a name="bkmk_DMDimension"></a> Descripción de las dimensiones de minería de datos y obtención de detalles  
 La opción **Permitir obtención de detalles**permite ejecutar consultas en los datos de cubo subyacentes mientras examina el modelo. Los datos no se encuentran en la nueva dimensión de minería de datos, pero la base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] puede utilizar los enlaces de datos para recuperar información del cubo de origen.  
  
 La opción **Crear dimensión de modelo de minería de datos**permite generar una nueva dimensión dentro del cubo existente que contiene los patrones detectados por el algoritmo. La jerarquía dentro de la dimensión viene determinada en gran medida por el tipo de modelo. Por ejemplo, la representación de un modelo de agrupación en clústeres es bastante plana, con el nodo (todos) en la parte superior de la jerarquía y cada clúster en el siguiente nivel. En cambio, la dimensión que se crea para un modelo de árbol de decisión podría tener una jerarquía muy profunda, que represente las ramas del árbol.  
  
 La opción **Crear el cubo con la dimensión del modelo de minería de datos**permite exportar la nueva dimensión de minería de datos en un nuevo cubo. Cualquier objeto necesario para la obtención de detalles en la dimensión de minería de datos se incluye automáticamente.  
  
> [!WARNING]  
>  Solo estos tipos de modelo admiten la creación de dimensiones de minería de datos: los modelos basados en el algoritmo de clústeres de Microsoft, el algoritmo de árboles de decisión de Microsoft o el algoritmo de asociación de Microsoft.  
  
## <a name="see-also"></a>Vea también  
 [Algoritmos de minería de datos & #40; Analysis Services: minería de datos & #41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Columnas de estructura de minería de datos](../../analysis-services/data-mining/mining-structure-columns.md)   
 [Columnas del modelo de minería de datos](../../analysis-services/data-mining/mining-model-columns.md)   
 [Propiedades del modelo de minería de datos](../../analysis-services/data-mining/mining-model-properties.md)   
 [Propiedades de la estructura de minería de datos y columnas de estructura](../../analysis-services/data-mining/properties-for-mining-structure-and-structure-columns.md)  
  
  
