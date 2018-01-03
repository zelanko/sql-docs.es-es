---
title: Utilizando los datos de los cubos OLAP en R | Documentos de Microsoft
ms.custom: 
ms.date: 12/08/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: r-services
ms.assetid: 8093599c-8307-4237-983b-0908d0f8ab77
caps.latest.revision: "12"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: afd642bec2af5dc3bd006e1153c61bb19846c6e1
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/20/2017
---
# <a name="using-data-from-olap-cubes-in-r"></a>Utilizando los datos de los cubos OLAP en R

El **olapR** paquete es un paquete de R, proporcionado por Microsoft para su uso con SQL Server y servidor de aprendizaje de máquina, que permite ejecutar consultas MDX para obtener datos de los cubos OLAP. Con este paquete, no necesita crear servidores vinculados o limpiar de conjuntos de filas planas; puede obtener datos OLAP directamente de R.

En este artículo se describe la API, junto con información general de OLAP y MDX para los usuarios de R que podría estar familiarizado con las bases de datos de cubo multidimensional.

> [!IMPORTANT]
> Una instancia de Analysis Services puede admitir convencionales cubos multidimensionales o modelos tabulares, pero una instancia no admite ambos tipos de modelos. Por lo tanto, antes de intentar crear una consulta MDX en un cubo, compruebe que la instancia de Analysis Services contiene los modelos multidimensionales.

## <a name="what-is-an-olap-cube"></a>¿Qué es un cubo OLAP?

OLAP es la abreviatura de Online Analytical Processing. Soluciones OLAP se utilizan ampliamente para capturar y almacenar los datos críticos del negocio con el tiempo. Hay una serie de herramientas, paneles y visualizaciones que usan datos OLAP para el análisis empresarial. Para obtener más información, consulte [procesamiento analítico en línea](https://en.wikipedia.org/wiki/Online_analytical_processing).

Microsoft proporciona [Analysis Services](https://docs.microsoft.com/sql/analysis-services/analysis-services), que le permite diseñar, implementar y consultar los datos OLAP en el formulario de _cubos_ o _los modelos tabulares_. Un cubo es una base de datos multidimensional. _Dimensiones_ son como las facetas de los datos o los factores de R: usar dimensiones para identificar un determinado subconjunto de datos que desea resumir o analizar. Por ejemplo, el tiempo es una dimensión importante, tanta por lo que muchas soluciones OLAP incluyen varios calendarios definidos de forma predeterminada, que se utilizará al segmentar y resumir los datos. 

Por motivos de rendimiento, una base de datos OLAP calcula a menudo resúmenes (o _agregaciones_) de antemano y, a continuación, almacenarlos para una recuperación más rápida. Resúmenes se basan en *medidas*, que representan las fórmulas que se pueden aplicar a los datos numéricos. Usar las dimensiones para definir un subconjunto de datos y, a continuación, calcular la medida con esos datos. Por ejemplo, usaría una medida para calcular las ventas totales para una determinada línea de producto durante varios trimestres menos impuestos, para informar de los costos del envío promedio para un proveedor determinado, sueldo acumulado hasta la fecha de pago y así sucesivamente.

MDX, abreviatura de expresiones multidimensionales, es el idioma que se usa para consultar cubos. Una consulta MDX normalmente contiene una definición de datos que incluye una o más dimensiones y al menos una medida, aunque las consultas MDX pueden obtener mucho más complejas e incluir windows graduales, acumulativas promedios, sumas, rangos o percentiles. 

Estos son algunos de los términos que pueden resultarle útiles al iniciar la creación de consultas MDX:

+ *Segmentación* tiene un subconjunto del cubo mediante el uso de valores de una sola dimensión.

+ El*desglose* crea un subcubo al especificar un intervalo de valores en varias dimensiones.

+ La*obtención de detalles* va desde un resumen a los detalles.

+ La*exploración* pasa de los detalles a un mayor nivel de agregación.

+ La*acumulación* resume los datos en una dimensión.

+ La*dinamización* gira el cubo o la selección de datos.

## <a name="how-to-use-olapr-to-create-mdx-queries"></a>Cómo usar olapR para crear consultas MDX

El artículo siguiente proporciona ejemplos detallados de la sintaxis para crear o ejecutar consultas de un cubo:

+ [Cómo crear consultas MDX mediante R](../../advanced-analytics/r/how-to-create-mdx-queries-using-olapr.md)

## <a name="olapr-api"></a>olapR API

El paquete **olapR** admite dos métodos de creación de consultas MDX:

- **Utilizar el Generador MDX.** Utilizar las funciones de R en el paquete para generar una consulta MDX simple, elegir un cubo y, a continuación, establecer ejes y segmentaciones de datos. Se trata de una manera fácil de crear una consulta MDX válida si no tiene acceso a las herramientas tradicionales de OLAP o no tiene un conocimiento profundo del lenguaje MDX.

    No todas las consultas MDX pueden crearse mediante el uso de este método, dado que MDX puede ser complejo. Sin embargo, esta API admite la mayoría de las operaciones habituales y útiles, incluyendo segmento, dados, obtención de detalles, paquete acumulativo de actualizaciones y dinámica en las dimensiones de N.

+ **Copiar y pegar MDX correcto.** Crear manualmente y, a continuación, pegue en cualquier consulta MDX. Esta opción es el mejor si hay consultas MDX existentes que desea volver a, o si la consulta que desee crear es demasiado compleja para **olapR** a controlar.

    Después de compilar el MDX con cualquier utilidad de cliente, como SSMS o Excel, guarde la cadena de consulta. Proporcione esta cadena MDX como un argumento a la *controlador de consultas SSAS* en el **olapR** paquete. El proveedor envía la consulta al servidor de Analysis Services especificado y devuelve los resultados para R. 

Para obtener ejemplos de cómo compilar un MDX consulta o ejecutan una consulta MDX existente, consulte [cómo crear consultas MDX mediante R](../../advanced-analytics/r/how-to-create-mdx-queries-using-olapr.md).

## <a name="known-issues"></a>Problemas conocidos

Esta sección enumeran algunos problemas conocidos y preguntas comunes sobre la **olapR** paquete.

### <a name="tabular-model-support"></a>Compatibilidad con los modelos tabulares

Si se conecta a una instancia de Analysis Services que contiene un modelo tabular, el `explore` función devuelve el estado correcto con un valor devuelto de TRUE. Sin embargo, los objetos del modelo tabular son diferentes de objetos multidimensionales, y la estructura de una base de datos multidimensional es diferente de un modelo tabular.

Aunque DAX (expresiones de análisis de datos) es el lenguaje que se suele utilizado con los modelos tabulares, puede diseñar consultas MDX válidas en un modelo tabular, si ya está familiarizado con MDX. No puede usar los constructores olapR para generar consultas MDX válidas en un modelo tabular.

Sin embargo, las consultas MDX son una manera eficaz para recuperar datos de un modelo tabular. Si necesita obtener datos de un modelo tabular para su uso en R, considere la posibilidad de estos métodos en su lugar:

+ Habilitar DirectQuery en el modelo y agregar el servidor como un servidor vinculado en SQL Server. 
+ Si el modelo tabular se basa en un puesto de datos relacionales, obtenga los datos directamente desde el origen.

### <a name="how-to-determine-whether-an-instance-contains-tabular-or-multidimensional-models"></a>Cómo determinar si una instancia contiene los modelos tabulares o multidimensionales

Una única instancia de Analysis Services puede contener un solo tipo de modelo, aunque puede contener varios modelos. La razón es que hay diferencias fundamentales entre los modelos tabulares y los modelos multidimensionales que controlan la forma en que se almacenan los datos y se procesan. Por ejemplo, los modelos tabulares se almacenan en memoria y aprovechan los índices de almacén de columnas para realizar cálculos muy rápidos. En modelos multidimensionales, se almacenan datos en disco y las agregaciones se definen de antemano y se recuperan mediante el uso de consultas MDX.

Si se conecta a Analysis Services mediante un cliente como SQL Server Management Studio, puede indicar un vistazo qué tipo de modelo se admite, examinando el icono de la base de datos.

También puede ver y consultar las propiedades del servidor para determinar qué tipo de modelo de la instancia admite. El **modo de servidor** propiedad es compatible con dos valores: _multidimensionales_ o _tabular_.

Vea el artículo siguiente para obtener información general acerca de los dos tipos de modelos:

+ [Comparación de modelos multidimensionales y tabulares](https://docs.microsoft.com/sql/analysis-services/comparing-tabular-and-multidimensional-solutions-ssas)

Vea el artículo siguiente para obtener información sobre cómo consultar las propiedades del servidor:

+ [OLE DB para los conjuntos de filas de esquema OLAP](https://docs.microsoft.com/sql/analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets)

### <a name="writeback-is-not-supported"></a>No se admite la reescritura

No es posible volver a escribir los resultados de cálculos de R personalizados en el cubo.

En general, incluso si un cubo está habilitado para la escritura diferida, se admiten solo las operaciones limitadas y podría ser necesaria una configuración adicional. Se recomienda utilizar MDX para tales operaciones.

+ [Dimensiones habilitadas para escritura](https://docs.microsoft.com/sql/analysis-services/multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions)
+ [Particiones habilitadas para escritura](https://docs.microsoft.com/sql/analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-write-enabled-partitions)
+ [Configurar el acceso personalizado a datos de celda](https://docs.microsoft.com/sql/analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services)

### <a name="long-running-mdx-queries-block-cube-processing"></a>Las consultas MDX de larga ejecución bloquee el procesamiento de cubos

Aunque la **olapR** paquete realiza solo las operaciones de lectura, las consultas MDX pueden crear bloqueos que impiden que se procese el cubo de ejecución prolongada. Pruebe siempre las consultas MDX de antemano para que sepa que se debe devolver la cantidad de datos.

Si intenta conectarse a un cubo que se bloquea, podría obtener un error que no se puede alcanzar el almacén de datos de SQL Server. Las resoluciones sugeridas incluyen la habilitación de las conexiones remotas, comprobando el servidor o nombre de instancia y así sucesivamente; Sin embargo, considere la posibilidad de una conexión abierta anterior.

Un administrador SSAS puede evitar problemas de bloqueo mediante la identificación y terminar sesiones abiertas. Una propiedad de tiempo de espera también puede aplicarse a las consultas MDX en el nivel de servidor para forzar la finalización de todas las consultas de larga duración.

## <a name="resources"></a>Recursos

Si está familiarizado para OLAP o a las consultas MDX, vea estos artículos de Wikipedia: 

+ [Cubos OLAP](https://en.wikipedia.org/wiki/OLAP_cube)
+ [Consultas MDX](https://en.wikipedia.org/wiki/MultiDimensional_eXpressions)
