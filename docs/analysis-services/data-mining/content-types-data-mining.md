---
title: (Minería de datos) de tipos de contenido | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0dcc5840467f039e78c0c4d4b75862bbf78a6a42
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62725189"
---
# <a name="content-types-data-mining"></a>Tipos de contenido (minería de datos)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  En [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], puede definir tanto el tipo de datos físico de una columna en una estructura de minería como un tipo de datos lógico de la columna cuando se utilice en un modelo.  
  
 El *tipo de datos* determina el modo en que los algoritmos procesan los datos de esas columnas cuando se crean modelos de minería. La definición del tipo de datos de una columna proporciona al algoritmo información sobre el tipo de datos de las columnas y el modo de procesar los datos. Cada tipo de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] admite uno o varios tipos de contenido para la minería de datos.  
  
 El *tipo de contenido* describe el comportamiento del contenido incluido en la columna. Por ejemplo, si el contenido de una columna se repite en un intervalo concreto, como los días de la semana, puede especificar el tipo de contenido de esa columna como cíclico.  
  
 Algunos algoritmos requieren tipos de datos y de contenido específicos para que funcionen correctamente. Por ejemplo, el algoritmo Bayes naive de Microsoft no puede utilizar columnas continuas como entrada ni predecir valores continuos. Algunos tipos de contenido, como Key Sequence, solo son utilizados por un algoritmo concreto. Para consultar una lista de los algoritmos y de los tipos de contenido que admite cada uno, vea [Algoritmos de minería de datos &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md).  
  
 En la lista siguiente se describen los tipos de contenido que se usan en la minería de datos y se identifican los tipos de datos que admiten cada tipo.  
  
## <a name="discrete"></a>Discrete  
 El tipo de contenido*discreto* indica que la columna contiene un número finito de valores no continuos. Por ejemplo, una columna de género es una columna de atributos discreta muy habitual, en la que los datos representan un número específico de categorías.  
  
 Los valores de una columna de atributos discreta no pueden implicar la ordenación, aun cuando los valores sean numéricos. Además, aunque los valores utilizados para la columna discreta sean numéricos, no se pueden calcular valores fraccionarios. Los códigos telefónicos de cada zona son un buen ejemplo de datos numéricos discretos.  
  
 El tipo de contenido **Discrete** es compatible con todos los tipos de datos de minería de datos.  
  
## <a name="continuous"></a>Continuous  
 *Continuo* indica que la columna contiene valores que representan datos numéricos en una escala que permite valores intermedios. A diferencia de una columna discreta, que representa datos numerables y finitos, una columna continua representa medidas escalables; además, es posible que los datos contengan un número infinito de valores fraccionarios. Una columna de temperaturas es un ejemplo de una columna de atributos continua.  
  
 Cuando una columna contiene datos numéricos y se sabe cómo deben distribuirse los datos, se podrían obtener análisis más exactos especificando la distribución prevista de los valores. La distribución de columnas se especifica en el nivel de la estructura de minería. Por lo tanto, la configuración se aplica a todos los modelos basados en la estructura. Para más información, vea [Distribuciones de columnas &#40;Minería de datos&#41;](../../analysis-services/data-mining/column-distributions-data-mining.md).  
  
 El **Continuous** tipo de contenido es compatible con los siguientes tipos de datos: **Fecha**, **doble**, y **largo**.  
  
## <a name="discretized"></a>Discretized  
 La*discretización* es el proceso mediante el cual los valores de un conjunto de datos continuo se incluyen en depósitos para que haya un número limitado de valores posibles. Solo se pueden discretizar los datos numéricos.  
  
 Por tanto, el tipo de contenido *discretized* indica que la columna contiene valores que representan grupos o depósitos de valores que se derivan de una columna continua. Los depósitos se tratan como si fueran valores ordenados y discretos.  
  
 Se pueden discretizar los datos manualmente, para asegurarse de que se obtienen los depósitos deseados, o se pueden utilizar los métodos de discretización proporcionados en SQL Server Analysis Services. Algunos algoritmos realizan la discretización automáticamente. Para más información, vea [Cambiar la discretización de una columna en un modelo de minería de datos](../../analysis-services/data-mining/change-the-discretization-of-a-column-in-a-mining-model.md).  
  
 El **Discretized** tipo de contenido es compatible con los siguientes tipos de datos: **Fecha**, **doble**, **largo**, y **texto**.  
  
## <a name="key"></a>Key  
 El tipo de contenido *clave* indica que la columna identifica una fila de forma inequívoca. Normalmente, en una tabla de casos, la columna de clave es un identificador numérico o de texto. Establezca el tipo de contenido en **key** para indicar que la columna no debe utilizarse para el análisis, sino para realizar el seguimiento de los registros.  
  
 Las tablas anidadas también tienen claves, pero el uso de la clave de tabla anidada es ligeramente diferente. En una tabla anidada debe establecer el tipo de contenido en **key** si la columna es el atributo que desea analizar. Los valores de la clave de tabla anidada deben ser únicos para cada caso, pero puede haber duplicados en todo el conjunto de casos.  
  
 Por ejemplo, si está analizando los productos que compran los clientes, debe establecer el tipo de contenido en Key para la columna **CustomerID** de la tabla de casos, y también debe establecer el tipo de contenido en Key para la columna **PurchasedProducts** de la tabla anidada.  
  
> [!NOTE]  
>  Las tablas anidadas solo están disponibles si utiliza los datos de un origen de datos externo definido como una vista del origen de datos (Analysis Services).  
  
 Este tipo de contenido es compatible con los siguientes tipos de datos: **Fecha**, **doble**, **largo**, y **texto**.  
  
## <a name="key-sequence"></a>Key Sequence  
 El tipo de contenido *secuencia de claves* solamente se puede utiliza en modelos de agrupación en clústeres de secuencia. Cuando se establece el tipo de contenido en **key sequence**, se indica que la columna contiene valores que representan una secuencia de eventos. Los valores están ordenados y no tienen que estar separados por una distancia equivalente.  
  
 Este tipo de contenido es compatible con los siguientes tipos de datos: **Double**, **largo**, **texto**, y **fecha**.  
  
## <a name="key-time"></a>Key Time  
 El tipo de contenido *clave temporal* solamente se puede utilizar en modelos de serie temporal. Cuando se establece el tipo de contenido en **key time**, se indica que los valores están ordenados y que representan una escala de tiempo.  
  
 Este tipo de contenido es compatible con los siguientes tipos de datos: **Double**, **largo**, y **fecha**.  
  
## <a name="table"></a>Table  
 El tipo de contenido *tabla* indica que la columna contiene otra tabla de datos, con una o más columnas y una o más filas. Para cualquier fila concreta de la tabla de casos, esta columna puede contener varios valores, todos ellos relacionados con el registro del caso primario. Por ejemplo, si la tabla de casos principal contiene una lista de clientes, podría tener varias columnas con tablas anidadas, como una columna **ProductosComprados** , donde la tabla anidada muestre una lista de los productos que este cliente ha comprado en el pasado, y una columna **Aficiones** que muestre las aficiones del cliente.  
  
 El tipo de datos de esta columna siempre es **Table**.  
  
## <a name="cyclical"></a>Cíclico  
 El tipo de contenido *cíclico* indica que la columna contiene valores que representan un conjunto ordenado cíclico. Por ejemplo, los días numerados de la semana es un conjunto ordenado cíclico, ya que el día número uno sigue al día número siete.  
  
 Las columnas cíclicas se consideran ordenadas y discretas en términos de tipo de contenido.  
  
 Este tipo de contenido es compatible con todos los tipos de datos de minería de datos en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Sin embargo, la mayoría de los algoritmos tratan los valores cíclicos como valores discretos y no realizan ningún procesamiento especial.  
  
## <a name="ordered"></a>Ordenado  
 El tipo de contenido *ordenado* indica también que la columna contiene valores que definen una secuencia u orden. Sin embargo, en este tipo de contenido los valores utilizados para la ordenación no implican ninguna relación de distancia o magnitud entre los valores del conjunto. Por ejemplo, si una columna de atributos ordenados contiene información acerca de una lista de niveles de especialización que vayan del uno al cinco, no existe información implícita entre los niveles de especialización; un nivel cinco de especialización no es necesariamente cinco veces mejor que un nivel uno de especialización.  
  
 Las columnas de atributos ordenados se consideran discretas en términos de tipo de contenido.  
  
 Este tipo de contenido es compatible con todos los tipos de datos de minería de datos en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Sin embargo, la mayoría de los algoritmos tratan los valores ordenados como valores discretos y no realizan ningún procesamiento especial.  
  
## <a name="classified"></a>Classified  
 Además de los tipos de contenido anteriores cuyo uso es común en todos los modelos, para algunos tipos de datos puede utilizar columnas clasificadas para definir tipos de contenido. Para más información sobre las columnas clasificadas, vea [Columnas clasificadas &#40;Minería de datos&#41;](../../analysis-services/data-mining/classified-columns-data-mining.md).  
  
## <a name="see-also"></a>Vea también  
 [Tipos de contenido &#40;DMX&#41;](../../dmx/content-types-dmx.md)   
 [Tipos de datos &#40;minería de datos&#41;](../../analysis-services/data-mining/data-types-data-mining.md)   
 [Tipos de datos &#40;DMX&#41;](../../dmx/data-types-dmx.md)   
 [Cambiar las propiedades de una estructura de minería de datos](../../analysis-services/data-mining/change-the-properties-of-a-mining-structure.md)   
 [Columnas de la estructura de minería de datos](../../analysis-services/data-mining/mining-structure-columns.md)  
  
  
