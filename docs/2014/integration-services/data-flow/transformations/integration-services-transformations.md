---
title: Transformaciones de Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- transformations [Integration Services], listed
- transformations [Integration Services], types
- transformations [Integration Services]
- data flow [Integration Services], transformations
- business intelligence transformations [Integration Services]
- join transformations
- split transformations [Integration Services]
- custom transformations [Integration Services]
- row transformations [Integration Services]
- rowset transformations [Integration Services]
ms.assetid: c70c4f6e-82dd-4948-b923-fd5193f67f7e
author: janinezhang
ms.author: janinez
ms.openlocfilehash: e90e459e5243d623ae0744ed2d7298cfd27eee5e
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84939479"
---
# <a name="integration-services-transformations"></a>Transformaciones de Integration Services
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] son los componentes en el flujo de datos de un paquete que agregan, combinan, distribuyen y modifican datos. Las transformaciones también pueden realizar operaciones de búsqueda y generar conjuntos de datos de ejemplo. Esta sección describe las transformaciones que incluye [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] y explica cómo funcionan.  
  
## <a name="business-intelligence-transformations"></a>Transformaciones de inteligencia empresarial  
 Las siguientes transformaciones realizan operaciones de inteligencia empresarial tales como limpiar datos, realizar minería de texto y ejecutar consultas de predicción de minería de datos.  
  
|Transformación|Descripción|  
|--------------------|-----------------|  
|[Transformación Dimensión de variación lenta](slowly-changing-dimension-transformation.md)|Transformación que configura la actualización de una dimensión de variación lenta.|  
|[Transformación Agrupación aproximada](fuzzy-grouping-transformation.md)|Transformación que normaliza los valores de los datos de una columna.|  
|[Transformación Búsqueda aproximada](lookup-transformation.md)|Transformación que busca valores en una tabla de referencia mediante una coincidencia aproximada.|  
|[Transformación Extracción de términos](term-extraction-transformation.md)|Transformación que extrae términos del texto.|  
|[Transformación Búsqueda de términos](term-lookup-transformation.md)|Transformación que busca términos en una tabla de referencia y cuenta los términos extraídos del texto.|  
|[Transformación Consulta de minería de datos](data-mining-query-transformation.md)|Transformación que ejecuta consultas de predicción de minería de datos.|  
|[Transformación Limpieza de DQS](dqs-cleansing-transformation.md)|Transformación que corrige los datos de un origen de datos conectado aplicando las reglas que se crearon para el origen de datos.|  
  
## <a name="row-transformations"></a>Transformaciones de fila  
 Las siguientes transformaciones actualizan los valores de columna y crean columnas nuevas. La transformación se aplica a cada fila en la entrada de transformación.  
  
|Transformación|Descripción|  
|--------------------|-----------------|  
|[Transformación Mapa de caracteres](character-map-transformation.md)|Transformación que aplica funciones de cadena a caracteres.|  
|[Transformación Copiar columna](copy-column-transformation.md)|Transformación que agrega copias de columnas de entrada a la salida de transformación.|  
|[Transformación Conversión de datos](data-conversion-transformation.md)|Transformación que convierte el tipo de datos de una columna en un tipo de datos diferente.|  
|[Transformación Columna derivada](derived-column-transformation.md)|Transformación que rellena las columnas con los resultados de las expresiones.|  
|[Transformación Exportar columna](export-column-transformation.md)|Transformación que inserta datos de un flujo de datos en un archivo.|  
|[Transformación Importar columna](import-column-transformation.md)|Transformación que lee los datos de un archivo y los agrega a un flujo de datos.|  
|[Componente de script](script-component.md)|Transformación que usa script para extraer, transformar o cargar datos.|  
|[Transformación Comando de OLE DB](ole-db-command-transformation.md)|Transformación que ejecuta comandos SQL para cada fila de un flujo de datos.|  
  
## <a name="rowset-transformations"></a>Transformaciones de conjunto de filas  
 Las siguientes transformaciones crean nuevos conjuntos de filas. El conjunto de filas puede incluir valores agregados y ordenados, conjuntos de filas de ejemplo y conjuntos de filas dinamizados y de anulación de dinamización.  
  
|Transformación|Descripción|  
|--------------------|-----------------|  
|[Transformación Agregado](aggregate-transformation.md)|Transformación que realiza agregaciones tales como AVERAGE, SUM y COUNT.|  
|[Transformación Ordenar](sort-transformation.md)|Transformación que ordena datos.|  
|[Transformación Muestreo de porcentaje](percentage-sampling-transformation.md)|Transformación que crea un conjunto de datos de ejemplo mediante un porcentaje para especificar el tamaño del ejemplo.|  
|[Transformación Muestreo de fila](row-sampling-transformation.md)|Transformación que crea un conjunto de datos de ejemplo especificando la cantidad de filas en la muestra.|  
|[Transformación dinámica](pivot-transformation.md)|Transformación que crea una versión menos normalizada de una tabla normalizada.|  
|[Transformación Anular dinamización](unpivot-transformation.md)|Transformación que crea una versión más normalizada de una tabla no normalizada.|  
  
## <a name="split-and-join-transformations"></a>Transformaciones de división y combinación  
 Las siguientes transformaciones distribuyen filas a diferentes salidas, crean copias de las entradas de transformación, combinan varias entradas en una salida y realizan operaciones de búsqueda.  
  
|Transformación|Descripción|  
|--------------------|-----------------|  
|[Transformación División condicional](conditional-split-transformation.md)|Transformación que enruta las filas de datos a diferentes salidas.|  
|[Transformación Multidifusión](multicast-transformation.md)|Transformación que distribuye conjuntos de datos a varias salidas.|  
|[Transformación Unión de todo](union-all-transformation.md)|Transformación que combina varios conjuntos de datos.|  
|[Transformación Mezclar](merge-transformation.md)|Transformación que combina dos conjuntos de datos ordenados.|  
|[Transformación Combinación de mezcla](merge-join-transformation.md)|Transformación que combina dos conjuntos de datos mediante una combinación FULL, LEFT o INNER.|  
|[Transformación Búsqueda](lookup-transformation.md)|Transformación que busca valores en una tabla de referencia con una coincidencia exacta.|  
|[Transformación de caché](cache-transform.md)|La transformación que escribe los datos procedentes de un origen de datos conectado del flujo de datos en un administrador de conexiones de caché que guarda los datos en un archivo caché. La transformación de búsqueda realiza búsquedas en los datos del archivo caché.|  
|[Transformación Distribuidor de datos equilibrado](balanced-data-distributor-transformation.md)|La transformación distribuye uniformemente los búferes de filas entrantes entre los resultados de subprocesos independientes para mejorar el rendimiento de los paquetes de SSIS que se ejecutan en servidores con varios núcleos y varios procesadores.|  
  
## <a name="auditing-transformations"></a>Auditar transformaciones  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] incluye las transformaciones siguientes para agregar filas de recuento e información.  
  
|Transformación|Descripción|  
|--------------------|-----------------|  
|[Transformación Auditar](audit-transformation.md)|Transformación que hace que la información sobre el entorno esté a disposición del flujo de datos en un paquete.|  
|[Transformación Recuento de filas](row-count-transformation.md)|Transformación que cuenta las filas a medida que se mueven por ella y almacena el recuento final en una variable.|  
  
## <a name="custom-transformations"></a>Transformaciones personalizadas  
 También puede escribir transformaciones personalizadas. Para más información, vea [Desarrollar un componente de transformación personalizado con salidas sincrónicas](../../extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md) y [Desarrollar un componente de transformación personalizado con salidas asincrónicas](../../extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-asynchronous-outputs.md).  
  
  
