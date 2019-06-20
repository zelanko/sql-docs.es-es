---
title: Crear una nueva estructura de minería de datos OLAP | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d0a12d7fad2deb138d2dac445492ffce55f1493a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62911318"
---
# <a name="create-a-new-olap-mining-structure"></a>Crear una estructura de minería de datos OLAP
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Puede usar el Asistente para minería de datos de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para crear una estructura de minería de datos que utilice datos de un modelo multidimensional. Los modelos de minería de datos basados en los cubos OLAP pueden utilizar las columnas y los valores de las tablas de hechos, las dimensiones y los grupos de medida como atributos para el análisis.  
  
### <a name="to-create-a-new-olap-mining-structure"></a>Para crear una estructura de minería de datos OLAP  
  
1.  En el Explorador de soluciones de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], haga clic con el botón derecho en la carpeta **Estructuras de minería de datos** de un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y luego haga clic en **Nueva estructura de minería de datos** para abrir el Asistente para minería de datos.  
  
2.  En la página de inicio del **Asistente para minería de datos** , haga clic en **Siguiente**.  
  
3.  En la página **Seleccionar el método de definición** , seleccione **A partir de un cubo existente**y, a continuación, haga clic en **Siguiente**.  
  
     Si aparece el mensaje de error No se puede recuperar una lista de algoritmos de minería de datos admitidos, abra el cuadro de diálogo **Propiedades del proyecto** y compruebe que ha especificado el nombre de una instancia de Analysis Services que admite modelos multidimensionales. No puede crear modelos de minería de datos en una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que admita la creación de modelos tabulares.  
  
4.  En la página **Crear la estructura de minería de datos** , decida si desea crear solo una estructura de minería de datos o una estructura de minería de datos más un modelo de minería de datos relacionado. Generalmente, resulta más fácil crear un modelo de minería de datos al mismo tiempo, ya que de esta forma se le solicitará que incluya las columnas necesarias.  
  
     Si va a crear un modelo de minería de datos, seleccione el algoritmo de minería de datos que desee usar y, a continuación, haga clic en **Siguiente**. Para más información sobre cómo seleccionar un algoritmo, vea [Algoritmos de minería de datos &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md).  
  
5.  En la página **Seleccionar la dimensión de cubo de origen** , en **Seleccione una dimensión de cubo de origen**, busque la dimensión que contenga la mayoría de los datos de los casos.  
  
     Por ejemplo, si intenta identificar agrupaciones de clientes, puede seleccionar la dimensión Customer; si intenta analizar las compras entre las distintas transacciones, puede seleccionar la dimensión Internet Sales Order Details. No está obligado a utilizar únicamente los datos de esta dimensión, pero esta debería contener atributos importantes para su uso en el análisis.  
  
     Haga clic en **Siguiente**.  
  
6.  En la página **Seleccionar la clave de caso** , en **Atributos**, seleccione el atributo que se utilizará como clave de la estructura de minería de datos y, a continuación, haga clic en **Siguiente**.  
  
     Normalmente, el atributo utilizado como clave para la estructura de minería de datos es también una clave para la dimensión y aparecerá seleccionado.  
  
7.  En la página **Seleccionar columnas de nivel de caso** , en **Atributos y medidas relacionados**, seleccione los atributos y las medidas que contengan los valores que desea agregar a la estructura de minería de datos como datos de los casos. Haga clic en **Siguiente**.  
  
8.  En la página **Especificar el uso de las columnas del modelo de minería** , en **Estructura del modelo de minería de datos**, establezca primero la columna de predicción y, a continuación, elija las columnas que desea utilizar como entradas.  
  
    -   Active la casilla de la columna situada en el extremo izquierdo para incluir los datos en la estructura de minería de datos. Puede incluir columnas en la estructura y usarlas como referencia, pero no para el análisis.  
  
    -   Seleccione la casilla de la columna **Entrada** para utilizar el atributo como una variable en el análisis.  
  
    -   Seleccione la casilla de la columna **Predicción** solo para los atributos de predicción.  
  
     Tenga en cuenta que las columnas que ha designado como claves no se pueden utilizar para la entrada o la predicción.  
  
     Haga clic en **Siguiente**.  
  
9. También puede agregar y quitar tablas anidadas a la estructura de minería de datos en la página **Especificar el uso de las columnas del modelo de minería** , utilizando **Agregar tablas anidadas** y **Tablas anidadas**.  
  
     En un modelo de minería de datos OLAP, una tabla anidada es otro conjunto de datos del cubo que tiene una relación de uno a varios con la dimensión que representa los atributos del caso. Por lo tanto, cuando se abre el cuadro de diálogo, aparecerán seleccionados los grupos de medida que ya están relacionados con la dimensión seleccionada como la tabla de casos. En este momento, deberá elegir una dimensión diferente que contenga información adicional que resulte útil para el análisis.  
  
     Por ejemplo, si está analizando clientes, usará la dimensión [Customer] como tabla de casos. En la tabla anidada, puede agregar la razón citada por los clientes al realizar una compra, que está incluida en la dimensión [Sales Reason].  
  
     Si agrega datos anidados, deberá especificar dos columnas adicionales:  
  
    -   La clave de la tabla anidada: Esto aparecerá ya seleccionada en la página, **seleccione clave de tabla anidada**.  
  
    -   Los atributos o atributos que se usarán para el análisis: La página, **seleccionar las columnas de tabla anidada**proporciona una lista de medidas y atributos de la selección de tabla anidada.  
  
        -   Para cada atributo que incluya en el modelo, active la casilla de la columna izquierda.  
  
        -   Si desea utilizar el atributo solo para el análisis, active **Entrada**.  
  
        -   Si desea incluir la columna como uno de los atributos de predicción para el modelo, seleccione **Predicción**.  
  
        -   Los elementos incluidos en la estructura pero que no se han especificado como atributos de entrada o de predicción se agregarán a la estructura con la marca **Ignore**; esto significa que los datos se procesan al generar el modelo pero no se utilizan en el análisis, y solo están disponibles para la obtención de detalles. Esto puede ser útil si desea incluir detalles como los nombres de cliente pero no desea utilizar en el análisis.  
  
     Haga clic en **Finalizar** para cerrar la parte del asistente que trabaja con las tablas anidadas. Puede repetir el proceso para agregar varias columnas anidadas.  
  
10. En la página **Especificar el contenido y el tipo de datos de las columnas** , en **Estructura del modelo de minería de datos**, establezca el tipo de contenido y el tipo de datos de cada columna.  
  
    > [!NOTE]  
    >  Los modelos de minería de datos OLAP no admiten el uso de la característica **Detectar** para detectar automáticamente si una columna contiene datos continuos o discretos.  
  
     Haga clic en **Siguiente**.  
  
11. En la página **Segmentar el cubo de origen** , puede filtrar los datos que se utilizan para crear la estructura de minería de datos.  
  
     La segmentación del cubo le permite restringir los datos utilizados para generar el modelo. Por ejemplo, puede generar modelos independientes para cada región realizando la segmentación por la jerarquía Geography y  
  
    -   **Dimensión**: Elija una dimensión relacionada en la lista desplegable.  
  
    -   **Hierarchy**:  Seleccione el nivel de la jerarquía de dimensión a la que desea aplicar el filtro. Por ejemplo, si realiza la segmentación por la dimensión [Geography], seleccionará un nivel de jerarquía como [Region Country Name].  
  
    -   **Operador**: Elija un operador en la lista.  
  
    -   **Expresión de filtro**: Escriba un valor o expresión que se usará como condición de filtro, o utilice la lista desplegable para seleccionar un valor de la lista de los miembros del nivel especificado de la jerarquía.  
  
         Por ejemplo, si seleccionó [Geography] como dimensión y [Region Country Name] como nivel de jerarquía, la lista desplegable contendrá todos los países válidos que puede usar como condición de filtro. Puede hacer selecciones múltiples. Como resultado, los datos de la estructura de minería de datos estarán limitados a los datos del cubo de estas áreas geográficas.  
  
    -   **Parámetros**: Omita esta casilla. Este cuadro de diálogo admite varios escenarios de filtrado de cubos y esta opción no es relevante para generar una estructura de minería de datos.  
  
     Haga clic en **Siguiente**.  
  
12. En la página **Dividir los datos en conjuntos de aprendizaje y conjuntos de pruebas** , especifique el porcentaje de los datos de la estructura de minería de datos que va a reservar para realizar pruebas, o especifique el número máximo de casos de prueba. Haga clic en **Siguiente**.  
  
     Si especifica ambos valores, los límites se combinan para usar el que sea más bajo.  
  
13. En la página **Finalización del asistente** , especifique un nombre para la nueva estructura minería de datos OLAP y el modelo de minería de datos inicial.  
  
14. Haga clic en **Finalizar**.  
  
15. En la página **Finalización del asistente** , también tiene la opción de crear una dimensión de modelo de minería de datos o un cubo mediante la dimensión de modelo de minería de datos. Estas opciones solo se admiten en los modelos generados mediante los algoritmos siguientes:  
  
    -   Algoritmo de clústeres de Microsoft  
  
    -   Algoritmo de árboles de decisión de Microsoft  
  
    -   Algoritmo de reglas de asociación de Microsoft  
  
     **Crear dimensión de modelo de minería de datos**: Active esta casilla y proporcione un nombre de tipo para la dimensión de modelo de minería de datos. Al utilizar esta opción, se crea una nueva dimensión dentro del cubo original utilizado para generar la estructura de minería de datos. Puede utilizar esta dimensión para explorar los datos en profundidad y realizar un análisis más exhaustivo. Dado que la dimensión está situada dentro del cubo, esta se asignará automáticamente a la dimensión de los datos de los casos.  
  
     **Crear el cubo con la dimensión del modelo de minería de datos**: Active esta casilla y proporcione un nombre para el nuevo cubo. Al utilizar esta opción, se creará un nuevo cubo que contiene tanto las dimensiones existentes que se usaron para generar la estructura como la nueva dimensión de minería de datos que contiene los resultados del modelo.  
  
## <a name="see-also"></a>Vea también  
 [Tareas y procedimientos de las estructuras de minería de datos](../../analysis-services/data-mining/mining-structure-tasks-and-how-tos.md)  
  
  
