---
title: Transformación Agregado| Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.aggregatetrans.f1
helpviewer_keywords:
- IsBig property
- aggregate functions [Integration Services]
- Aggregate transformation [Integration Services]
- large data, SSIS transformations
ms.assetid: 2871cf2a-fbd3-41ba-807d-26ffff960e81
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4759050a9453e1925ea47bc3dbf66d13aa821feb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62770641"
---
# <a name="aggregate-transformation"></a>Transformación Agregado
  La transformación Agregado aplica funciones de agregado, como Average, a los valores de columnas y copia los resultados en la salida de transformación. Además de las funciones de agregado, la transformación proporciona la cláusula GROUP BY, que se puede usar para especificar los grupos en los que se debe realizar el agregado.  
  
## <a name="operations"></a>Operaciones  
 La transformación Agregado admite las siguientes operaciones.  
  
|Operación|Descripción|  
|---------------|-----------------|  
|GROUP BY|Divide los conjuntos de datos en grupos. Se pueden usar columnas de cualquier tipo de datos para la agrupación. Para más información, vea [GROUP BY &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-group-by-transact-sql).|  
|Sum|Suma los valores de una columna. Solo podrán sumarse las columnas con tipos de datos numéricos. Para más información, vea [SUM &#40;Transact-SQL&#41;](/sql/t-sql/functions/sum-transact-sql).|  
|Promedio|Devuelve la media de los valores de columna de una columna. Solo podrá calcularse la media de las columnas con tipos de datos numéricos. Para más información, vea [AVG &#40;Transact-SQL&#41;](/sql/t-sql/functions/avg-transact-sql).|  
|Count|Devuelve el número de elementos de un grupo. Para más información, vea [COUNT &#40;Transact-SQL&#41;](/sql/t-sql/functions/count-transact-sql).|  
|COUNT DISTINCT|Devuelve el número de valores únicos distintos de NULL de un grupo.|  
|Mínima|Devuelve el valor mínimo en un grupo. Para más información, vea [MIN &#40;Transact-SQL&#41;](/sql/t-sql/functions/min-transact-sql). En comparación con la función MIN de Transact-SQL, esta operación se puede usar únicamente con tipos de datos numéricos, de fecha y hora.|  
|Máximo|Devuelve el valor máximo en un grupo. Para más información, vea [MAX &#40;Transact-SQL&#41;](/sql/t-sql/functions/max-transact-sql). En comparación con la función MAX de Transact-SQL, esta operación se puede usar únicamente con tipos de datos numéricos, de fecha y hora.|  
  
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
  
 Esta transformación no pasa por ninguna columna, sino que crea nuevas columnas en el flujo de datos para los datos que publica. Solo las columnas de entrada a las que se aplican las funciones de agregado o las columnas de entrada que usa la transformación para agrupar se copian en la salida de transformación. Por ejemplo, una entrada de transformación Agregado puede tener tres columnas: **PaísRegión**, **Ciudad** y **Población**. La transformación agrupa de acuerdo con la columna **CountryRegion** y aplica la función Sum a la columna **Population** . Por tanto, la salida no incluye la columna **City** .  
  
 Puede también agregar varias salidas a la transformación Agregado y dirigir cada agregación a una salida diferente. Por ejemplo, si la transformación Agregado aplica las funciones Sum y Average, cada agregación se puede dirigir a una salida diferente.  
  
 Puede aplicar varias agregaciones a una sola columna de entrada. Por ejemplo, si quiere los valores de suma y promedio de una columna de entrada denominada **Sales**, puede configurar la transformación para aplicar las funciones Sum y Average a la columna **Sales** .  
  
 La transformación Agregado tiene una entrada y una o varias salidas. No admite una salida de error.  
  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información sobre las propiedades que se pueden configurar en el cuadro de diálogo **Editor de transformación Agregado** , haga clic en uno de los siguientes temas:  
  
-   [Editor de transformación Agregado &#40;pestaña Agregaciones&#41;](../../aggregate-transformation-editor-aggregations-tab.md)  
  
-   [Editor de transformación Agregado &#40;pestaña Avanzadas&#41;](../../aggregate-transformation-editor-advanced-tab.md)  
  
 El cuadro de diálogo **Editor avanzado** indica las propiedades que se pueden establecer mediante programación. Para obtener más información acerca de las propiedades que puede establecer a través del cuadro de diálogo **Editor avanzado** o mediante programación, haga clic en uno de los temas siguientes:  
  
-   [Propiedades comunes](../../common-properties.md)  
  
-   [Propiedades personalizadas de transformación](transformation-custom-properties.md)  
  
 Para obtener más información sobre cómo establecer valores de propiedades, haga clic en uno de los temas siguientes:  
  
-   [Agregar valores en un conjunto de datos mediante la transformación Agregado](aggregate-values-in-a-dataset-by-using-the-aggregate-transformation.md)  
  
-   [Establecer las propiedades de un componente de flujo de datos](../set-the-properties-of-a-data-flow-component.md)  
  
-   [Ordenación de datos para las transformaciones Mezclar y Combinación de mezcla](sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 [Incorporación de valores en un conjunto de datos con la transformación Agregado](aggregate-values-in-a-dataset-by-using-the-aggregate-transformation.md)  
  
## <a name="see-also"></a>Vea también  
 [Flujo de datos](../data-flow.md)   
 [Transformaciones de Integration Services](integration-services-transformations.md)  
  
  
