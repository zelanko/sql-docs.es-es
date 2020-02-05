---
title: Agregar filtros de conjunto de datos, filtros de región de datos y filtros de grupo | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: fcca7243-a702-4725-8e6f-cf118e988acf
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: d3ab6708212ce429f2abacae4353670235a687cb
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "65582055"
---
# <a name="add-dataset-filters-data-region-filters-and-group-filters"></a>Agregar filtros de conjunto de datos, filtros de región de datos y filtros de grupo
  En un informe, un filtro es una parte de un conjunto de datos, una región de datos o un grupo de regiones de datos que se crea para restringir los datos que se usan en el informe. Los filtros pueden ayudarle a controlar los datos de informe si no puede cambiar la consulta de conjunto de datos, por ejemplo si usa un conjunto de datos compartido.  
  
 Los filtros le ayudan a controlar los datos que se ven y se procesan en los informes. Puede especificar filtros para un conjunto de datos, una región de datos o un grupo, o para cualquier combinación de estos elementos.  
  
 Para más información, vea [Agregar un filtro a un conjunto de datos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-data/add-a-filter-to-a-dataset-report-builder-and-ssrs.md) y [Ejemplos de ecuaciones de filtro &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/filter-equation-examples-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="When"></a> Elegir cuándo se establecerá un filtro  
 Cuando no pueda filtrar los datos en el origen, especifique filtros para los elementos de informe. Por ejemplo, use filtros de informe cuando el origen de datos no admita parámetros de consulta, cuando tenga que ejecutar procedimientos almacenados y no pueda modificar la consulta, o cuando una instantánea de informe con parámetros muestre datos personalizados para usuarios diferentes.  
  
 Puede filtrar datos de informe antes o después de recuperarlos para un conjunto de datos de informe. Para filtrar los datos antes de su recuperación, cambie la consulta de cada conjunto de datos. Cuando se filtran los datos de la consulta, se filtran los datos en el origen de datos, lo que reduce la cantidad de datos que es necesario recuperar y procesar en un informe. Para filtrar los datos después de su recuperación, cree expresiones de filtro en el informe. Puede establecer expresiones de filtro para un conjunto de datos, una región de datos o un grupo, incluidos los grupos de detalles. También puede incluir parámetros en las expresiones de filtro; esto proporciona una manera de filtrar datos de valores o usuarios específicos, por ejemplo, puede filtrar según un valor que identifica al usuario que ve el informe.  
  
##  <a name="Where"></a> Elegir dónde se establecerá un filtro  
 Determine el lugar donde desea establecer un filtro basándose en el efecto que desea conseguir en el informe. En tiempo de ejecución, el procesador de informes aplica los filtros en el orden siguiente: en el conjunto de datos, a continuación, en la región de datos y, por último, en los grupos, comenzando en la parte superior de cada jerarquía de grupo. En una tabla, matriz o lista, los filtros de los grupos de filas, los grupos de columnas y los grupos adyacentes se aplican de forma independiente. En un gráfico, también se aplican de forma independiente los filtros de los grupos de categorías y los grupos de series. Cuando el procesador de informes aplica el filtro, todas las ecuaciones de filtro se aplican en el orden en el que están definidas en la página **Filtro** del cuadro de diálogo **Propiedades** para cada elemento de informe; esto equivale a combinarlas con las operaciones Boolean AND.  
  
 En la lista siguiente, se compara el efecto de establecer filtros en elementos de informe diferentes:  
  
-   **En el conjunto de datos** : establezca un filtro en el conjunto de datos cuando desee que una o más regiones de datos que están enlazadas a un único conjunto de datos se filtren de la misma manera. Por ejemplo, establezca el filtro en el conjunto de datos que está enlazado a una tabla que muestra los datos de ventas y a un gráfico que muestra los mismos datos.  
  
-   **En la región de datos** : establezca un filtro en la región de datos cuando desee que una o más regiones de datos que están enlazadas a un único conjunto de datos proporcionen una vista diferente de dicho conjunto de datos. Por ejemplo, establezca el filtro en una región de datos Tabla para mostrar los diez establecimientos con más ventas y en otra región de datos Tabla para mostrar los diez establecimientos con menos ventas en el mismo informe.  
  
-   **En los grupos de filas o de columnas de una región de datos Tablix** : establezca un filtro en un grupo cuando desee incluir o excluir ciertos valores para que una expresión de grupo controle qué valores de grupo deben aparecer en la tabla, la matriz o la lista.  
  
-   **En el grupo de detalles de una región de datos Tablix** : establezca un filtro en el grupo de detalles cuando tenga varios grupos de detalles para una región de datos y desee que cada uno de ellos muestre un conjunto de datos diferente del conjunto de datos.  
  
-   **En los grupos de series o de categorías de una región de datos Gráfico** : establezca un filtro en un grupo de series o de categorías cuando desee incluir o excluir ciertos valores para que una expresión de grupo controle qué valores deben aparecer en el gráfico.  
  
 Volver al principio  
  
##  <a name="FilterEquations"></a> Descripción de una ecuación de filtro  
 En tiempo de ejecución, el procesador de informes convierte el valor en el tipo de datos especificado y, a continuación, usa al operador especificado para comparar la expresión y el valor. En la lista siguiente, se describe cada una de las partes de la ecuación de filtro:  
  
-   **Expresión** : define lo que se va a filtrar. Normalmente, se trata de un campo de conjunto de datos.  
  
-   **Tipo de datos** : especifica el tipo de datos que se usará cuando el procesador de informes evalúe la ecuación de filtro en tiempo de ejecución. El tipo de datos que seleccione debe ser uno de los tipos de datos admitidos por el esquema de definición de informe.  
  
-   **Operador** : define cómo comparar las dos partes de la ecuación de filtro.  
  
-   **Valor** : define la expresión que se usará en la comparación.  
  
 En las secciones siguientes, se describe cada una de las partes de la ecuación de filtro.  
  
### <a name="expression"></a>Expression  
 Cuando el procesador de informes evalúe la ecuación de filtro en tiempo de ejecución, los tipos de datos de la expresión y el valor deberán ser los mismos. La extensión de procesamiento de datos o el proveedor de datos que se usa para recuperar los datos del origen de datos determinará el tipo de datos del campo que seleccione en **Expresión** . Los valores predeterminados de **Valor** determinan el tipo de datos de la expresión especificada en Valor [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Los tipos de datos admitidos para una definición de informe determinan las opciones para el tipo de datos. El proveedor de datos puede convertir los valores de la base de datos en un tipo CLR.  
  
### <a name="data-type"></a>Tipo de datos  
 Para que el procesador de informes pueda comparar dos valores, los tipos de datos deben ser los mismos. En la tabla siguiente, se especifica la asignación entre los tipos de datos CLR y los tipos de datos de la definición de informe. Los datos que recupere de un origen de datos pueden convertirse en un tipo de datos diferente cuando sean datos de informe.  
  
|**Tipo de datos del esquema de definición de informe**|**Tipos CLR**|  
|--------------------------------------------|-----------------------|  
|**Boolean**|**Boolean**|  
|**DateTime**|**DateTime**, **DateTimeOffset**|  
|**Entero**|**Int16**, **Int32**, **UInt16**, **Byte**, **SByte**|  
|**Float**|**Single**, **Double**, **Decimal**|  
|**Texto**|**String**, **Char**, **GUID**, **Timespan**|  
  
 En los casos en que es necesario especificar un tipo de datos, puede especificar su propia conversión en la parte Valor de la expresión.  
  
### <a name="operator"></a>Operator  
 En la tabla siguiente, se especifican los operadores que puede usar en una ecuación de filtro y lo que el procesador de informes usa para evaluar la ecuación de filtro.  
  
|Operator|Acción|  
|--------------|------------|  
|**Equal, Like, NotEqual, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual**|Compara la expresión con un valor.|  
|**TopN, BottomN**|Compara la expresión con un valor **Integer** .|  
|**TopPercent, BottomPercent**|Compara la expresión con un valor **Integer** o **Float** .|  
|**Entre**|Prueba si la expresión está entre dos valores, ambos inclusive.|  
|**In**|Prueba si la expresión está dentro de un conjunto de valores.|  
  
### <a name="value"></a>Value  
 La expresión de valor especifica la parte final de la ecuación de filtro. El procesador de informes convierte la expresión evaluada en el tipo de datos que especificó y, a continuación, evalúa la ecuación de filtro completa para determinar si los datos especificados en Expresión pasan a través del filtro.  
  
 Para convertir en un tipo de datos que no es un tipo de datos CLR estándar, debe modificar la expresión para que realice la conversión de manera explícita. Puede usar las funciones de conversión del cuadro de diálogo **Expresión** comprendidas en la categoría **Funciones comunes**, **Conversión**. Por ejemplo, para un campo `ListPrice` que representa datos que están almacenados como un tipo de datos **money** en un origen de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , la extensión de procesamiento de datos devuelve el valor de campo como un tipo de datos <xref:System.Decimal> . Si desea establecer un filtro para usar solo valores mayores que **$50000.00** en la moneda del informe, convierta el valor en Decimal con la expresión `=CDec(50000.00)`.  
  
 Este valor también puede incluir una referencia de parámetro para permitir al usuario seleccionar de forma interactiva el valor por el que va a filtrarse.  
  
 Volver al principio  
  
## <a name="see-also"></a>Consulte también  
 [Usar expresiones en informes &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Parámetros de informe &#40;Generador de informes y Diseñador de informes&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)  
  
  
