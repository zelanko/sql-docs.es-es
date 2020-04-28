---
title: CREAR ESTRUCTURA DE MINERÍA DE DATOS (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 87b27f9e1c5927392b4ea221dcb6b7468a42ff9c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68892824"
---
# <a name="create-mining-structure-dmx"></a>CREAR ESTRUCTURA DE MINERÍA DE DATOS (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Crea una nueva estructura de minería de datos en una base de datos y, opcionalmente, define las particiones de aprendizaje y de pruebas. Después de crear la estructura de minería de datos, puede usar la instrucción [ALTER Mining structure &#40;DMX&#41;](../dmx/alter-mining-structure-dmx.md) para agregar modelos a la estructura de minería de datos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
CREATE [SESSION] MINING STRUCTURE <structure>  
(  
    [(<column definition list>)]  
)  
[WITH HOLDOUT (<holdout-specifier> [OR <holdout-specifier>])]  
[REPEATABLE(<holdout seed>)]  
<holdout-specifier>::=  <holdout-maxpercent> PERCENT | <holdout-maxcases> CASES  
```  
  
## <a name="arguments"></a>Argumentos  
 *structure*  
 Nombre único de la estructura.  
  
 *lista de definiciones de columna*  
 Lista delimitada por comas de definiciones de columna.  
  
 *exclusión: maxpercent*  
 Número entero entre 1 y 100 que indica el porcentaje de datos que se reservan para las pruebas.  
  
 *exclusión: maxcases*  
 Número entero que indica el número máximo de casos que deben utilizarse para las pruebas.  
  
 Si el valor especificado para el número máximo de casos es mayor que el número de casos de entrada, se utilizarán todos los casos de entrada para las pruebas y se generará un mensaje de advertencia.  
  
> [!NOTE]  
>  Si se especifica tanto el porcentaje como el número máximo de casos, se utilizará el menor de los dos límites.  
  
 *inicialización de exclusión*  
 Número entero utilizado como valor de inicialización para iniciar la partición de los datos.  
  
 Si se establece en 0, el hash del identificador de la estructura de minería de datos se utiliza como valor de inicialización.  
  
> [!NOTE]  
>  Debería especificar un valor de inicialización si necesita asegurarse de que se puede reproducir una partición.  
  
 Valor predeterminado: REPEATABLE(0)  
  
## <a name="remarks"></a>Observaciones  
 Para definir una estructura de minería de datos hay que especificar una lista de columnas y, opcionalmente, las relaciones jerárquicas entre las columnas; también existe la opción de crear particiones de la estructura de minería de datos en conjuntos de datos de aprendizaje y de pruebas.  
  
 La palabra clave opcional SESSION indica que la estructura es una estructura temporal que solamente puede usarse durante el transcurso de la sesión actual. Cuando finalice la sesión, se eliminará la estructura, así como cualquier modelo basado en la estructura. Para crear estructuras y modelos de minería de datos temporales, primero debe establecer la propiedad de la base de datos AllowSessionMiningModels,. Para más información, consulte [Data Mining Properties](https://docs.microsoft.com/analysis-services/server-properties/data-mining-properties).  
  
## <a name="column-definition-list"></a>Lista de definiciones de columna  
 Para definir una estructura de minería de datos, debe incluir la siguiente información para cada columna de la lista de definiciones de columna:  
  
-   Nombre (obligatorio)  
  
-   Tipo de datos (obligatorio)  
  
-   Distribución  
  
-   Lista de marcas de modelado  
  
-   Tipo de contenido (obligatorio)  
  
-   Relación con una columna de atributos (obligatoria solamente si corresponde), que se indica mediante la cláusula RELATED TO  
  
 Use la siguiente sintaxis en la lista de definiciones de columna para definir una sola columna:  
  
```  
<column name>    <data type>    [<Distribution>]    [<Modeling Flags>]    <Content Type>    [<column relationship>]  
```  
  
 Use la siguiente sintaxis en la lista de definiciones de columna para definir una columna de tabla anidada:  
  
```  
<column name>    TABLE    ( <column definition list> )  
```  
  
 Para obtener una lista de los tipos de datos, tipos de contenido, distribuciones de columnas y marcadores de modelado que pueden usarse en la definición de una columna de estructura, vea los siguientes temas:  
  
-   [Tipos de datos &#40;minería de datos&#41;](https://docs.microsoft.com/analysis-services/data-mining/data-types-data-mining)  
  
-   [Tipos de contenido &#40;minería de datos&#41;](https://docs.microsoft.com/analysis-services/data-mining/content-types-data-mining)  
  
-   [Distribuciones de columnas &#40;minería de datos&#41;](https://docs.microsoft.com/analysis-services/data-mining/column-distributions-data-mining)  
  
-   [Marcas de modelado &#40;Minería de datos&#41;](https://docs.microsoft.com/analysis-services/data-mining/modeling-flags-data-mining)  
  
 Puede definir varios valores de marcas de modelado para una columna. Sin embargo, solo puede haber un tipo de contenido y un tipo de datos para cada columna.  
  
### <a name="column-relationships"></a>Relaciones entre columnas  
 Puede agregar una cláusula a cualquier instrucción de definición de columna para describir la relación existente entre dos columnas. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]admite el uso de la siguiente \<cláusula de relación de columna>.  
  
 **RELACIONADO CON**  
 Indica una jerarquía de valores. El destino de una columna RELATED TO puede ser una columna de clave de una tabla anidada, una columna de valores discretos en la fila de caso u otra columna con una cláusula RELATED TO, que indica una jerarquía de más niveles.  
  
## <a name="holdout-parameters"></a>Parámetros de exclusión  
 Cuando se especifican parámetros de exclusión, se crea una partición de los datos de la estructura. La cantidad de datos especificada para la exclusión se reserva para las pruebas y los datos restantes se utilizan para el aprendizaje. De forma predeterminada, si crea una estructura de minería de datos mediante [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], se crea automáticamente una partición de exclusión que contiene un 30 por ciento de datos de pruebas y un 70 por ciento de datos de aprendizaje. Para más información, consulte [Training and Testing Data Sets](https://docs.microsoft.com/analysis-services/data-mining/training-and-testing-data-sets).  
  
 Si crea una estructura de minería de datos mediante Extensiones de minería de datos (DMX), debe especificar manualmente que se cree una partición de exclusión.  
  
> [!NOTE]  
>  La instrucción **ALTER Mining Structure** no admite la exclusión.  
  
 Puede especificar hasta tres parámetros de exclusión. Si especifica tanto un número máximo de casos de exclusión como un porcentaje de exclusión, se reserva un porcentaje de casos hasta que se alcance el límite máximo de casos. Especifique el porcentaje de exclusión como un entero seguido de la palabra clave **Percent** y especifique el número máximo de casos como un entero seguido de la palabra clave **Cases** . Las condiciones pueden combinarse en cualquier orden, como se muestra en los ejemplos siguientes:  
  
```  
WITH HOLDOUT (20 PERCENT)   
WITH HOLDOUT (2000 CASES)   
WITH HOLDOUT (20 PERCENT OR 2000 CASES)   
WITH HOLDOUT (2000 CASES OR 20 PERCENT)  
```  
  
 El valor de inicialización de la exclusión controla el punto inicial del proceso que asigna de forma aleatoria los casos a los conjuntos de datos de aprendizaje o de pruebas. Si establece un valor de inicialización de la exclusión, puede asegurarse de que se puede repetir la partición. Si no especifica un valor de inicialización de la exclusión, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] utiliza el nombre de la estructura de minería de datos para crear un valor de inicialización. Si cambia el nombre de la estructura, cambiará el valor de inicialización. El parámetro del valor de inicialización de la exclusión se puede utilizar con cualquiera de los otros dos parámetros de exclusión o con ambos.  
  
> [!NOTE]  
>  Dado que la información de la partición se almacena en la memoria caché con los datos de entrenamiento, para usar la exclusión, debe asegurarse de que la propiedad **CacheMode** de la estructura de minería de datos está establecida en **KeepTrainingData**. Ésta es la configuración predeterminada en [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] para las estructuras de minería de datos nuevas. Cambiar la propiedad **CacheMode** a **ClearTrainingCases** en una estructura de minería de datos existente que contenga una partición de exclusión no afectará a los modelos de minería de datos que se hayan procesado. Sin embargo, <xref:Microsoft.AnalysisServices.MiningStructureCacheMode> si no se establece en **KeepTrainingData**, los parámetros de exclusión no tendrán ningún efecto. Esto significa que todos los datos de origen se utilizarán para el aprendizaje y no habrá ningún conjunto de pruebas disponible. La definición de la partición se almacena en memoria caché con la estructura; si borra la memoria caché de casos de aprendizaje, también borrará la memoria caché de datos de pruebas y la definición del conjunto de exclusión.  
  
## <a name="examples"></a>Ejemplos  
 En los ejemplos siguientes se muestra cómo crear una estructura de minería de datos con exclusión mediante DMX.  
  
### <a name="example-1-adding-a-structure-with-no-training-set"></a>Ejemplo 1: agregar una estructura sin un conjunto de aprendizaje  
 En el ejemplo siguiente se crea una estructura de minería de datos denominada `New Mailing` sin crear ningún modelo de minería de datos asociado y sin utilizar la exclusión. Para obtener información sobre cómo agregar un modelo de minería de datos a la estructura, consulte [ALTER Mining structure &#40;DMX&#41;](../dmx/alter-mining-structure-dmx.md).  
  
```  
CREATE MINING STRUCTURE [New Mailing]  
(  
    CustomerKey LONG KEY,   
    Gender TEXT DISCRETE,  
    [Number Cars Owned] LONG DISCRETE,  
    [Bike Buyer] LONG DISCRETE   
)  
```  
  
### <a name="example-2-specifying-holdout-percentage-and-seed"></a>Ejemplo 2: especificar el porcentaje y el valor de inicialización de la exclusión  
 Puede agregarse la siguiente cláusula a continuación de la lista de definiciones de columna para definir un conjunto de datos que puede usarse para probar todos los modelos de minería de datos asociados a la estructura de minería de datos. La instrucción creará un conjunto de pruebas con el 25 por ciento del total de casos de entrada sin un límite en el número máximo de casos. Se utiliza 5000 como valor de inicialización para crear la partición. Cuando especifique un valor de inicialización, se elegirán los mismo casos para el conjunto de pruebas cada vez que procese la estructura de minería de datos, siempre y cuando los datos subyacentes no cambien.  
  
```  
CREATE MINING STRUCTURE [New Mailing]  
(  
    CustomerKey LONG KEY,   
    Gender TEXT DISCRETE,  
    [Number Cars Owned] LONG DISCRETE,  
    [Bike Buyer] LONG DISCRETE   
)   
WITH HOLDOUT(25 PERCENT) REPEATABLE(5000)  
```  
  
### <a name="example-3-specifying-holdout-percentage-and-max-cases"></a>Ejemplo 3: especificar el porcentaje y el número máximo de casos de exclusión  
 La cláusula siguiente creará un conjunto de pruebas que contiene el 25 por ciento del total de casos de entrada o 2000 casos, lo que sea menor. Dado que se especifica 0 como valor de inicialización, se utiliza el nombre de la estructura de minería de datos para crear el valor de inicialización que se usa para empezar el muestreo de los casos de entrada.  
  
```  
CREATE MINING STRUCTURE [New Mailing]  
(  
    CustomerKey LONG KEY,   
    Gender TEXT DISCRETE,  
    [Number Cars Owned] LONG DISCRETE,  
    [Bike Buyer] LONG DISCRETE   
)   
WITH HOLDOUT(25 PERCENT OR 2000 CASES) REPEATABLE(0)  
```  
  
## <a name="see-also"></a>Consulte también  
 [Extensiones de minería de datos &#40;DMX&#41; instrucciones de definición de datos](../dmx/dmx-statements-data-definition.md)   
 [Extensiones de minería de datos &#40;DMX&#41; instrucciones de manipulación de datos](../dmx/dmx-statements-data-manipulation.md)   
 [Referencia de instrucciones de Extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
