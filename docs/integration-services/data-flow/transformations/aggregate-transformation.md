---
title: "Transformación Agregado| Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.aggregatetrans.f1
- sql13.dts.designer.aggregationtransformation.aggregations.f1
- sql13.dts.designer.aggregationtransformation.advanced.f1
helpviewer_keywords:
- IsBig property
- aggregate functions [Integration Services]
- Aggregate transformation [Integration Services]
- large data, SSIS transformations
ms.assetid: 2871cf2a-fbd3-41ba-807d-26ffff960e81
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 7262db9da133a2aa6f82f501e8dab3228de16efb
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="aggregate-transformation"></a>Transformación Agregado
  La transformación Agregado aplica funciones de agregado, como Average, a los valores de columnas y copia los resultados en la salida de transformación. Además de las funciones de agregado, la transformación proporciona la cláusula GROUP BY, que se puede usar para especificar los grupos en los que se debe realizar el agregado.  
  
## <a name="operations"></a>Operaciones  
 La transformación Agregado admite las siguientes operaciones.  
  
|Operación|Description|  
|---------------|-----------------|  
|GROUP BY|Divide los conjuntos de datos en grupos. Se pueden usar columnas de cualquier tipo de datos para la agrupación. Para más información, vea [GROUP BY &#40;Transact-SQL&#41;](../../../t-sql/queries/select-group-by-transact-sql.md).|  
|SUM|Suma los valores de una columna. Solo podrán sumarse las columnas con tipos de datos numéricos. Para más información, vea [SUM &#40;Transact-SQL&#41;](../../../t-sql/functions/sum-transact-sql.md).|  
|Promedio|Devuelve la media de los valores de columna de una columna. Solo podrá calcularse la media de las columnas con tipos de datos numéricos. Para más información, vea [AVG &#40;Transact-SQL&#41;](../../../t-sql/functions/avg-transact-sql.md).|  
|Count|Devuelve el número de elementos de un grupo. Para más información, vea [COUNT &#40;Transact-SQL&#41;](../../../t-sql/functions/count-transact-sql.md).|  
|COUNT DISTINCT|Devuelve el número de valores únicos distintos de NULL de un grupo.|  
|Mínima|Devuelve el valor mínimo en un grupo. Para más información, vea [MIN &#40;Transact-SQL&#41;](../../../t-sql/functions/min-transact-sql.md). En comparación con la función MIN de Transact-SQL, esta operación se puede usar únicamente con tipos de datos numéricos, de fecha y hora.|  
|Máximo|Devuelve el valor máximo en un grupo. Para más información, vea [MAX &#40;Transact-SQL&#41;](../../../t-sql/functions/max-transact-sql.md). En comparación con la función MAX de Transact-SQL, esta operación se puede usar únicamente con tipos de datos numéricos, de fecha y hora.|  
  
 La transformación Agregado controla los valores NULL de la misma forma que el motor de base de datos relacional de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Este comportamiento se define en el estándar SQL-92. Se aplican las reglas siguientes:  
  
-   En una cláusula GROUP BY, los valores NULL se tratan como cualquier otro valor de columna. Si la columna de agrupamiento contiene varios valores NULL, éstos se colocan en un grupo individual.  
  
-   En las funciones COUNT (nombre de columna) y COUNT (nombre de columna DISTINCT), los valores NULL se omiten y el resultado excluye las filas que contienen valores NULL en la columna con nombre.  
  
-   En la función COUNT (*), se cuentan todas las filas, incluso las filas con valores NULL.  
  
## <a name="big-numbers-in-aggregates"></a>Números grandes en agregados  
 Una columna puede contener valores numéricos que requieren una consideración especial debido a su elevado valor o requisitos de precisión. La transformación Agregado incluye la propiedad IsBig, que se puede establecer en columnas de salida para invocar un control especial de números grandes o de alta precisión. Si el valor de la columna puede superar los 4 mil millones o se requiere una precisión más allá del tipo de datos float, IsBig se debe establecer en 1.  
  
 Si se establece la propiedad IsBig en 1, esto afecta la salida de la transformación Agregado de las siguientes maneras:  
  
-   Se usa el tipo de datos DT_R8 en lugar del tipo de datos DT_R4.  
  
-   Los resultados del recuento se almacenan como el tipo de datos DT_UI8.  
  
-   Los resultados del recuento diferente se almacenan como el tipo de datos DT_UI4.  
  
> [!NOTE]  
>  No se puede establecer IsBig en 1 en columnas que se usan en las operaciones GROUP BY, MAX y MIN.  
  
## <a name="performance-considerations"></a>Consideraciones de rendimiento  
 La transformación Agregado incluye un conjunto de propiedades que se pueden establecer para mejorar el rendimiento de la transformación.  
  
-   Cuando realice una operación **Group by** , defina las propiedades Keys o KeysScale del componente y las salidas de componente. Si usa Keys, puede especificar el número exacto de claves que se espera que la transformación administre. (En este contexto, Keys hace referencia al número de grupos que se espera como resultado de una operación **Group by**). Con KeysScale, puede especificar un número aproximado de claves. Si especifica un valor correcto para Keys o KeyScale, mejorará el rendimiento porque la transformación podrá asignar la memoria adecuada a los datos que almacena en memoria caché.  
  
-   Cuando realice una operación **Distinct count** , defina las propiedades CountDistinctKeys o CountDistinctScale del componente. Con CountDistinctKeys, puede especificar el número exacto de claves que se espera que la transformación controle en una operación count distinct. (En este contexto, CountDistinctKeys hace referencia al número de valores distintos que se esperan como resultado de una operación **Distinct count**). Mediante CountDistinctScale, puede especificar una cantidad aproximada de claves para una operación count distinct. Si especifica un valor correcto para CountDistinctKeys o CountDistinctScale, mejorará el rendimiento porque la transformación podrá asignar la memoria adecuada a los datos que almacena en memoria caché.  
  
## <a name="aggregate-transformation-configuration"></a>Configuración de la transformación Agregado  
 La transformación Agregado se configura en los niveles de transformación, salida y columna.  
  
-   En el nivel de la transformación, se configura la transformación Agregado a efectos de rendimiento especificando los valores siguientes:  
  
    -   El número de grupos que esperan obtenerse como resultado de la operación **GROUP BY** .  
  
    -   El número de valores distintos que esperan obtenerse como resultado de la operación **COUNT DISTINCT** .  
  
    -   El porcentaje en el que la memoria se puede ampliar durante la agregación.  
  
     La transformación Agregado también se puede configurar para generar una advertencia en lugar de un error cuando el valor de un divisor es cero.  
  
-   En el nivel de salida, la transformación Agregado se configura a efectos de rendimiento especificando el número de grupos que se esperan como resultado de una operación **GROUP BY** . La transformación Agregado admite varias salidas y cada una se puede configurar de forma diferente.  
  
-   En el nivel de columna, se especifican los valores siguientes:  
  
    -   La agregación que la columna realiza.  
  
    -   Las opciones de comparación de la agregación.  
  
 La transformación Agregado también se puede configurar a efectos de rendimiento especificando estos valores:  
  
-   El número de grupos que se espera obtener como resultado de la operación **GROUP BY** de la columna.  
  
-   El número de valores distintos que se espera obtener como resultado de la operación **COUNT DISTINCT** de la columna.  
  
 También puede identificar las columnas como IsBig si una columna contiene valores numéricos grandes o valores numéricos con alta precisión.  
  
 La transformación Agregado es asincrónica, lo que significa que no utiliza ni publica datos fila por fila. En lugar de ello, utiliza todo el conjunto de filas, realiza sus agrupaciones y agregaciones, y, seguidamente, publica los resultados.  
  
 Esta transformación no pasa por ninguna columna, sino que crea nuevas columnas en el flujo de datos para los datos que publica. Solo las columnas de entrada a las que se aplican las funciones de agregado o las columnas de entrada que usa la transformación para agrupar se copian en la salida de transformación. Por ejemplo, una entrada de la transformación Agregado puede tener tres columnas: **CountryRegion**, **City**y **Population**. La transformación agrupa de acuerdo con la columna **CountryRegion** y aplica la función Sum a la columna **Population** . Por tanto, la salida no incluye la columna **City** .  
  
 Puede también agregar varias salidas a la transformación Agregado y dirigir cada agregación a una salida diferente. Por ejemplo, si la transformación Agregado aplica las funciones Sum y Average, cada agregación se puede dirigir a una salida diferente.  
  
 Puede aplicar varias agregaciones a una sola columna de entrada. Por ejemplo, si quiere los valores de suma y promedio de una columna de entrada denominada **Sales**, puede configurar la transformación para aplicar las funciones Sum y Average a la columna **Sales** .  
  
 La transformación Agregado tiene una entrada y una o varias salidas. No admite una salida de error.  
  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o mediante programación.  
  
 El cuadro de diálogo **Editor avanzado** indica las propiedades que se pueden establecer mediante programación. Para obtener más información acerca de las propiedades que puede establecer a través del cuadro de diálogo **Editor avanzado** o mediante programación, haga clic en uno de los temas siguientes:  
  
-   [Propiedades comunes](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Propiedades personalizadas de transformación](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 Para obtener más información sobre cómo establecer valores de propiedades, haga clic en uno de los temas siguientes:  
  
-   [Agregar valores en un conjunto de datos mediante la transformación Agregado](../../../integration-services/data-flow/transformations/aggregate-values-in-a-dataset-by-using-the-aggregate-transformation.md)  
  
-   [Establecer las propiedades de un componente de flujo de datos](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
-   [Ordenación de datos para las transformaciones Mezclar y Combinación de mezcla](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 [Incorporación de valores en un conjunto de datos con la transformación Agregado](../../../integration-services/data-flow/transformations/aggregate-values-in-a-dataset-by-using-the-aggregate-transformation.md)  
  
## <a name="aggregate-transformation-editor-aggregations-tab"></a>Editor de transformación Agregado (pestaña Agregaciones)
  Use la pestaña **Agregaciones** del cuadro de diálogo **Editor de transformación Agregado** para especificar las columnas que desea agregar y las propiedades de agregación. Puede aplicar diversas agregaciones. Esta transformación no genera una salida de errores.  
  
> [!NOTE]  
>  Las opciones para el recuento de claves, la escala de claves, la clave Count Distinct y la escala de claves distintas estarán disponibles en el componente si se especifican en la pestaña **Avanzadas** , en la salida si se especifican en la pantalla avanzada de la pestaña **Agregaciones** y en la columna si se especifican en la lista de columnas en la parte inferior de la pestaña **Agregaciones** .  
>   
>  En la transformación Agregado, **Claves** y **Escala de claves** hacen referencia al número de grupos que se esperan como resultado de una operación **Agrupar por** . **Claves Count Distinct** y **Escala Count Distinct** hacen referencia al número de valores distintos que se esperan como resultado de una operación **Recuento distinto** .  
  
### <a name="options"></a>.  
 **Avanzadas/Básicas**  
 Muestra u oculta opciones para configurar diversas agregaciones para varias salidas. De forma predeterminada, las opciones Avanzadas aparecen ocultas.  
  
 **Nombre de agregación**  
 En la pantalla Avanzadas, escriba un nombre descriptivo para la agregación.  
  
 **Agrupar por columnas**  
 En la pantalla Avanzadas, seleccione las columnas que quiere agrupar en la lista **Columnas de entrada disponibles** como se explica a continuación.  
  
 **Escala de claves**  
 En la pantalla Avanzadas, especifique opcionalmente el número aproximado de claves que podrá escribir la agregación. De forma predeterminada, el valor de esta opción es **No especificado**. Si se seleccionan las propiedades **Escala de claves** y **Claves** , tendrá prioridad el valor de **Claves** .  
  
|Valor|Description|  
|-----------|-----------------|  
|No especificado|No se utiliza la propiedad Escala de claves.|  
|Baja|La agregación podrá escribir aproximadamente 500 000 claves.|  
|Media|La agregación podrá escribir aproximadamente 5.000.000 claves.|  
|Alta|La agregación podrá escribir más de 25.000.000 claves.|  
  
 **Claves**  
 En la pantalla Avanzadas, especifique opcionalmente el número exacto de claves que podrá escribir la agregación. Si se especifican **Escala de claves** y **Claves** , tendrá prioridad **Claves** .  
  
 **Columnas de entrada disponibles**  
 Seleccione una columna en la lista de columnas de entrada disponibles con las casillas de la tabla.  
  
 **Columna de entrada**  
 Seleccione las columnas de entrada disponibles de la lista.  
  
 **Alias de salida**  
 Escriba un alias para cada columna. El nombre predeterminado es el de la columna de entrada, pero puede elegir cualquier nombre descriptivo único.  
  
 **Operación**  
 Elija una operación de la lista de operaciones disponibles con la siguiente tabla como guía.  
  
|Operación|Description|  
|---------------|-----------------|  
|**GROUP BY**|Divide los conjuntos de datos en grupos. Podrán agruparse columnas con cualquier tipo de datos. Para obtener más información, vea GROUP BY.|  
|**Sum**|Suma los valores de una columna. Solo podrán sumarse las columnas con tipos de datos numéricos. Para obtener más información, vea SUM.|  
|**Promedio**|Devuelve la media de los valores de columna de una columna. Solo podrá calcularse la media de las columnas con tipos de datos numéricos. Para obtener más información, vea AVG.|  
|**Count**|Devuelve el número de elementos de un grupo. Para obtener más información, vea COUNT.|  
|**CountDistinct**|Devuelve el número de valores únicos distintos de NULL de un grupo. Para obtener más información, vea COUNT y Distinct.|  
|**Mínima**|Devuelve el valor mínimo en un grupo. Está restringido a los tipos de datos numéricos.|  
|**Máximo**|Devuelve el valor máximo en un grupo. Está restringido a los tipos de datos numéricos.|  
  
 **Marcas de comparación**  
 Si selecciona **Agrupar por**, use las casillas para controlar cómo realiza la transformación la comparación. Para obtener más información acerca de las opciones de comparación de cadenas, vea [Comparing String Data](../../../integration-services/data-flow/comparing-string-data.md).  
  
 **Count Distinct Scale**  
 Opcionalmente, puede especificar el número aproximado de valores DISTINCT que podrá escribir la agregación. De forma predeterminada, el valor de esta opción es **No especificado**. Si se especifican **CountDistinctScale** y **CountDistinctKeys** , tendrá prioridad **CountDistinctKeys** .  
  
|Valor|Description|  
|-----------|-----------------|  
|No especificado|No se utiliza la propiedad **CountDistinctScale** .|  
|Baja|La agregación podrá escribir aproximadamente 500.000 valores DISTINCT.|  
|Media|La agregación podrá escribir aproximadamente 5 000 000 valores DISTINCT.|  
|Alta|La agregación podrá escribir más de 25.000.000 valores DISTINCT.|  
  
 **Count Distinct Keys**  
 Opcionalmente, puede especificar el número exacto de valores DISTINCT que podrá escribir la agregación. Si se especifican **CountDistinctScale** y **CountDistinctKeys** , tendrá prioridad **CountDistinctKeys** .  
  
## <a name="aggregate-transformation-editor-advanced-tab"></a>Editor de transformación Agregado (pestaña Avanzadas)
  Utilice la pestaña **Avanzadas** del cuadro de diálogo **Editor de transformación Agregado** para establecer las propiedades del componente, especificar agregaciones y establecer las propiedades de las columnas de entrada y salida.  
  
> [!NOTE]  
>  Las opciones para el recuento de claves, la escala de claves, la clave Count Distinct y la escala de claves distintas estarán disponibles en el componente si se especifican en la pestaña **Avanzadas** , en la salida si se especifican en la pantalla avanzada de la pestaña **Agregaciones** y en la columna si se especifican en la lista de columnas en la parte inferior de la pestaña **Agregaciones** .  
>   
>  En la transformación Agregado, **Claves** y **Escala de claves** hacen referencia al número de grupos que se esperan como resultado de una operación **Agrupar por** . **Claves Count Distinct** y **Escala Count Distinct** hacen referencia al número de valores distintos que se esperan como resultado de una operación **Recuento distinto** .  
  
### <a name="options"></a>.  
 **Escala de claves**  
 Si lo desea, especifique el número aproximado de claves que espera la agregación. La transformación utiliza esta información para optimizar el tamaño de caché inicial. De forma predeterminada, el valor de esta opción es **No especificado**. Si se especifica tanto **Escala de claves** como **Número de claves** , prevalece la opción **Número de claves** .  
  
|Valor|Description|  
|-----------|-----------------|  
|No especificado|No se utiliza la propiedad **Escala de claves** .|  
|Baja|La agregación podrá escribir aproximadamente 500 000 claves.|  
|Media|La agregación podrá escribir aproximadamente 5.000.000 claves.|  
|Alta|La agregación podrá escribir más de 25.000.000 claves.|  
  
 **Número de claves**  
 Si lo desea, especifique el número exacto de claves que espera la agregación. La transformación utiliza esta información para optimizar el tamaño de caché inicial. Si se especifica tanto **Escala de claves** como **Número de claves** , prevalece la opción **Número de claves** .  
  
 **Escala Count Distinct**  
 Opcionalmente, puede especificar el número aproximado de valores DISTINCT que podrá escribir la agregación. De forma predeterminada, el valor de esta opción es **No especificado**. Si se especifica tanto **Escala Count Distinct** como **Claves Count Distinct** , prevalece la opción **Claves Count Distinct** .  
  
|Valor|Description|  
|-----------|-----------------|  
|No especificado|No se utiliza la propiedad CountDistinctScale.|  
|Baja|La agregación podrá escribir aproximadamente 500.000 valores DISTINCT.|  
|Media|La agregación podrá escribir aproximadamente 5 000 000 valores DISTINCT.|  
|Alta|La agregación podrá escribir más de 25.000.000 valores DISTINCT.|  
  
 **Claves Count Distinct**  
 Opcionalmente, puede especificar el número exacto de valores DISTINCT que podrá escribir la agregación. Si se especifica tanto **Escala Count Distinct** como **Claves Count Distinct** , prevalece la opción **Claves Count Distinct** .  
  
 **Factor de ampliación automática**  
 Utilice un valor comprendido entre 1 y 100 para especificar el porcentaje en el que se puede ampliar la memoria durante la agregación. De forma predeterminada, el valor de esta opción es **25%**.  
  
## <a name="see-also"></a>Ver también  
 [Flujo de datos](../../../integration-services/data-flow/data-flow.md)   
 [Transformaciones de Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
