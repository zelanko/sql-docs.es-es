---
title: Usar datos de cubos OLAP en R
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 3063758e1186dc81e5ce9e70891403e7afd3a89f
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345112"
---
# <a name="using-data-from-olap-cubes-in-r"></a>Usar datos de cubos OLAP en R
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

El  paquete olapr es un paquete de R, proporcionado por Microsoft para su uso con Machine Learning Server y SQL Server, que le permite ejecutar consultas MDX para obtener datos de cubos OLAP. Con este paquete, no es necesario crear servidores vinculados ni limpiar conjuntos de filas planas. puede obtener datos OLAP directamente desde R.

En este artículo se describe la API, junto con una introducción a OLAP y MDX para los usuarios de R que podrían ser nuevos en las bases de datos de cubo multidimensionales.

> [!IMPORTANT]
> Una instancia de Analysis Services puede admitir cubos multidimensionales convencionales o modelos tabulares, pero una instancia de no puede admitir ambos tipos de modelos. Por lo tanto, antes de intentar crear una consulta MDX en un cubo, compruebe que la instancia de Analysis Services contiene modelos multidimensionales.

## <a name="what-is-an-olap-cube"></a>¿Qué es un cubo OLAP?

OLAP es breve para el procesamiento analítico en línea. Las soluciones OLAP se usan ampliamente para capturar y almacenar datos empresariales críticos a lo largo del tiempo. Hay una serie de herramientas, paneles y visualizaciones que usan datos OLAP para el análisis empresarial. Para obtener más información, vea [procesamiento analítico en línea](https://en.wikipedia.org/wiki/Online_analytical_processing).

Microsoft proporciona [Analysis Services](https://docs.microsoft.com/sql/analysis-services/analysis-services), que permite diseñar, implementar y consultar datos OLAP en forma de cubos o  _modelos tabulares_. Un cubo es una base de datos multidimensional. Las _dimensiones_ son similares a las de los datos, o factores en R: las dimensiones se utilizan para identificar un subconjunto determinado de datos que se desea resumir o analizar. Por ejemplo, la hora es una dimensión importante, tanto para que muchas soluciones OLAP incluyan varios calendarios definidos de forma predeterminada, para usarlos al segmentar y resumir los datos. 

Por motivos de rendimiento, una base de datos OLAP calcula a menudo resúmenes (o agregaciones) de antemano y, a continuación, los almacena para una recuperación más rápida. Los resúmenes se basan en *medidas*, que representan fórmulas que se pueden aplicar a datos numéricos. Las dimensiones se utilizan para definir un subconjunto de datos y, a continuación, se calcula la medida sobre esos datos. Por ejemplo, se usaría una medida para calcular el total de ventas de una determinada línea de producto en varios trimestres menos impuestos, para informar de los costos de envío promedio de un proveedor determinado, los salarios acumulados anuales hasta la fecha pagados, etc.

MDX, Short para las expresiones multidimensionales, es el lenguaje que se usa para consultar los cubos. Una consulta MDX contiene normalmente una definición de datos que incluye una o más dimensiones, y al menos una medida, aunque las consultas MDX pueden ser considerablemente más complejas e incluir ventanas graduales, promedios acumulados, sumas, rangos o percentiles. 

Estos son algunos otros términos que pueden resultar útiles al empezar a crear consultas MDX:

+ La segmentación toma un subconjunto del cubo usando valores de una sola dimensión.

+ El*desglose* crea un subcubo al especificar un intervalo de valores en varias dimensiones.

+ La*obtención de detalles* va desde un resumen a los detalles.

+ La*exploración* pasa de los detalles a un mayor nivel de agregación.

+ La*acumulación* resume los datos en una dimensión.

+ La*dinamización* gira el cubo o la selección de datos.

## <a name="how-to-use-olapr-to-create-mdx-queries"></a>Cómo usar olapr para crear consultas MDX

En el siguiente artículo se proporcionan ejemplos detallados de la sintaxis para crear o ejecutar consultas en un cubo:

+ [Cómo crear consultas MDX con R](../../advanced-analytics/r/how-to-create-mdx-queries-using-olapr.md)

## <a name="olapr-api"></a>API de OLAP

El paquete **olapR** admite dos métodos de creación de consultas MDX:

- **Usar el Generador MDX.** Utilice las funciones de R en el paquete para generar una consulta MDX simple, eligiendo un cubo y, a continuación, estableciendo los ejes y las segmentaciones. Esta es una manera fácil de generar una consulta MDX válida si no tiene acceso a las herramientas tradicionales de OLAP o no tiene profundo conocimiento del lenguaje MDX.

    No todas las consultas MDX se pueden crear con este método, ya que MDX puede ser complejo. Sin embargo, esta API es compatible con la mayoría de las operaciones más comunes y útiles, como segmentos, índices, obtención de detalles, acumulación y dinamización en N dimensiones.

+ **Copiar y pegar MDX con formato correcto.** Crear y pegar manualmente en cualquier consulta MDX. Esta opción es la mejor si tiene consultas MDX existentes que desea volver a usar o si la consulta que desea compilar es demasiado compleja para que **olapr** la administre.

    Después de compilar el MDX con cualquier utilidad de cliente, como SSMS o Excel, guarde la cadena de consulta. Proporcione esta cadena MDX como argumento para el *controlador de consultas SSAS* en el paquete **olapr** . El proveedor envía la consulta al servidor de Analysis Services especificado y devuelve los resultados a R. 

Para obtener ejemplos de cómo crear una consulta MDX o ejecutar una consulta MDX existente, consulte [How to Create MDX queries Using R](../../advanced-analytics/r/how-to-create-mdx-queries-using-olapr.md).

## <a name="known-issues"></a>Problemas conocidos

En esta sección se enumeran algunos problemas conocidos y preguntas  comunes sobre el paquete olapr.

### <a name="tabular-model-support"></a>Compatibilidad con modelos tabulares

Si se conecta a una instancia de Analysis Services que contiene un modelo tabular, `explore` la función notifica el éxito con un valor devuelto de true. Sin embargo, los objetos de modelo tabular son diferentes de los objetos multidimensionales y la estructura de una base de datos multidimensional es diferente de la de un modelo tabular.

Aunque DAX (expresiones de análisis de datos) es el lenguaje que se suele usar con los modelos tabulares, puede diseñar consultas MDX válidas en un modelo tabular si ya está familiarizado con MDX. No puede utilizar los constructores de OLAP para generar consultas MDX válidas en un modelo tabular.

Sin embargo, las consultas MDX son una forma ineficaz de recuperar datos de un modelo tabular. Si necesita obtener datos de un modelo tabular para su uso en R, considere estos métodos en su lugar:

+ Habilite DirectQuery en el modelo y agregue el servidor como servidor vinculado en SQL Server. 
+ Si el modelo tabular se compiló en un data mart relacional, obtenga los datos directamente del origen.

### <a name="how-to-determine-whether-an-instance-contains-tabular-or-multidimensional-models"></a>Cómo determinar si una instancia contiene modelos tabulares o multidimensionales

Una sola instancia de Analysis Services solo puede contener un tipo de modelo, aunque puede contener varios modelos. La razón es que existen diferencias fundamentales entre los modelos tabulares y los modelos multidimensionales que controlan la forma en que se almacenan y procesan los datos. Por ejemplo, los modelos tabulares se almacenan en memoria y aprovechan los índices de almacén de columnas para realizar cálculos muy rápidos. En los modelos multidimensionales, los datos se almacenan en el disco y las agregaciones se definen de antemano y se recuperan mediante consultas MDX.

Si se conecta a Analysis Services mediante un cliente como SQL Server Management Studio, puede saber de un vistazo qué tipo de modelo se admite, examinando el icono de la base de datos.

También puede ver y consultar las propiedades del servidor para determinar qué tipo de modelo admite la instancia. La propiedad **modo de servidor** admite dos valores: multidimensional o _tabular_.

Vea el artículo siguiente para obtener información general sobre los dos tipos de modelos:

+ [Comparar modelos multidimensionales y tabulares](https://docs.microsoft.com/sql/analysis-services/comparing-tabular-and-multidimensional-solutions-ssas)

Consulte el siguiente artículo para obtener información acerca de cómo consultar las propiedades del servidor:

+ [OLE DB para los conjuntos de filas de esquema OLAP](https://docs.microsoft.com/bi-reference/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets)

### <a name="writeback-is-not-supported"></a>No se admite la reescritura

No es posible volver a escribir los resultados de los cálculos de R personalizados en el cubo.

En general, incluso cuando un cubo está habilitado para la reescritura, solo se admiten operaciones limitadas y es posible que se necesite una configuración adicional. Se recomienda usar MDX para tales operaciones.

+ [Dimensiones habilitadas para escritura](https://docs.microsoft.com/sql/analysis-services/multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions)
+ [Particiones habilitadas para escritura](https://docs.microsoft.com/sql/analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-write-enabled-partitions)
+ [Establecer el acceso personalizado a los datos de celda](https://docs.microsoft.com/sql/analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services)

### <a name="long-running-mdx-queries-block-cube-processing"></a>Las consultas MDX de ejecución prolongada bloquean el procesamiento de cubos

Aunque el  paquete olapr solo realiza operaciones de lectura, las consultas MDX de ejecución prolongada pueden crear bloqueos que impiden que se procese el cubo. Pruebe siempre las consultas MDX de antemano para saber cuántos datos deben devolverse.

Si intenta conectarse a un cubo que está bloqueado, es posible que reciba un error que le informará de que no se puede alcanzar el almacenamiento de datos de SQL Server. Las resoluciones sugeridas incluyen habilitar conexiones remotas, comprobar el nombre del servidor o de la instancia, etc. sin embargo, tenga en cuenta la posibilidad de una conexión abierta anterior.

Un administrador de SSAS puede evitar problemas de bloqueo mediante la identificación y terminación de las sesiones abiertas. También se puede aplicar una propiedad de tiempo de espera a las consultas MDX en el nivel de servidor para forzar la finalización de todas las consultas de ejecución prolongada.

## <a name="resources"></a>Recursos

Si no está familiarizado con OLAP o con las consultas MDX, consulte estos artículos de Wikipedia: 

+ [Cubos OLAP](https://en.wikipedia.org/wiki/OLAP_cube)
+ [Consultas MDX](https://en.wikipedia.org/wiki/MultiDimensional_eXpressions)
