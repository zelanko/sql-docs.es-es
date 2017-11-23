---
title: Utilizando los datos de los cubos OLAP en R | Documentos de Microsoft
ms.custom: 
ms.date: 11/03/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: R
ms.assetid: 8093599c-8307-4237-983b-0908d0f8ab77
caps.latest.revision: "12"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 1c55a5b834cd91478a87ded7ebb86884117c7bfb
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="using-data-from-olap-cubes-in-r"></a>Utilizando los datos de los cubos OLAP en R

El **olapR** paquete es un paquete de R, proporcionado por Microsoft para su uso con SQL Server R Services y el servidor de aprendizaje de máquina, que permite ejecutar consultas MDX para obtener datos de los cubos OLAP. Con este paquete, no necesita crear servidores vinculados o limpiar de conjuntos de filas planas; datos OLAP se pueden usar directamente en R.

En este artículo se describe la API, junto con información general sobre fo OLAP y MDX para los usuarios de R que podría estar familiarizado con las bases de datos de cubo multidimensional.

## <a name="what-is-an-olap-cube"></a>¿Qué es un cubo OLAP?

OLAP es la abreviatura de Online Analytical Processing. Soluciones OLAP se utilizan ampliamente para capturar y almacenar los datos críticos del negocio con el tiempo. Hay una serie de herramientas, paneles y visualizaciones que usan datos OLAP para el análisis empresarial. Para obtener más información, consulte [procesamiento analítico en línea](https://en.wikipedia.org/wiki/Online_analytical_processing).

Microsoft proporciona [Analysis Services](https://docs.microsoft.com/sql/analysis-services/analysis-services), que le permite diseñar, implementar y consultar los datos OLAP en el formulario de _cubos_ o _los modelos tabulares_. Un cubo es una base de datos multidimensional. _Dimensiones_ son como las facetas de los datos o los factores de R: usar dimensiones para identificar un determinado subconjunto de datos que desea resumir o analizar. Por ejemplo, el tiempo es una dimensión importante, tanta por lo que muchas soluciones OLAP incluyen varios calendarios definidos de forma predeterminada, que se utilizará al segmentar y resumir los datos. 

Por motivos de rendimiento, una base de datos OLAP calcula a menudo resúmenes (o _agregaciones_) de antemano y, a continuación, almacenarlos para una recuperación más rápida. Resúmenes se basan en *medidas*, que representan las fórmulas que se pueden aplicar a los datos numéricos. Usar las dimensiones para definir un subconjunto de datos y, a continuación, calcular la medida con esos datos. Por ejemplo, usaría una medida para calcular las ventas totales para una determinada línea de producto durante varios trimestres menos impuestos, para informar de los costos del envío promedio para un proveedor determinado, sueldo acumulado hasta la fecha de pago y así sucesivamente.

MDX, abreviatura de expresiones multidimensionales, es el idioma que se usa para consultar cubos. Una consulta MDX normalmente contiene una definición de datos que incluye una o más dimensiones y al menos una medida, las consultas MDX de thogh pueden obtener mucho más complejas y se incluyen la implantación de windows, acumulativas promedios o sumas, percentiles. 

Estos son algunos de los términos que pueden resultarle útiles al iniciar la creación de consultas MDX:

+ *Segmentación* tiene un subconjunto del cubo mediante el uso de valores de una sola dimensión.

+ El*desglose* crea un subcubo al especificar un intervalo de valores en varias dimensiones.

+ La*obtención de detalles* va desde un resumen a los detalles.

+ La*exploración* pasa de los detalles a un mayor nivel de agregación.

+ La*acumulación* resume los datos en una dimensión.

+ La*dinamización* gira el cubo o la selección de datos.

Este tema proporciona más ejemplos de la sintaxis básica para las consultas en un cubo: 

+ [Cómo crear consultas MDX mediante R](../../advanced-analytics/r-services/how-to-create-mdx-queries-using-olapr.md)

## <a name="olapr-api"></a>olapR API

El paquete **olapR** admite dos métodos de creación de consultas MDX:

- **Utilizar el Generador MDX.** Utilizar las funciones de R en el paquete para generar una consulta MDX simple, eligiendo un cubo y los ejes de configuración y las segmentaciones de datos. Se trata de una manera fácil de crear una consulta MDX válida si no tiene acceso a las herramientas tradicionales de OLAP o no tiene un conocimiento profundo del lenguaje MDX.

    No todas las posibles consultas MDX pueden crearse mediante el uso de este método, dado que MDX puede ser complejo. Sin embargo, esta API admite la mayoría de las operaciones habituales y útiles, incluyendo segmento, dados, obtención de detalles, paquete acumulativo de actualizaciones y dinámica en las dimensiones de N.

+ **Copiar y pegar MDX correcto.** Crear manualmente y, a continuación, pegue en cualquier consulta MDX. Esta opción es el mejor si hay consultas MDX existentes que desea volver a, o si la consulta que desee crear es demasiado compleja para **olapR** a controlar. 

    Compile el MDX con cualquier utilidad de cliente, como SSMS o Excel y, a continuación, guarde la cadena que define la consulta MDX. Proporcione esta cadena MDX como un argumento a la *controlador de consultas SSAS* en el **olapR** paquete. La función envía la consulta al servidor de Analysis Services especificado y devuelve los resultados a R, suponiendo que tenga permisos para consultar el cubo por supuesto.

Para obtener ejemplos de cómo compilar un MDX consulta o ejecutan una consulta MDX existente, consulte [cómo crear consultas MDX mediante R](../../advanced-analytics/r/how-to-create-mdx-queries-using-olapr.md).

## <a name="known-issues"></a>Problemas conocidos

### <a name="tabular-models-not-supported"></a>No admitidos los modelos tabulares

+ Si se conecta a una instancia tabular de Analysis Services, el `explore` función devuelve el estado correcto con un valor devuelto de TRUE. Sin embargo, los objetos del modelo tabular no son un tipo compatible y no se puede explorar.

+ Los modelos tabulares se pueden consultar mediante DAX o MDX. Si diseña una consulta MDX válida en un modelo tabular mediante una herramienta externa y, a continuación, pegue la consulta en esta API, la consulta devuelve un resultado nulo y no notifica un error.

## <a name="resources"></a>Recursos

Si no está familiarizado con OLAP o con las consultas MDX, vea estos artículos de Wikipedia: [Cubo OLAP](https://en.wikipedia.org/wiki/OLAP_cube)
[Expresiones MDX](https://en.wikipedia.org/wiki/MultiDimensional_eXpressions)

### <a name="samples"></a>Ejemplos

Si quiere aprender más sobre los cubos, puede crear el cubo que se usa en estos ejemplos si sigue el tutorial de Analysis Services hasta lección 4: [Creación de un cubo OLAP](../../analysis-services/multidimensional-modeling-adventure-works-tutorial.md)

También puede descargar un cubo existente como copia de seguridad y restaurarla en una instancia de Analysis Services. Por ejemplo, puede descargar un cubo totalmente procesado de [Adventure Works Multidimensional Model SQL 2014](http://msftdbprodsamples.codeplex.com/downloads/get/882334)en formato zip y restaurarlo en la instancia SSAS. Para más información, vea [Realizar una copia de seguridad y restaurarla](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md)o [Cmdlet Restore-ASDatabase](../../analysis-services/powershell/restore-asdatabase-cmdlet.md).
