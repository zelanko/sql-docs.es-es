---
title: Uso de datos de cubos OLAP en R - SQL Server Machine Learning Services
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: e55093c83e9a306a06235d6bb613dac78d4677ce
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62642307"
---
# <a name="using-data-from-olap-cubes-in-r"></a>Uso de datos de cubos OLAP en R
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

El **olapR** paquete es un paquete de R proporcionados por Microsoft para su uso con Machine Learning Server y SQL Server, que le permite ejecutar consultas MDX para obtener datos de cubos OLAP. Con este paquete, no es necesario crear servidores vinculados ni limpiar conjuntos de filas planas; puede obtener los datos OLAP directamente desde R.

En este artículo se describe la API, junto con información general de OLAP y MDX para los usuarios de R que podría ser nuevo para bases de datos de cubo multidimensional.

> [!IMPORTANT]
> Una instancia de Analysis Services puede admitir convencionales cubos multidimensionales o modelos tabulares, pero una instancia no admite ambos tipos de modelos. Por lo tanto, antes de intentar crear una consulta MDX en un cubo, compruebe que la instancia de Analysis Services contiene los modelos multidimensionales.

## <a name="what-is-an-olap-cube"></a>¿Qué es un cubo OLAP?

OLAP es la abreviatura de Online Analytical Processing. Soluciones OLAP se utilizan ampliamente para capturar y almacenar datos críticos del negocio con el tiempo. Hay una serie de herramientas, paneles y visualizaciones que usan datos OLAP para el análisis empresarial. Para obtener más información, consulte [procesamiento analítico en línea](https://en.wikipedia.org/wiki/Online_analytical_processing).

Microsoft proporciona [Analysis Services](https://docs.microsoft.com/sql/analysis-services/analysis-services), que le permite diseñar, implementar y consultar datos OLAP en forma de _cubos_ o _los modelos tabulares_. Un cubo es una base de datos multidimensional. _Dimensiones_ son como las facetas de los datos o los factores de R: usar dimensiones para identificar un determinado subconjunto de datos que desea resumir o analizar. Por ejemplo, el tiempo es una dimensión importante, tanta para que muchas soluciones OLAP incluyen varios calendarios definidos de forma predeterminada, que se usará al segmentar y resumir los datos. 

Por motivos de rendimiento, una base de datos OLAP a menudo calcula resúmenes (o _agregaciones_) de antemano y, a continuación, almacenarlos para una recuperación más rápida. Los resúmenes se basan en *medidas*, que representan las fórmulas que se pueden aplicar a datos numéricos. Usar las dimensiones para definir un subconjunto de datos y, a continuación, calcular la medida a esos datos. Por ejemplo, podría usar una medida para calcular las ventas totales para una determinada línea de producto durante varios trimestres menos los impuestos, para informar de los costos del envío promedio para un proveedor determinado, salarios acumulativas año hasta la fecha de pago y así sucesivamente.

MDX, abreviatura de expresiones multidimensionales, es el idioma que se usa para consultar los cubos. Normalmente, una consulta MDX contiene una definición de datos que incluye una o más dimensiones y al menos una medida, aunque las consultas MDX pueden obtener considerablemente más complejas e incluir windows graduales, acumulativas promedios, sumas, rangos o percentiles. 

Estos son algunos otros términos que podrían ser útiles para comenzar a crear consultas MDX:

+ *Segmentación* toma un subconjunto del cubo mediante el uso de valores de una sola dimensión.

+ El*desglose* crea un subcubo al especificar un intervalo de valores en varias dimensiones.

+ La*obtención de detalles* va desde un resumen a los detalles.

+ La*exploración* pasa de los detalles a un mayor nivel de agregación.

+ La*acumulación* resume los datos en una dimensión.

+ La*dinamización* gira el cubo o la selección de datos.

## <a name="how-to-use-olapr-to-create-mdx-queries"></a>Cómo usar olapR para crear consultas MDX

El siguiente artículo proporciona ejemplos detallados de la sintaxis para crear o ejecutar consultas en un cubo:

+ [Cómo crear consultas MDX con R](../../advanced-analytics/r/how-to-create-mdx-queries-using-olapr.md)

## <a name="olapr-api"></a>olapR API

El paquete **olapR** admite dos métodos de creación de consultas MDX:

- **Use el Generador MDX.** Usar las funciones de R en el paquete para generar una consulta MDX simple, elección de un cubo y, a continuación, estableciendo los ejes y segmentaciones de datos. Se trata de una manera fácil de crear una consulta MDX válida si no tiene acceso a las herramientas tradicionales de OLAP o no tiene un conocimiento profundo del lenguaje MDX.

    No todas las consultas MDX pueden crearse mediante el uso de este método, ya que MDX puede ser complejo. Sin embargo, esta API admite la mayoría de las operaciones más habituales y útiles, como segmento, dice, obtención de detalles, paquete acumulativo de actualizaciones y dinámica en N dimensiones.

+ **Copie y pegue el MDX tiene el formato correcto.** Crear manualmente y, a continuación, pegue en cualquier consulta MDX. Esta opción es mejor si tiene consultas MDX existentes que desea volver a usar, o si la consulta que desea compilar es demasiado compleja para **olapR** para controlar.

    Después de compilar el MDX con cualquier utilidad de cliente, como SSMS o Excel, guarde la cadena de consulta. Proporcione esta cadena MDX como argumento a la *controlador de consultas SSAS* en el **olapR** paquete. El proveedor envía la consulta al servidor de Analysis Services especificado y devuelve los resultados a R. 

Para obtener ejemplos de cómo crear un MDX consulta o ejecutan una consulta MDX existente, consulte [cómo crear consultas MDX con R](../../advanced-analytics/r/how-to-create-mdx-queries-using-olapr.md).

## <a name="known-issues"></a>Problemas conocidos

Esta sección enumeran algunos problemas conocidos y preguntas comunes sobre la **olapR** paquete.

### <a name="tabular-model-support"></a>Compatibilidad con el modelo tabular

Si se conecta a una instancia de Analysis Services que contiene un modelo tabular, el `explore` función notifica el éxito con un valor devuelto de TRUE. Sin embargo, los objetos de modelo tabular son diferentes de objetos multidimensionales, y la estructura de una base de datos multidimensional es diferente de un modelo tabular.

Si bien DAX (expresiones de análisis de datos) es el idioma que se utiliza normalmente con los modelos tabulares, puede diseñar consultas MDX válidas en un modelo tabular, si ya está familiarizado con MDX. No puede usar los constructores olapR para generar consultas MDX válidas en un modelo tabular.

Sin embargo, las consultas MDX son una forma eficaz para recuperar datos de un modelo tabular. Si necesita obtener datos de un modelo tabular para su uso en R, tenga en cuenta estos métodos:

+ Habilitar DirectQuery en el modelo y agregar el servidor como un servidor vinculado en SQL Server. 
+ Si se creó el modelo tabular en un data mart relacional, obtener los datos directamente desde el origen.

### <a name="how-to-determine-whether-an-instance-contains-tabular-or-multidimensional-models"></a>Cómo determinar si una instancia contiene los modelos tabulares o multidimensionales

Una única instancia de Analysis Services puede contener sólo un tipo de modelo, aunque puede contener varios modelos. El motivo es que existen diferencias fundamentales entre los modelos tabulares y los modelos multidimensionales que controlen la forma en que se almacenan y procesan los datos. Por ejemplo, los modelos tabulares se almacenan en memoria y aprovechan los índices de almacén de columnas para realizar cálculos muy rápidos. En los modelos multidimensionales, se almacenan datos en disco y las agregaciones se definen de antemano y recuperar usando consultas MDX.

Si se conecta a Analysis Services utiliza a un cliente como SQL Server Management Studio, puede indicar un vistazo qué tipo de modelo es compatible, examinando el icono de la base de datos.

También puede ver y consultar las propiedades del servidor para determinar qué tipo de modelo de la instancia admite. El **modo servidor** propiedad admite dos valores: _multidimensionales_ o _tabular_.

Consulte el artículo siguiente para obtener información general acerca de los dos tipos de modelos:

+ [Comparación de modelos multidimensionales y tabulares](https://docs.microsoft.com/sql/analysis-services/comparing-tabular-and-multidimensional-solutions-ssas)

Consulte el artículo siguiente para obtener información sobre cómo consultar las propiedades del servidor:

+ [OLE DB para los conjuntos de filas de esquema OLAP](https://docs.microsoft.com/bi-reference/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets)

### <a name="writeback-is-not-supported"></a>No se admite la escritura diferida de contraseñas

No es posible volver a escribir los resultados de cálculos de R personalizados en el cubo.

En general, incluso cuando un cubo está habilitado para la escritura diferida, se admiten solo las operaciones limitadas y podría requerirse una configuración adicional. Se recomienda usar MDX para dichas operaciones.

+ [Dimensiones habilitadas para escritura](https://docs.microsoft.com/sql/analysis-services/multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions)
+ [Particiones habilitadas para escritura](https://docs.microsoft.com/sql/analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-write-enabled-partitions)
+ [Conjunto personalizado de acceso a datos de celda](https://docs.microsoft.com/sql/analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services)

### <a name="long-running-mdx-queries-block-cube-processing"></a>Las consultas MDX de larga ejecución bloquear el procesamiento del cubo

Aunque el **olapR** paquete realiza solo operaciones de lectura, las consultas MDX pueden crear bloqueos que impiden que se está procesando el cubo de ejecución prolongada. Pruebe siempre las consultas MDX de antemano para que sepa la cantidad de datos se debe devolver.

Si intenta conectarse a un cubo que se bloquea, podría obtener un error que no se puede alcanzar el almacenamiento de datos de SQL Server. Las resoluciones sugeridas incluyen habilitar conexiones remotas, comprobando el servidor o nombre de instancia y así sucesivamente; Sin embargo, considere la posibilidad de una conexión abierta anterior.

Un administrador SSAS puede evitar problemas de bloqueo mediante la identificación y finalizar las sesiones abiertas. Una propiedad de tiempo de espera también puede aplicarse a las consultas MDX en el nivel de servidor para forzar la finalización de todas las consultas de larga ejecución.

## <a name="resources"></a>Recursos

Si está familiarizado con OLAP o con las consultas MDX, vea estos artículos de Wikipedia: 

+ [Cubos OLAP](https://en.wikipedia.org/wiki/OLAP_cube)
+ [Consultas MDX](https://en.wikipedia.org/wiki/MultiDimensional_eXpressions)
