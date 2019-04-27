---
title: CREAR EL MODELO DE MINERÍA DE DATOS (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0e7ca6765ee44201badc54d15fb2a20aa9a863a5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62853470"
---
# <a name="create-mining-model-dmx"></a>CREATE MINING MODEL (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Crea un nuevo modelo de minería de datos y una estructura de minería de datos en la base de datos. Para crear un modelo, puede definir el nuevo modelo en la instrucción o usar el Lenguaje de marcado de modelos de predicción (PMML). Esta segunda opción es solo para usuarios expertos.  
  
 Para asignar el nombre a la estructura de minería de datos, se anexa "_structure" al nombre del modelo, lo que garantiza que el nombre de la estructura sea distinto del nombre del modelo.  
  
 Para crear un modelo de minería de datos para una estructura de minería de datos existente, use el [ALTER MINING STRUCTURE &#40;DMX&#41; ](../dmx/alter-mining-structure-dmx.md) instrucción.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
CREATE [SESSION] MINING MODEL <model>  
(  
    [(<column definition list>)]  
)  
USING <algorithm> [(<parameter list>)] [WITH DRILLTHROUGH]  
CREATE MINING MODEL <model> FROM PMML <xml string>  
```  
  
## <a name="arguments"></a>Argumentos  
 *model*  
 Nombre único del modelo.  
  
 *lista de definiciones de columna*  
 Lista delimitada por comas de definiciones de columna.  
  
 *algorithm*  
 Nombre de un algoritmo de minería de datos definido por el proveedor actual.  
  
> [!NOTE]  
>  Se puede recuperar una lista de los algoritmos admitidos por el proveedor actual mediante [filas DMSCHEMA_MINING_SERVICES](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-services-rowset). Para ver los algoritmos admitidos en la instancia actual de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], consulte [Data Mining Properties](../analysis-services/server-properties/data-mining-properties.md).  
  
 *lista de parámetros*  
 Opcional. Lista delimitada por comas de parámetros definidos por el proveedor para el algoritmo.  
  
 *Cadena XML*  
 (Sólo para uso avanzado.) Un modelo XML codificado (PMML). La cadena debe estar entre comillas simples (').  
  
 El **sesión** cláusula le permite crear un modelo de minería de datos que se quita automáticamente del servidor cuando se cierra la conexión o la sesión agota el tiempo. **SESIÓN** modelos de minería de datos son útiles porque no requieren que el usuario sea un administrador de base de datos, y sólo usan espacio en disco mientras la conexión está abierta.  
  
 El **WITH DRILLTHROUGH** cláusula permite la obtención de detalles en el nuevo modelo de minería de datos. La obtención de detalles solo se puede habilitar al crear el modelo. En algunos tipos de modelo, la obtención de detalles es necesaria para examinar el modelo en el visor personalizado. La obtención de detalles no es necesaria para la predicción o para examinar el modelo utilizando el Visor de árbol de contenido genérico de Microsoft.  
  
 El **CREATE MINING MODEL** instrucción crea un nuevo modelo de minería de datos que se basa en la lista de definiciones de columna, el algoritmo y la lista de parámetros de algoritmo.  
  
### <a name="column-definition-list"></a>Lista de definiciones de columna  
 Para definir la estructura de un modelo que usa la lista de definiciones de columna, debe incluir la siguiente información para cada columna:  
  
-   Nombre (obligatorio)  
  
-   Tipo de datos (obligatorio)  
  
-   Distribución  
  
-   Lista de marcas de modelado  
  
-   Tipo de contenido (obligatorio)  
  
-   Solicitud de predicción, que indica al algoritmo que debe predecir esta columna, indicada por el **PREDICT** o **PREDICT_ONLY** cláusula  
  
-   Relación con una columna de atributos (obligatoria solamente si corresponde), indicado por el **RELATED TO** cláusula  
  
 Use la siguiente sintaxis en la lista de definición de columnas para definir una sola columna:  
  
```  
<column name>    <data type>    [<Distribution>]    [<Modeling Flags>]    <Content Type>    [<prediction>]    [<column relationship>]   
```  
  
 Use la siguiente sintaxis en la lista de definición de columnas para definir una columna de tabla anidada:  
  
```  
<column name>    TABLE    [<prediction>] ( <non-table column definition list> )  
```  
  
 Excepto en el caso de las marcas de modelado, solamente se puede usar una única cláusula de un grupo específico para definir una columna. Puede definir varias marcas de modelado para una columna.  
  
 Para obtener una lista de los tipos de datos, tipos de contenido, distribuciones de columnas y marcas de modelado que puede usar en la definición de una columna, vea los siguientes temas:  
  
-   [Tipos de datos &#40;minería de datos&#41;](../analysis-services/data-mining/data-types-data-mining.md)  
  
-   [Tipos de contenido &#40;minería de datos&#41;](../analysis-services/data-mining/content-types-data-mining.md)  
  
-   [Distribuciones de columnas &#40;minería de datos&#41;](../analysis-services/data-mining/column-distributions-data-mining.md)  
  
-   [Marcas de modelado &#40;Minería de datos&#41;](../analysis-services/data-mining/modeling-flags-data-mining.md)  
  
 Puede agregar una cláusula a la instrucción para describir la relación existente entre dos columnas. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] admite el uso de las siguientes acciones \<relación de columna > cláusula.  
  
 **RELACIONADOS CON**  
 Este formulario indica una jerarquía de valores. El destino de una columna RELATED TO puede ser una columna de clave de una tabla anidada, una columna de valores discretos en la fila de caso u otra columna con una cláusula RELATED TO, que indica una jerarquía de más niveles.  
  
 Use una cláusula de predicción para describir el uso de la columna de predicción. La siguiente tabla describe las dos cláusulas posibles.  
  
|\<predicción > cláusula|Descripción|  
|---------------------------|-----------------|  
|**PREDICT**|Esta columna puede predecirla el modelo y puede proporcionarse en casos de entrada para predecir el valor de otras columnas de predicción.|  
|**PREDICT_ONLY**|Esta columna puede predecirla el modelo, pero sus valores no se pueden utilizar en escenarios de entrada para predecir el valor de otras columnas de predicción.|  
  
### <a name="parameter-definition-list"></a>Lista de definiciones de parámetros  
 Puede usar la lista de parámetros para ajustar el rendimiento y la funcionalidad de un modelo de minería de datos. La sintaxis de la lista de parámetros es:  
  
```  
[<parameter> = <value>, <parameter> = <value>,...]  
```  
  
 Para obtener una lista de los parámetros que están asociados con cada algoritmo, vea [algoritmos de minería de datos &#40;Analysis Services - minería de datos&#41;](../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md).  
  
## <a name="remarks"></a>Comentarios  
 Si desea crear un modelo que tenga un conjunto de datos de pruebas integrado, debe utilizar la instrucción CREATE MINING STRUCTURE seguida de ALTER MINING STRUCTURE. Sin embargo, no todos los tipos de modelo admiten un conjunto de datos de exclusiones. Para obtener más información, consulte [CREATE MINING STRUCTURE &#40;DMX&#41;](../dmx/create-mining-structure-dmx.md).  
  
 Para ver un tutorial sobre cómo crear un modelo de minería de datos mediante la instrucción CREATEMODEL, vea [Tutorial DMX de predicción de Series de temporales](https://msdn.microsoft.com/library/38ea7c03-4754-4e71-896a-f68cc2c98ce2).  
  
## <a name="naive-bayes-example"></a>Ejemplo de Bayes naive  
 En el siguiente ejemplo se usa el algoritmo Bayes naive de [!INCLUDE[msCoName](../includes/msconame-md.md)] para crear un nuevo modelo de minería de datos. La columna Bike Buyer se define como atributo de predicción.  
  
```  
CREATE MINING MODEL [NBSample]  
(  
    CustomerKey LONG KEY,   
    Gender TEXT DISCRETE,  
    [Number Cars Owned] LONG DISCRETE,  
    [Bike Buyer] LONG DISCRETE PREDICT  
)  
USING Microsoft_Naive_Bayes  
```  
  
## <a name="association-model-example"></a>Ejemplo de modelo de asociación  
 En el siguiente ejemplo se usa el algoritmo de asociación de [!INCLUDE[msCoName](../includes/msconame-md.md)] para crear un nuevo modelo de minería de datos. La instrucción aprovecha la capacidad de usar una columna de tabla para anidar tablas dentro de la definición de modelo. El modelo se modifica utilizando el *MINIMUM_PROBABILITY* y *MINIMUM_SUPPORT* parámetros.  
  
```  
CREATE MINING MODEL MyAssociationModel (  
    OrderNumber TEXT KEY,  
    [Products] TABLE PREDICT (  
        [Model] TEXT KEY  
    )  
)  
USING Microsoft_Association_Rules (Minimum_Probability = 0.1, MINIMUM_SUPPORT = 0.01)  
```  
  
## <a name="sequence-clustering-example"></a>Ejemplo de agrupación en clústeres de secuencia  
 En el siguiente ejemplo se usa el algoritmo de clústeres de secuencia de [!INCLUDE[msCoName](../includes/msconame-md.md)] para crear un nuevo modelo de minería de datos. Se usan dos claves para definir el modelo. La columna OrderNumber se utiliza como clave de caso y especifica los pedidos individuales. La columna LineNumber se utiliza como clave de tabla anidada y especifica la secuencia en la que los artículos se agregaron a un pedido.  
  
```  
CREATE MINING MODEL BuyingSequence (  
    [Order Number] TEXT KEY,  
    [Products] TABLE   
     (  
        [Line Number] LONG KEY SEQUENCE,  
        [Model] TEXT DISCRETE PREDICT  
    )  
)  
USING Microsoft_Sequence_Clustering  
```  
  
## <a name="time-series-example"></a>Ejemplo de serie temporal  
 En el siguiente ejemplo se usa el algoritmo de serie temporal de [!INCLUDE[msCoName](../includes/msconame-md.md)] para crear un nuevo modelo de minería de datos mediante el algoritmo ARTxp. ReportingDate es la columna de clave de la serie temporal y ModelRegion es la columna de clave de la serie de datos. En este ejemplo, se supone que la periodicidad de los datos es cada 12 meses. Por lo tanto, el *PERIODICITY_HINT* parámetro está establecido en 12.  
  
> [!NOTE]  
>  Debe especificar el *PERIODICITY_HINT* parámetro mediante el uso de caracteres de llave. Además, dado que el valor es una cadena, debe incluirse entre comillas simples: "{\<valor numérico >}".  
  
```  
CREATE MINING MODEL SalesForecast (  
        ReportingDate DATE KEY TIME,  
        ModelRegion TEXT KEY,  
        Amount LONG CONTINUOUS PREDICT,  
        Quantity LONG CONTINUOUS PREDICT  
)  
USING Microsoft_Time_Series (PERIODICITY_HINT = '{12}', FORECAST_METHOD = 'ARTXP')  
```  
  
## <a name="see-also"></a>Vea también  
 [Extensiones de minería de datos &#40;DMX&#41; instrucciones de definición de datos](../dmx/dmx-statements-data-definition.md)   
 [Extensiones de minería de datos &#40;DMX&#41; instrucciones de manipulación de datos](../dmx/dmx-statements-data-manipulation.md)   
 [Referencia de instrucciones de Extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
