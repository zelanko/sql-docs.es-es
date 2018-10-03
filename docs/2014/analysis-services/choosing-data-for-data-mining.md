---
title: Elegir datos para minería de datos | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- content type [data mining]
- nested tables
- key [data mining]
- continuous values
- key sequence [data mining]
- table data type
- key time [data mining]
- discrete values
- discretized
ms.assetid: 7c72d80e-913c-4bbe-b258-444294a78838
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 050a7e4b7b89eb52d9fcb8f9d7a6b8a911eaa825
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48134625"
---
# <a name="choosing-data-for-data-mining"></a>Elegir datos para minería de datos
  Cuando comienza la minería de datos, podría preguntar "¿cuántos datos necesito?" o "¿hay algún requisito especial que debo conocer al limpiar o dar formato a mis datos?".  
  
 En concreto, las personas sin experiencia en minería de datos suelen tener problemas con los datos de Excel, como la necesidad de dar formato a los datos de forma coherente dentro de las columnas, limpiar los valores ausentes o discretizar números. En esta sección también se muestran los requisitos de datos para determinados tipos de modelos.  
  
 [Elegir los datos](#bkmk_ChoosingData)  
  
 [Problemas comunes de datos](#bkmk_CommonDataProblems)  
  
 [Otros requisitos de datos](#bkmk_OtherRequirements)  
  
##  <a name="bkmk_ChoosingData"></a> Elegir los datos  
 La selección de los datos empleados para el análisis es quizás la parte importante del proceso de minería de datos, más incluso que la selección de un algoritmo. El motivo es que la minería de datos no suele estar controlada por hipótesis, sino por datos. En lugar de seleccionar y probar variables de antemano, como podría hacer con el modelo estadístico tradicional, la minería de datos puede tomar datos y detectar nuevas correlaciones (o no detectar ningún patrón). La calidad y la cantidad de los datos pueden tener un efecto significativo sobre los resultados.  
  
 En general, tenga en cuenta las reglas siguientes:  
  
-   Obtenga tantos datos limpios como sea posible.  
  
-   Genere perfiles de datos antes de probar cualquier modelo. Debe comprender los datos antes de poder derivar el significado de ellos. Como mínimo:  
  
    1.  Use las herramientas de los complementos para buscar los valores máximos y mínimos, los valores más comunes y los valores promedio.  
  
    2.  Rellene los valores que falten. Los complementos (así como algunos algoritmos) proporcionan herramientas para imputar valores que faltan.  
  
    3.  Corrija los datos incorrectos siempre que sea posible. Los proyectos de minería de datos sirven a menudo como ímpetu para las nuevas iniciativas de calidad de datos.  
  
-   Pruebe a generar un modelo de prueba y buscar problemas en los datos de esa manera. Cuando examine los resultados, puede ver por ejemplo que las previsiones de ventas se basan en datos anómalos debido a un error de conversión de moneda.  
  
-   Intente convertir los datos a formatos diferentes o pruebe a crear cubos de números. Con frecuencia surgen patrones cuando se transforman los datos.  
  
     Por ejemplo, el nivel de servicio del centro de llamadas puede verse afectado según el día de la semana, lo que no vería si solo utilizara valores datetime. Las previsiones son mejores cuando se generan en ciclos de 10 días en lugar de generarse en unidades semanales o diarias.  
  
-   Ponga los números en las ubicaciones adecuadas para reducir el número de valores posibles para el análisis.  
  
-   Cree varias versiones de los datos y genere varios modelos.  
  
 Para obtener sugerencias adicionales sobre cómo seleccionar, modificar y revisar los datos, vea [lista de comprobación de preparación para la minería de datos](checklist-of-preparation-for-data-mining.md).  
  
### <a name="how-much-data-do-i-need"></a>¿Cuántos datos necesito?  
 Una regla general es no tener nunca menos de 50-100 filas de datos para los tipos y escenarios de modelos más simples. Por ejemplo, si va a predecir un solo atributo mediante un modelo Bayes naive y el conjunto de datos es correcto, es posible que pueda generar predicciones bastante precisas con 50-100 filas de datos.  
  
 Para los modelos de asociación, normalmente se necesitan muchos más datos; puede que mil filas no sean suficientes si va a analizar muchos atributos, como asociaciones entre productos. Si el conjunto de datos es demasiado grande o demasiado pequeño, a veces puede conseguir mejores resultados si contrae las filas en categorías. Por ejemplo, en lugar de analizar las asociaciones entre productos individuales, puede categorizar los productos.  
  
 Si tiene un conjunto de datos de un tamaño razonable, céntrese más en la calidad de los datos que en agregar cada vez más datos. Llegado a un punto, se habrán encontrado todos los patrones que son estadísticamente válidos y el hecho de agregar más datos no mejora su validez. Por el contrario, a medida que se agregan más datos en ocasiones se pueden introducir correlaciones accidentales.  
  
### <a name="discrete-vs-continuous-numbers"></a>Números discretos frente a Números continuos  
 Una columna *discreta* contiene un número finito de valores. Por ejemplo, el texto siempre se trata como valor discreto.  
  
 Hay algunos atributos importantes para los valores discretos. Por ejemplo, si se trata los números como discretos, no se implica ningún orden entre ellos y no se puede calcular el promedio o sumar los números. Los códigos de área telefónicos son un buen ejemplo de datos numéricos discretos que nunca usaría para realizar operaciones matemáticas.  
  
 Los valores discretos también reciben el nombre de valores de categorías, ya que se puede agrupar un conjunto de datos basándose en ellos, mientras que no se puede hacer lo mismo con números organizados en una serie infinita.  
  
 Es posible que también decida tratar números como discretos cuando los valores están claramente separados y no existe ninguna posibilidad de que se den valores fraccionarios, o cuando los valores fraccionarios no son útiles.  
  
 Los datos numéricos*continuos* pueden incluir un número de valores fraccionales infinito. Una columna de ingresos es un ejemplo de una columna de atributos continua. Si especifica que una columna es numérica, cada valor de esa columna debe ser un número, excepto los valores NULL. Tenga en cuenta que, en Excel, se pueden considerar las marcas de tiempo y cualquier otra representación de fecha y hora que se pueda convertir a un tipo de datos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 **Convertir números en Variables de categorías**  
  
 Solo porque una columna contiene números no significa que debe tratarlos como números continuos. La*discretización* proporciona muchas ventajas para el análisis. Una es que el problema de espacio se reduce. Other es que a veces los números no son la forma adecuada de expresar un resultado.  
  
 Por ejemplo, el número de hijos por familia se puede tratar como un valor continuo o discreto. Como no es posible tener 2,5 hijos en el hogar, y los hogares con 3 o más hijos pueden comportarse de forma muy diferente a los hogares con 2 hijos, podría obtener mejores resultados si tratara este número como una categoría. Sin embargo, si va a crear un modelo de regresión o necesita un promedio (como 1,357 hijos por hogar), usaría un tipo de datos de número continuo.  
  
 No es posible crear un modelo de minería de datos con datos continuos y después tratar la columna como discreta. Los dos conjuntos de datos deben procesarse de forma diferente y se tratan en el back-end como estructuras de minería de datos independientes. Si no está seguro de la forma adecuada de tratar los datos, debe crear modelos independientes que controlen los datos de forma diferente. En cualquier caso, es conveniente obtener una perspectiva distinta de los datos y quizás resultados diferentes.  
  
 **Convertir números en texto**  
  
 Con mucha frecuencia, valores que deberían ser discretos, como Hombre y Mujer, se representan como datos numéricos mediante las etiquetas 1 y 2. Normalmente, esta codificación se realiza para simplificar la entrada de datos o ahorrar espacio de almacenamiento en una base de datos, pero puede llevar a ambigüedad acerca de la naturaleza o del significando de los valores. Es más, dado que los valores discretos se almacenan como números, al mover datos de una aplicación a otra podría hallar errores de conversión de tipo de datos, y los valores podrían calcularse o, por el contrario, ser tratados como continuos. Para evitar estos problemas, antes de comenzar la minería de datos, debería volver a convertir las etiquetas numéricas en etiquetas de texto discretas.  
  
 **Discretizar números**  
  
 Aunque, en principio, todos los números son infinitos y, por tanto, continuos, cuando se modela la información puede resultar más eficaz *discretizar* o *agrupar* los valores disponibles.  
  
 Puede discretizar datos de muchas formas:  
  
-   Especifique un número finito de cubos y deje que el algoritmo ordene los valores en cubos.  
  
-   Agrúpelos previamente creando un conjunto de agrupaciones que tenga un significado empresarial o con el que sea más fácil trabajar. Con este método, a menudo se pierde la verdadera distribución de los valores, pero los usuarios pueden leer más fácilmente los intervalos.  
  
-   Deje que el algoritmo determine tanto el número óptimo de cubos como la distribución de valores. Este es el valor predeterminado en la mayoría de las herramientas, pero puede invalidar estos valores predeterminados en los asistentes de la barra de herramientas **Minería de datos** .  
  
-   Aproximando valores a una media central o a un valor representativo.  
  
##  <a name="bkmk_CommonDataProblems"></a> Problemas comunes de datos  
  
### <a name="excel-number-formats"></a>Formatos de números de Excel  
 Excel es una herramienta fácil de usar porque es permisiva; es decir, permite colocar cualquier tipo de datos en cualquier sitio. Sin embargo, antes de empezar a buscar patrones y analizar correlaciones, debe imponer alguna estructura o restricciones en los datos.  
  
 De forma predeterminada, cuando se importan datos numéricos en [!INCLUDE[msCoName](../includes/msconame-md.md)] Office Excel, los números se almacenan en un formato decimal con dos posiciones decimales. Si este no es un formato de número adecuado, debería cambiar a otro formato numérico o modificar el número de decimales.  
  
 Una opción consiste en usar el [cambiar etiquetas](relabel-sql-server-data-mining-add-ins.md) herramienta para cambiar la manera en que los números se muestran o agrupan.  
  
 No obstante, si los datos son demasiado complejos como para procesarlos con la herramienta **Cambiar etiquetas** , puede usar las funciones numéricas de Excel para convertir los datos en rangos discretos, guardar el resultado en una columna independiente y, posteriormente, usar la columna de datos discretos para la clasificación.  
  
 Por ejemplo, si está analizando los resultados de una carrera y desea agrupar a los corredores por su tiempo de finalización en minutos, puede redondear al minuto más próximo y guardar el valor redondeado en una nueva columna. También podría extraer únicamente el valor de minuto con la función `MINUTE` y, a continuación, guardar dicho valor en una nueva columna para usarla en el análisis.  
  
### <a name="discretizing-numbers-and-dates-in-excel"></a>Discretizar números y fechas en Excel  
 De manera predeterminada, los datos numéricos en Excel se almacenan como `Double`. Las fechas y horas también se almacenan en formato numérico. Si necesita discretizar números o fechas para la minería de datos, debe agregar nuevas columnas antes de generar el modelo de minería de datos o convertir antes las fechas y los números a otro formato.  
  
### <a name="scientific-number-formats"></a>Formatos de números científicos  
 Las herramientas de minería de datos suelen dar como resultado probabilidades en notación científica para representar números que son muy grandes o muy pequeños. Si no está familiarizado con la notación científica, puede mostrar fácilmente estos números en otro formato cambiando simplemente el formato de la celda.  
  
##### <a name="to-change-scientific-notation-to-a-decimal-numeric-format"></a>Para cambiar la notación científica a un formato numérico decimal  
  
1.  En la tabla de datos de Excel, resalte la columna o la celda que contiene el número en notación científica.  
  
2.  Haga clic con el botón secundario y seleccione **Formato de celdas** en el menú contextual.  
  
3.  En la lista **Categoría** , seleccione **Número**.  
  
4.  Aumente el número de posiciones decimales. Generalmente, las probabilidades representadas en notación científica son muy pequeñas.  
  
     Solo cambia la visualización del número, no el valor subyacente.  
  
### <a name="working-with-dates-and-times"></a>Trabajar con fechas y horas  
 Cuando una columna de una tabla de Excel tiene fechas y se usa como entrada o como predicción, es posible que se obtengan resultados inesperados, en función del formato de la información de fecha y hora. Por ejemplo, cuando se usa **Detectar categorías** o **Clasificar** y se incluye una columna que contiene fechas, las fechas se clasifican como números con muchas posiciones decimales. No se trata de un error; es una representación exacta de los datos subyacentes. El algoritmo de minería de datos trabaja con el formato de almacenamiento subyacente, no con el formato de visualización.  
  
 Si tiene dificultades a la hora de trabajar con fechas y desea analizar fechas mediante agrupaciones comunes como mes o día, puede usar las funciones DATE de Excel para extraer el año, el mes o el día en una columna independiente y, posteriormente, usar esa columna para la clasificación.  
  
##  <a name="bkmk_OtherRequirements"></a> Otros requisitos de datos  
  
### <a name="requirements-by-algorithm-type"></a>Requisitos por tipo de algoritmo  
 Algunos de los algoritmos que se emplean en los complementos requieren determinados tipos de datos o de contenido para crear un modelo.  
  
 **Modelos Naïve Bayes**  
  
-   El algoritmo Bayes naive de [!INCLUDE[msCoName](../includes/msconame-md.md)] no puede usar columnas continuas como entrada. Esto significa que debe discretizar los números, o si hay muy pocos valores, tratarlos como valores discretos.  
  
-   Este tipo de modelo tampoco puede predecir valores continuos. Por tanto, si desea predecir un número continuo como los ingresos (por ejemplo) primero debe discretizar los valores en rangos significativos. Si no está seguro de cuáles son los intervalos adecuados, puede usar el algoritmo de clústeres para identificar los grupos de números en los datos.  
  
-   Cuando se usa un asistente basado en este algoritmo (como [analizar Influenciadores clave &#40;herramientas de análisis de tabla para Excel&#41;](analyze-key-influencers-table-analysis-tools-for-excel.md)), las columnas que son continuas se discretizarán por el asistente le.  
  
-   Si compila un modelo Bayes Naive utilizando la [avanzadas de modelado &#40;complementos minería de datos para Excel&#41; ](advanced-modeling-data-mining-add-ins-for-excel.md) opción, las columnas numéricas se quitarán del modelo. Si desea evitar este problema, utilice el [cambiar etiquetas &#40;complementos de minería de datos de SQL Server&#41; ](relabel-sql-server-data-mining-add-ins.md) herramienta para crear una nueva columna con valores discretizados.  
  
 **Modelos de agrupación en clústeres**  
  
-   Las herramientas de agrupación en clústeres ([Asistente para clúster &#40;complementos minería de datos para Excel&#41; ](cluster-wizard-data-mining-add-ins-for-excel.md) y [detectar categorías &#40;herramientas de análisis de tabla para Excel&#41;](detect-categories-table-analysis-tools-for-excel.md)) también no se puede usar continua números, pero ambas herramientas discretizarán automáticamente las columnas numéricas para usted.  
  
-   Ambas herramientas le ofrecen la opción de elegir el número de categorías de salida en los resultados, pero si desea controlar la manera en la que se agrupan los valores de columnas individuales, debe crear una nueva columna con la agrupación que desee.  
  
 **Los modelos de pronóstico**  
  
-   Todas las herramientas de pronóstico requieren que se prediga un número continuo. No puede predecir un número que se ha guardado como texto.  
  
-   Si los datos contienen columnas numéricas con un tipo de datos incorrecto, puede usar funciones de Excel o de PowerPivot para hacer una copia de la columna que tiene los tipos de datos numéricos correctos. Si lo hace, asegúrese de quitar la copia de la columna que tiene los números de texto para no duplicar los valores.  
  
-   Si desea crear un gráfico de dispersión de un modelo de regresión, las variables de entrada deben ser también números continuos, expresados como un tipo de datos adecuado.  
  
### <a name="using-content-types-to-make-better-models"></a>Usar tipos de contenido para crear mejores modelos  
 Un *tipo de contenido* es una propiedad que se aplica a una columna para especificar cómo debe usar el modelo los datos de la columna. El algoritmo puede usar el tipo de contenido como una instrucción o sugerencia al realizar el análisis.  
  
 Por ejemplo, si una columna contiene números que se repiten en un intervalo concreto para indicar los días de la semana, podría especificar el tipo de contenido de esa columna como `Cyclical`.  
  
 No tiene que preocuparse de los tipos de contenido si utiliza los asistentes y las herramientas proporcionadas en este complemento. Sin embargo, si usa el [Agregar modelo a estructura &#40;complementos minería de datos para Excel&#41; ](add-model-to-structure-data-mining-add-ins-for-excel.md) opción para agregar un nuevo modelo a los datos existentes de modelado, podría obtener un error relacionado con los tipos de contenido.  
  
 El motivo es que algunos tipos de modelo requieren una clase determinada de datos (como una marca de tiempo). Las herramientas procesan estas columnas según requisitos específicos y también agregan una propiedad de tipo de contenido. Por tanto, si reutiliza los datos con un algoritmo completamente diferente, necesitará cambiar el tipo de datos o el tipo de contenido.  
  
 En la lista siguiente se describen los tipos de contenido que se usan en la minería de datos y se identifican los tipos de datos que admiten cada tipo.  
  
 `Discrete`  
 La columna contiene un número finito de valores no continuos. Por ejemplo, una columna de género es una columna de atributos discreta muy habitual, en la que los datos representan un número específico de categorías.  
  
 El tipo de contenido `Discrete` puede utilizarse con todos los tipos de datos.  
  
 `Continuous`  
 La columna contiene valores que representan datos numéricos en una escala que permite valores intermedios. Una columna continua representa medidas escalables; además, es posible que los datos contengan un número infinito de valores fraccionarios. Una columna de temperaturas es un ejemplo de una columna de atributos continua.  
  
 El `Continuous` tipo de contenido puede usarse con los siguientes tipos de datos: `Date`, `Double`, y `Long`.  
  
 `Discretized`  
 La columna contiene valores que representan grupos de valores que se han derivado de una columna continua. Los cubos se tratan como si fueran valores **ordenados** y discretos.  
  
 El tipo de contenido `Discretized` se puede utilizar con los siguientes tipos de datos: `Date`, `Double` y `Long`.  
  
 **Key**  
 La columna identifica una fila de forma única.  
  
 Normalmente, la columna de clave es un identificador numérico o de texto que no debe utilizarse para el análisis, sino para realizar el seguimiento de los registros. Las excepciones son las claves de serie temporal y las claves de secuencia.  
  
 **Claves de tabla anidada** se usan únicamente al obtener datos desde un origen de datos externo definido como un [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] vista del origen de datos. Para obtener más información sobre las tablas anidadas, vea [ http://msdn.microsoft.com/library/ms175659.aspx ](http://msdn.microsoft.com/library/ms175659.aspx):  
  
 Este tipo de contenido se puede utilizar con los siguientes tipos de datos: `Date`, `Double`, `Long` y `Text`.  
  
 **Secuencia de teclas**  
 La columna contiene valores que representan una secuencia de eventos. Los valores están ordenados y no tienen que estar separados por una distancia equivalente.  
  
 Este tipo de contenido es compatible con los siguientes tipos de datos: `Double`, `Long`, `Text`, y `Date`.  
  
 **Clave temporal**  
 La columna contiene valores que se ordenan y representan una escala de tiempo. Solo puede utilizar el tipo de contenido Key Time si el modelo es un modelo de serie temporal o un modelo de agrupación en clústeres de secuencia.  
  
 Este tipo de contenido es compatible con los siguientes tipos de datos: `Double`, `Long` y `Date`.  
  
 **Table**  
 Este tipo de contenido también se utiliza únicamente al obtener datos de un origen de datos externo definido como una vista del origen de datos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 Lo que significa es que cada fila de datos contiene realmente una tabla de datos anidada, con una o más columnas y una o más filas.  
  
 Las tablas anidadas son muy útiles, pero se puede utilizar solo con el [avanzadas de modelado &#40;complementos minería de datos para Excel&#41; ](advanced-modeling-data-mining-add-ins-for-excel.md) opciones de modelado. Por ejemplo, los datos de ejemplo para el [Asistente asociar &#40;cliente de minería de datos para Excel&#41; ](associate-wizard-data-mining-client-for-excel.md) asistente y [análisis de cesta de la compra &#40;herramientas de análisis de tabla para Excel&#41; ](shopping-basket-analysis-table-analysistools-for-excel.md) herramienta contiene los datos que se han aplanado de una tabla anidada.  

  
  
