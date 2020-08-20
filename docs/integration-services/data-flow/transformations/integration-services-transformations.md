---
description: Transformaciones de Integration Services
title: Transformaciones de Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
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
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 1952a15280f2e1779ddc0c53828dd0801acb3827
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88457272"
---
# <a name="integration-services-transformations"></a>Transformaciones de Integration Services

[!INCLUDE[sqlserver-ssis](../../../includes/applies-to-version/sqlserver-ssis.md)]


  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] son los componentes en el flujo de datos de un paquete que agregan, combinan, distribuyen y modifican datos. Las transformaciones también pueden realizar operaciones de búsqueda y generar conjuntos de datos de ejemplo. Esta sección describe las transformaciones que incluye [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] y explica cómo funcionan.  
  
## <a name="business-intelligence-transformations"></a>Transformaciones de inteligencia empresarial  
 Las siguientes transformaciones realizan operaciones de inteligencia empresarial tales como limpiar datos, realizar minería de texto y ejecutar consultas de predicción de minería de datos.  
  
|Transformación|Descripción|  
|--------------------|-----------------|  
|[Transformación Dimensión de variación lenta](../../../integration-services/data-flow/transformations/slowly-changing-dimension-transformation.md)|Transformación que configura la actualización de una dimensión de variación lenta.|  
|[Transformación Agrupación aproximada](../../../integration-services/data-flow/transformations/fuzzy-grouping-transformation.md)|Transformación que normaliza los valores de los datos de una columna.|  
|[Transformación Búsqueda aproximada](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation.md)|Transformación que busca valores en una tabla de referencia mediante una coincidencia aproximada.|  
|[Transformación Extracción de términos](../../../integration-services/data-flow/transformations/term-extraction-transformation.md)|Transformación que extrae términos del texto.|  
|[Transformación Búsqueda de términos](../../../integration-services/data-flow/transformations/term-lookup-transformation.md)|Transformación que busca términos en una tabla de referencia y cuenta los términos extraídos del texto.|  
|[Transformación Consulta de minería de datos](../../../integration-services/data-flow/transformations/data-mining-query-transformation.md)|Transformación que ejecuta consultas de predicción de minería de datos.|  
|[Transformación Limpieza de DQS](../../../integration-services/data-flow/transformations/dqs-cleansing-transformation.md)|Transformación que corrige los datos de un origen de datos conectado aplicando las reglas que se crearon para el origen de datos.|  
  
## <a name="row-transformations"></a>Transformaciones de fila  
 Las siguientes transformaciones actualizan los valores de columna y crean columnas nuevas. La transformación se aplica a cada fila en la entrada de transformación.  
  
|Transformación|Descripción|  
|--------------------|-----------------|  
|[Transformación Mapa de caracteres](../../../integration-services/data-flow/transformations/character-map-transformation.md)|Transformación que aplica funciones de cadena a caracteres.|  
|[Transformación Copiar columna](../../../integration-services/data-flow/transformations/copy-column-transformation.md)|Transformación que agrega copias de columnas de entrada a la salida de transformación.|  
|[Transformación Conversión de datos](../../../integration-services/data-flow/transformations/data-conversion-transformation.md)|Transformación que convierte el tipo de datos de una columna en un tipo de datos diferente.|  
|[Transformación Columna derivada](../../../integration-services/data-flow/transformations/derived-column-transformation.md)|Transformación que rellena las columnas con los resultados de las expresiones.|  
|[Transformación Exportar columna](../../../integration-services/data-flow/transformations/export-column-transformation.md)|Transformación que inserta datos de un flujo de datos en un archivo.|  
|[Transformación Importar columna](../../../integration-services/data-flow/transformations/import-column-transformation.md)|Transformación que lee los datos de un archivo y los agrega a un flujo de datos.|  
|[Componente de script](../../../integration-services/data-flow/transformations/script-component.md)|Transformación que usa script para extraer, transformar o cargar datos.|  
|[Transformación Comando de OLE DB](../../../integration-services/data-flow/transformations/ole-db-command-transformation.md)|Transformación que ejecuta comandos SQL para cada fila de un flujo de datos.|  
  
## <a name="rowset-transformations"></a>Transformaciones de conjunto de filas  
 Las siguientes transformaciones crean nuevos conjuntos de filas. El conjunto de filas puede incluir valores agregados y ordenados, conjuntos de filas de ejemplo y conjuntos de filas dinamizados y de anulación de dinamización.  
  
|Transformación|Descripción|  
|--------------------|-----------------|  
|[Transformación Agregado](../../../integration-services/data-flow/transformations/aggregate-transformation.md)|Transformación que realiza agregaciones tales como AVERAGE, SUM y COUNT.|  
|[Transformación Ordenar](../../../integration-services/data-flow/transformations/sort-transformation.md)|Transformación que ordena datos.|  
|[Transformación Muestreo de porcentaje](../../../integration-services/data-flow/transformations/percentage-sampling-transformation.md)|Transformación que crea un conjunto de datos de ejemplo mediante un porcentaje para especificar el tamaño del ejemplo.|  
|[Transformación Muestreo de fila](../../../integration-services/data-flow/transformations/row-sampling-transformation.md)|Transformación que crea un conjunto de datos de ejemplo especificando la cantidad de filas en la muestra.|  
|[Transformación dinámica](../../../integration-services/data-flow/transformations/pivot-transformation.md)|Transformación que crea una versión menos normalizada de una tabla normalizada.|  
|[Transformación Anular dinamización](../../../integration-services/data-flow/transformations/unpivot-transformation.md)|Transformación que crea una versión más normalizada de una tabla no normalizada.|  
  
## <a name="split-and-join-transformations"></a>Transformaciones de división y combinación  
 Las siguientes transformaciones distribuyen filas a diferentes salidas, crean copias de las entradas de transformación, combinan varias entradas en una salida y realizan operaciones de búsqueda.  
  
|Transformación|Descripción|  
|--------------------|-----------------|  
|[Transformación División condicional](../../../integration-services/data-flow/transformations/conditional-split-transformation.md)|Transformación que enruta las filas de datos a diferentes salidas.|  
|[Transformación Multidifusión](../../../integration-services/data-flow/transformations/multicast-transformation.md)|Transformación que distribuye conjuntos de datos a varias salidas.|  
|[Transformación Unión de todo](../../../integration-services/data-flow/transformations/union-all-transformation.md)|Transformación que combina varios conjuntos de datos.|  
|[Transformación Mezclar](../../../integration-services/data-flow/transformations/merge-transformation.md)|Transformación que combina dos conjuntos de datos ordenados.|  
|[Transformación Combinación de mezcla](../../../integration-services/data-flow/transformations/merge-join-transformation.md)|Transformación que combina dos conjuntos de datos mediante una combinación FULL, LEFT o INNER.|  
|[Transformación Búsqueda](../../../integration-services/data-flow/transformations/lookup-transformation.md)|Transformación que busca valores en una tabla de referencia con una coincidencia exacta.|  
|[Transformación de caché](../../../integration-services/data-flow/transformations/cache-transform.md)|La transformación que escribe los datos procedentes de un origen de datos conectado del flujo de datos en un administrador de conexiones de caché que guarda los datos en un archivo caché. La transformación de búsqueda realiza búsquedas en los datos del archivo caché.|  
|[Transformación Distribuidor de datos equilibrado](../../../integration-services/data-flow/transformations/balanced-data-distributor-transformation.md)|La transformación distribuye uniformemente los búferes de filas entrantes entre los resultados de subprocesos independientes para mejorar el rendimiento de los paquetes de SSIS que se ejecutan en servidores con varios núcleos y varios procesadores.|  
  
## <a name="auditing-transformations"></a>Auditar transformaciones  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] incluye las transformaciones siguientes para agregar filas de recuento e información.  
  
|Transformación|Descripción|  
|--------------------|-----------------|  
|[Transformación Auditar](../../../integration-services/data-flow/transformations/audit-transformation.md)|Transformación que hace que la información sobre el entorno esté a disposición del flujo de datos en un paquete.|  
|[Transformación Recuento de filas](../../../integration-services/data-flow/transformations/row-count-transformation.md)|Transformación que cuenta las filas a medida que se mueven por ella y almacena el recuento final en una variable.|  
  
## <a name="custom-transformations"></a>Transformaciones personalizadas  
 También puede escribir transformaciones personalizadas. Para más información, vea [Desarrollar un componente de transformación personalizado con salidas sincrónicas](../../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md) y [Desarrollar un componente de transformación personalizado con salidas asincrónicas](../../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-asynchronous-outputs.md).  
  
  
