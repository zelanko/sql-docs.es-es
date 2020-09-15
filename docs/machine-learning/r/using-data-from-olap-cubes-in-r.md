---
title: Uso de datos de cubos OLAP en R
description: Este artículo describe la API de olapR, junto con una introducción a OLAP y MDX para los usuarios de R que podrían ser nuevos en las bases de datos de cubos multidimensionales.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 04/15/2018
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 4ae9985ae7d203387eb268a50d97ee91849b33a8
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/13/2020
ms.locfileid: "88180452"
---
# <a name="using-data-from-olap-cubes-in-r"></a>Uso de datos de cubos OLAP en R
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

El paquete de **OLAP** es un paquete de R, proporcionado por Microsoft para su uso con Machine Learning Server y SQL Server, que le permite ejecutar consultas MDX para obtener datos de cubos OLAP. Con este paquete, no necesita crear servidores vinculados ni limpiar conjuntos de filas planas; se pueden obtener datos OLAP directamente de R.

Este artículo describe la API, junto con una introducción a OLAP y MDX para los usuarios de R que podrían ser nuevos en las bases de datos de cubos multidimensionales.

> [!IMPORTANT]
> Una instancia de Analysis Services puede admitir cubos multidimensionales convencionales o modelos tabulares, pero una instancia no puede admitir ambos tipos de modelos. Por lo tanto, antes de intentar crear una consulta MDX en un cubo, compruebe que la instancia de Analysis Services contiene modelos multidimensionales.

## <a name="what-is-an-olap-cube"></a>¿Qué es un cubo OLAP?

OLAP es la forma abreviada para designar el procesamiento analítico en línea. Las soluciones OLAP se usan mucho para capturar y almacenar datos empresariales críticos a lo largo del tiempo. Hay una serie de herramientas, paneles y visualizaciones que usan datos OLAP para el análisis empresarial. Para obtener más información, vea [Procesamiento analítico en línea](https://en.wikipedia.org/wiki/Online_analytical_processing).

Microsoft proporciona [Analysis Services](https://docs.microsoft.com/sql/analysis-services/analysis-services), que permite diseñar, implementar y consultar datos OLAP en forma de _cubos_ o _modelos tabulares_. Un cubo es una base de datos multidimensional. Las _dimensiones_ son similares a las de los datos, o factores en R: las dimensiones se utilizan para identificar un subconjunto determinado de datos que desea resumir o analizar. Por ejemplo, el tiempo es una dimensión importante, tanto para que muchas soluciones OLAP incluyan varios calendarios definidos de forma predeterminada, como para usarlo al segmentar y resumir los datos. 

Por motivos de rendimiento, una base de datos OLAP calcula normalmente resúmenes (o _agregaciones_) de antemano y, a continuación, los almacena para una recuperación más rápida. Los resúmenes se basan en *medidas*, que representan las fórmulas que se pueden aplicar a los datos numéricos. Las dimensiones se utilizan para definir un subconjunto de datos y, a continuación, se calcula la medida sobre dichos datos. Por ejemplo, se usaría una medida para calcular las ventas totales de una determinada línea de producto en varios trimestres menos impuestos, para informar del promedio de costos de envío de un proveedor determinado, los salarios acumulados anuales hasta la fecha pagados, etc.

MDX, la abreviatura que se utiliza para hacer referencia a las expresiones multidimensionales, es el lenguaje que se usa para consultar los cubos. Una consulta MDX contiene normalmente una definición de datos que incluye una o más dimensiones, y al menos una medida, aunque las consultas MDX pueden ser considerablemente más complejas e incluir ventanas con desplazamiento, promedios acumulados, sumas, clasificaciones o percentiles. 

Estos son algunos otros términos que pueden resultar útiles al empezar a crear consultas MDX:

+ La *segmentación* toma un subconjunto del cubo usando valores de una sola dimensión.

+ El*desglose* crea un subcubo al especificar un intervalo de valores en varias dimensiones.

+ La*obtención de detalles* va desde un resumen a los detalles.

+ La*exploración* pasa de los detalles a un mayor nivel de agregación.

+ La*acumulación* resume los datos en una dimensión.

+ La*dinamización* gira el cubo o la selección de datos.

## <a name="how-to-use-olapr-to-create-mdx-queries"></a>Cómo usar olapR para crear consultas MDX

En el siguiente artículo se proporcionan ejemplos detallados de la sintaxis para crear o ejecutar consultas en un cubo:

+ [Cómo crear consultas MDX con R](../../machine-learning/r/how-to-create-mdx-queries-using-olapr.md)

## <a name="olapr-api"></a>API de olapR

El paquete **olapR** admite dos métodos de creación de consultas MDX:

- **Uso del generador MDX.** Utilice las funciones de R en el paquete para generar una consulta MDX simple, eligiendo un cubo y, a continuación, estableciendo los ejes y las segmentaciones. Esta es una manera fácil de crear consultas MDX válidas si no tiene acceso a herramientas tradicionales de OLAP o no tenga un conocimiento profundo del lenguaje MDX.

    No todas las consultas MDX se pueden crear con este método, ya que MDX puede ser complejo. Sin embargo, esta API admite la mayoría de las operaciones más habituales y útiles, como segmentar, desglosar, obtener detalles, acumular y dinamizar en N dimensiones.

+ **Copiado y pegado de MDX con formato correcto.** Cree manualmente y luego pegue en cualquier consulta MDX. Esta opción es la mejor si tiene consultas MDX existentes que quiere volver a usar o si la consulta que quiere compilar es demasiado compleja para que **olapR** la controle.

    Después de crear el MDX con cualquier utilidad de cliente, como SSMS o Excel, guarde la cadena de consulta. Proporcione esta cadena MDX como argumento para el *controlador de consultas SSAS* en el paquete de **olapR**. El proveedor envía la consulta al servidor de Analysis Services especificado y vuelve a pasar los resultados a R. 

Para ver ejemplos de cómo compilar una consulta MDX o ejecutar una consulta MDX existente, vea [Cómo crear consultas MDX con R](../../machine-learning/r/how-to-create-mdx-queries-using-olapr.md).

## <a name="known-issues"></a>Problemas conocidos

En esta sección se enumeran algunos problemas conocidos y preguntas comunes sobre el paquete de **olapR**.

### <a name="tabular-model-support"></a>Compatibilidad con modelos tabulares

Si conecta una instancia de Analysis Services que contiene un modelo tabular, la función `explore` notifica el éxito con un valor devuelto de TRUE. Sin embargo, los objetos de modelo tabular son diferentes de los objetos multidimensionales y la estructura de una base de datos multidimensional es diferente a la de un modelo tabular.

Aunque DAX (Expresiones de análisis de datos) es el lenguaje que se suele usar con los modelos tabulares, puede diseñar consultas MDX válidas en un modelo tabular si ya está familiarizado con MDX. No puede utilizar los constructores de olapR para crear consultas MDX válidas en un modelo tabular.

Sin embargo, las consultas MDX son una forma ineficaz de recuperar datos de un modelo tabular. Si necesita obtener datos de un modelo tabular para su uso en R, le recomendamos usar estos métodos en su lugar:

+ Habilite DirectQuery en el modelo y agregue el servidor como servidor vinculado en SQL Server. 
+ Si el modelo tabular se ha creado en un data mart relacional, obtenga los datos directamente del origen.

### <a name="how-to-determine-whether-an-instance-contains-tabular-or-multidimensional-models"></a>Cómo determinar si una instancia contiene modelos tabulares o multidimensionales

Una sola instancia de Analysis Services solo puede contener un tipo de modelo, aunque puede contener varios modelos. La razón es que existen diferencias fundamentales entre los modelos tabulares y los modelos multidimensionales que controlan la forma en que se almacenan y procesan los datos. Por ejemplo, los modelos tabulares se almacenan en la memoria y aprovechan los índices de almacén de columnas para realizar cálculos muy rápidos. En los modelos multidimensionales, los datos se almacenan en el disco y las agregaciones se definen de antemano y se recuperan mediante consultas MDX.

Si se conecta a Analysis Services mediante un cliente como SQL Server Management Studio, puede conocer inmediatamente qué tipo de modelo se admite, examinando el icono de la base de datos.

También puede ver y consultar las propiedades del servidor para determinar qué tipo de modelo admite la instancia. La propiedad **Modo de servidor** admite dos valores: _multidimensional_ o _tabular_.

Vea el artículo siguiente para obtener información general sobre los dos tipos de modelos:

+ [Comparación de modelos multidimensionales y tabulares](https://docs.microsoft.com/sql/analysis-services/comparing-tabular-and-multidimensional-solutions-ssas)

Vea el siguiente artículo para obtener información acerca de las propiedades del servidor:

+ [OLE DB para los conjuntos de filas de esquema OLAP](https://docs.microsoft.com/previous-versions/sql/sql-server-2012/ms126079(v=sql.110))

### <a name="writeback-is-not-supported"></a>No se admite la reescritura

No es posible volver a escribir los resultados de los cálculos de R personalizados en el cubo.

En general, incluso cuando un cubo está habilitado para la reescritura, solo se admiten operaciones limitadas y es posible que se requiera una configuración adicional. Recomendamos usar MDX para dichas operaciones.

+ [Dimensiones habilitadas para escritura](https://docs.microsoft.com/sql/analysis-services/multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions)
+ [Particiones habilitadas para escritura](https://docs.microsoft.com/sql/analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-write-enabled-partitions)
+ [Establecimiento del acceso personalizado a los datos de las celdas](https://docs.microsoft.com/sql/analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services)

### <a name="long-running-mdx-queries-block-cube-processing"></a>Las consultas MDX de ejecución prolongada bloquean el procesamiento de cubos

Aunque el paquete de **olapR** solo realiza operaciones de lectura, las consultas MDX de ejecución prolongada pueden crear bloqueos que impiden que se procese el cubo. Pruebe siempre las consultas MDX de antemano para saber cuántos datos deben devolverse.

Si intenta conectarse a un cubo que está bloqueado, es posible que reciba un error que le informará de que no se puede alcanzar el almacenamiento de datos de SQL Server. Las resoluciones sugeridas incluyen la habilitación de conexiones remotas, la comprobación del nombre del servidor o de la instancia, etc. Sin embargo, tenga en cuenta la posibilidad de que exista una conexión abierta anterior.

Un administrador de SSAS puede evitar problemas de bloqueo mediante la identificación y finalización de las sesiones abiertas. También se puede aplicar una propiedad de tiempo de expiración a las consultas MDX en el nivel de servidor para forzar la finalización de todas las consultas de ejecución prolongada.

## <a name="resources"></a>Recursos

Si no está familiarizado con OLAP o con las consultas MDX, vea estos artículos de Wikipedia: 

+ [Cubos OLAP](https://en.wikipedia.org/wiki/OLAP_cube)
+ [Consultas MDX](https://en.wikipedia.org/wiki/MultiDimensional_eXpressions)
