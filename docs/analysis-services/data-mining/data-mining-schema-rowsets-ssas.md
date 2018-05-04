---
title: Conjuntos de filas de esquema (SSAs) de minería de datos | Documentos de Microsoft
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: data-mining
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 497abfa736d0a7f97c34ea28cf9e7bcd6dbe93b6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="data-mining-schema-rowsets-ssas"></a>Conjuntos de filas de esquema de minería de datos (SSAs)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  En [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)],muchos de los conjuntos de filas de esquema de minería de datos de OLE DB existentes se han expuesto como un conjunto de tablas del sistema que puede consultar con facilidad utilizando las instrucciones de Extensiones de minería de datos (DMX). Creando consultas para el conjunto de filas de esquema de minería de datos, puede identificar los servicios que están disponibles, obtener actualizaciones sobre el estado de los modelos y estructuras, y obtener detalles sobre el contenido o los parámetros del modelo. Para obtener una descripción de los conjuntos de filas de esquema de minería de datos, vea [Data Mining Schema Rowsets](../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md).  
  
> [!NOTE]  
>  También puede consultar los conjuntos de filas de esquema de minería de datos utilizando XMLA. Para más información sobre cómo hacer esto en SQL Server Management Studio, vea [Crear una consulta de minería de datos utilizando XMLA](../../analysis-services/data-mining/create-a-data-mining-query-by-using-xmla.md).  
  
## <a name="list-of-data-mining-schema-rowsets"></a>Lista de conjuntos de filas de esquema de minería de datos  
 En la tabla siguiente se muestran los conjuntos de filas de esquema de minería de datos que pueden ser útiles para consultar y supervisar.  
  
|Nombre del conjunto de filas|Description|  
|-----------------|-----------------|  
|DMSCHEMA_MINING_MODELS|Muestra todos los modelos de minería de datos del contexto actual.<br /><br /> Incluye información tal como la fecha de creación, los parámetros utilizados para crear el modelo y el tamaño del conjunto de aprendizaje.|  
|DMSCHEMA_MINING_COLUMNS|Muestra todas las columnas utilizadas en modelos de minería de datos en el contexto actual.<br /><br /> La información incluye funciones de asignación a columna de origen de estructura de minería de datos, tipo de datos, precisión y funciones de predicción que se pueden utilizar con la columna.|  
|DMSCHEMA_MINING_STRUCTURES|Muestra toda la estructura de minería de datos del contexto actual.<br /><br /> La información incluye si se rellena la estructura, la última fecha en la que se procesó la estructura y la definición del conjunto de datos de exclusiones para la estructura, si existe.|  
|DMSCHEMA_MINING_STRUCTURE_COLUMNS|Muestra todas las columnas utilizadas en estructuras de minería en el contexto actual.<br /><br /> La información incluye el tipo de contenido y el tipo de datos, la nulabilidad y si la columna contiene los datos de tabla anidada.|  
|DMSCHEMA_MINING_SERVICES|Muestra la lista de servicios o algoritmos de minería que están disponibles en el servidor especificado.<br /><br /> La información incluye marcas de modelado compatibles, tipos de entrada y tipos de origen de datos compatibles.|  
|DMSCHEMA_MINING_SERVICE_PARAMETERS|Muestra todos los parámetros para servicios de minería que están disponibles en la instancia actual.<br /><br /> La información incluye el tipo de datos para cada parámetro, los valores predeterminados y los límites superiores e inferiores.|  
|DMSCHEMA_MODEL_CONTENT|Devuelve el contenido del modelo si se ha procesado el modelo.<br /><br /> Para más información, vea [Contenido del modelo de minería de datos &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md).|  
|DBSCHEMA_CATALOGS|Muestra todas las bases de datos (catálogos) de la instancia actual de Analysis Services.|  
|MDSCHEMA_INPUT_DATASOURCES|Muestra todos los orígenes de datos de la instancia actual de Analysis Services.|  
  
> [!NOTE]  
>  La lista de la tabla no es completa; muestra solo los conjuntos de filas que pueden tener más interés para solucionar problemas.  
  
## <a name="examples"></a>Ejemplos  
 En la sección siguiente se proporcionan algunos ejemplos de consultas para los conjuntos de filas de esquema de minería de datos.  
  
### <a name="example-1-list-data-mining-services"></a>Ejemplo 1: lista de servicios de minería de datos  
 La consulta siguiente devuelve una lista de servicios de minería que están disponibles en el servidor actual, es decir, los algoritmos que están habilitados. Las columnas proporcionadas para cada servicio de minería incluyen las marcas de modelado y tipos de contenido que pueden ser utilizados por cada algoritmo, el GUID para cada servicio y los límites de predicción que se puede haber agregado para cada servicio.  
  
```  
SELECT *  
FROM $system.DMSCHEMA_MINING_SERVICES  
```  
  
### <a name="example-2-list-mining-model-parameters"></a>Ejemplo 2: lista de parámetros de modelo de minería  
 En el ejemplo siguiente se devuelven los parámetros que se utilizaron para crear un modelo de minería concreto:  
  
```  
SELECT MINING_PARAMETERS   
FROM $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'TM Clustering'  
```  
  
### <a name="example-3-list-all-rowsets"></a>Ejemplo 3: lista de todos los conjuntos de filas  
 En el ejemplo siguiente se devuelve una lista completa de los conjuntos de filas que están disponibles en el servidor actual:  
  
```  
SELECT *   
FROM $system.DBSCHEMA_TABLES  
```  
  
  
