---
title: Consultar los conjuntos de filas de esquema de minería de datos (Analysis Services-minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- schema rowsets [Analysis Services], data mining
- data mining [Analysis Services], queries
- mining model content
- data mining [Analysis Services], schema rowsets
- schema rowsets [Analysis Services], retrieving
- data mining [Analysis Services], troubleshooting
ms.assetid: 442d8c29-07c7-45de-9a15-d556059f68d7
author: minewiskan
ms.author: owend
ms.openlocfilehash: 8775ec4dbfb7d851d98e0a943d052589f45b1ade
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/08/2020
ms.locfileid: "84523071"
---
# <a name="querying-the-data-mining-schema-rowsets-analysis-services---data-mining"></a>Consultar los conjuntos de filas de esquema de minería de datos (Analysis Services - Minería de datos)
  En [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)],muchos de los conjuntos de filas de esquema de minería de datos de OLE DB existentes se han expuesto como un conjunto de tablas del sistema que puede consultar con facilidad utilizando las instrucciones de Extensiones de minería de datos (DMX). Creando consultas para el conjunto de filas de esquema de minería de datos, puede identificar los servicios que están disponibles, obtener actualizaciones sobre el estado de los modelos y estructuras, y obtener detalles sobre el contenido o los parámetros del modelo. Para obtener una descripción de los conjuntos de filas de esquema de minería de datos, vea [Data Mining Schema Rowsets](../../relational-databases/native-client-ole-db-rowsets/rowsets.md).  
  
> [!NOTE]  
>  También puede consultar los conjuntos de filas de esquema de minería de datos utilizando XMLA. Para más información sobre cómo hacer esto en SQL Server Management Studio, vea [Crear una consulta de minería de datos utilizando XMLA](create-a-data-mining-query-by-using-xmla.md).  
  
## <a name="list-of-data-mining-schema-rowsets"></a>Lista de conjuntos de filas de esquema de minería de datos  
 En la tabla siguiente se muestran los conjuntos de filas de esquema de minería de datos que pueden ser útiles para consultar y supervisar.  
  
|Nombre del conjunto de filas|Descripción|  
|-----------------|-----------------|  
|DMSCHEMA_MINING_MODELS|Muestra todos los modelos de minería de datos del contexto actual.<br /><br /> Incluye información tal como la fecha de creación, los parámetros utilizados para crear el modelo y el tamaño del conjunto de aprendizaje.|  
|DMSCHEMA_MINING_COLUMNS|Muestra todas las columnas utilizadas en modelos de minería de datos en el contexto actual.<br /><br /> La información incluye funciones de asignación a columna de origen de estructura de minería de datos, tipo de datos, precisión y funciones de predicción que se pueden utilizar con la columna.|  
|DMSCHEMA_MINING_STRUCTURES|Muestra toda la estructura de minería de datos del contexto actual.<br /><br /> La información incluye si se rellena la estructura, la última fecha en la que se procesó la estructura y la definición del conjunto de datos de exclusiones para la estructura, si existe.|  
|DMSCHEMA_MINING_STRUCTURE_COLUMNS|Muestra todas las columnas utilizadas en estructuras de minería en el contexto actual.<br /><br /> La información incluye el tipo de contenido y el tipo de datos, la nulabilidad y si la columna contiene los datos de tabla anidada.|  
|DMSCHEMA_MINING_SERVICES|Muestra la lista de servicios o algoritmos de minería que están disponibles en el servidor especificado.<br /><br /> La información incluye marcas de modelado compatibles, tipos de entrada y tipos de origen de datos compatibles.|  
|DMSCHEMA_MINING_SERVICE_PARAMETERS|Muestra todos los parámetros para servicios de minería que están disponibles en la instancia actual.<br /><br /> La información incluye el tipo de datos para cada parámetro, los valores predeterminados y los límites superiores e inferiores.|  
|DMSCHEMA_MODEL_CONTENT|Devuelve el contenido del modelo si se ha procesado el modelo.<br /><br /> Para obtener más información, vea [Contenido del modelo de minería de datos &#40;Analysis Services - Minería de datos&#41;](mining-model-content-analysis-services-data-mining.md).|  
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
  
## <a name="see-also"></a>Consulte también  
 [Conceptos de la solución de problemas (Analysis Services - Minería de datos)](https://msdn.microsoft.com/library/cc645881.aspx)  
  
  
