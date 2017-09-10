---
title: Uso de datos de cubos OLAP en R | Microsoft Docs
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- R
ms.assetid: 8093599c-8307-4237-983b-0908d0f8ab77
caps.latest.revision: 12
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 21010e4ad5633aced0c59c9016fbfbab8324c6fe
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="using-data-from-olap-cubes-in-r"></a>Uso de datos de cubos OLAP en R

El paquete **olapR** es un nuevo paquete de R que se proporciona en Microsoft R Server y SQL Server R Services y que permite ejecutar consultas MDX y usar los datos de cubos OLAP en la solución de R.

Con este paquete, no necesita crear servidores vinculados ni limpiar conjuntos de filas planas; se pueden usar datos OLAP directamente en R,

## <a name="overview"></a>Información general

Un cubo OLAP es una base de datos multidimensional que contiene agregaciones precalculadas de *medidas*que normalmente capturan métricas empresariales importantes, como importes de ventas, recuentos de ventas u otros valores numéricos. Los cubos OLAP se usan mucho para capturar y almacenar datos empresariales críticos a lo largo del tiempo. Hay una serie de herramientas, paneles y visualizaciones que usan datos OLAP para el análisis empresarial. Para más información, vea [Procesamiento analítico en línea](https://en.wikipedia.org/wiki/Online_analytical_processing)

El paquete **olapR** admite dos métodos de creación de consultas MDX: 

- Puede generar una consulta MDX sencilla mediante una API de estilo R para elegir un cubo, ejes y segmentaciones de datos. Con estas funciones puede crear consultas MDX válidas aunque no tenga acceso a herramientas tradicionales de OLAP o no tenga un conocimiento profundo del lenguaje MDX.

  Tenga en cuenta que no se pueden crear todas las posibles consultas MDX mediante este método en el paquete **olapR** , ya que MDX puede ser muy complejo. Pero admite las operaciones más habituales y útiles, como segmentar, desglosar, obtener detalles, acumular y dinamizar en N dimensiones.

+ Puede crear manualmente y luego pegar en cualquier consulta MDX. Esta opción es útil si tiene consultas MDX existentes que quiere volver a usar o si la consulta que quiere compilar es demasiado compleja para que **olapR** la controle. 

  Con este enfoque, la consulta MDX se compila con cualquier utilidad de cliente, como SSMS o Excel, y luego se usa como un argumento de cadena para el *controlador de consultas SSAS* proporcionado por este paquete. La función **olapR** enviará la consulta al servidor de Analysis Services especificado y volverá a pasar los resultados a R.

Para ver ejemplos de cómo compilar una consulta MDX o ejecutar una consulta MDX existente, vea [Cómo crear consultas MDX con R](../../advanced-analytics/r-services/how-to-create-mdx-queries-using-olapr.md).


## <a name="mdx-basics"></a>Conceptos básicos de MDX

Los datos de un cubo se pueden recuperar mediante el lenguaje de consulta MDX (expresión multidimensional). Dado que los datos de un cubo OLAP (o base de datos de Analysis Services) son multidimensionales en lugar de tabulares, MDX admite una sintaxis compleja y una serie de operaciones de filtrado y segmentación de datos:

+ La*segmentación* toma un subconjunto del cubo al seleccionar un valor para una dimensión, lo que da lugar a un cubo que es una dimensión más pequeño. 

+ El*desglose* crea un subcubo al especificar un intervalo de valores en varias dimensiones.

+ La*obtención de detalles* va desde un resumen a los detalles.

+ La*exploración* pasa de los detalles a un mayor nivel de agregación.

+ La*acumulación* resume los datos en una dimensión.

+ La*dinamización* gira el cubo o la selección de datos.

Este tema proporciona más ejemplos en los que se muestra la sintaxis básica para consultar a un cubo.
[Cómo crear consultas MDX con R](../../advanced-analytics/r-services/how-to-create-mdx-queries-using-olapr.md)


## <a name="known-issues"></a>Problemas conocidos

### <a name="tabular-models-not-supported-currently"></a>De momento no se admiten modelos tabulares

Puede conectarse a una instancia tabular de Analysis Services y la función `explore` informará de la corrección del proceso con un valor devuelto de TRUE, pero los objetos de modelo tabular no son un tipo compatible y no se pueden explorar. 

Los modelos tabulares admiten consultas MDX, pero una consulta MDX válida en un modelo tabular devolverá un resultado NULL y no notificará un error.

## <a name="resources"></a>Recursos

Si no está familiarizado con OLAP o con las consultas MDX, vea estos artículos de Wikipedia: [Cubo OLAP](https://en.wikipedia.org/wiki/OLAP_cube)
[Expresiones MDX](https://en.wikipedia.org/wiki/MultiDimensional_eXpressions)

### <a name="samples"></a>Ejemplos

Si quiere aprender más sobre los cubos, puede crear el cubo que se usa en estos ejemplos si sigue el tutorial de Analysis Services hasta lección 4: [Creación de un cubo OLAP](https://msdn.microsoft.com/library/ms170208.aspx)

También puede descargar un cubo existente como copia de seguridad y restaurarla en una instancia de Analysis Services. Por ejemplo, puede descargar un cubo totalmente procesado de [Adventure Works Multidimensional Model SQL 2014](http://msftdbprodsamples.codeplex.com/downloads/get/882334)en formato zip y restaurarlo en la instancia SSAS. Para más información, vea [Realizar una copia de seguridad y restaurarla](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md)o [Cmdlet Restore-ASDatabase](../../analysis-services/powershell/restore-asdatabase-cmdlet.md).

## <a name="see-also"></a>Vea también
[Cómo crear consultas MDX con R](../../advanced-analytics/r-services/how-to-create-mdx-queries-using-olapr.md)

[Diseñador de consultas MDX de Analysis Services](http://msdn.microsoft.com/library/7e288eee-2d37-485e-a6a0-dbba5e041e26)



