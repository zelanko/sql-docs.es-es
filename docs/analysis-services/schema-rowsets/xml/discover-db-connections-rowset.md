---
title: Conjunto de filas DISCOVER_DB_CONNECTIONS | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DISCOVER_DB_CONNECTIONS rowset
ms.assetid: 12a51a4e-5f3d-4449-9d94-7836fea1bc8b
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a592cffbf5d8fe19d37fc48989d9c2776df81a4e
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="discoverdbconnections-rowset"></a>DISCOVER_DB_CONNECTIONS, conjunto de filas
  Proporciona información sobre el uso de los recursos y la actividad en las conexiones abiertas actualmente desde el servidor a una base de datos.  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El conjunto de filas **DISCOVER_DB_CONNECTIONS** contiene las siguientes columnas.  
  
|Nombre de columna|Indicador de tipo|Longitud|Description|  
|-----------------|--------------------|------------|-----------------|  
|**CONNECTION_CATALOG_NAME**|**DBTYPE_WSTR**||Nombre de la base de datos conectada actualmente.|  
|**CONNECTION_ID**|**DBTYPE_I4**||Número único que identifica la conexión.|  
|**CONNECTION_IDLE_TIME_MS**|**DBTYPE_I8**||Tiempo de inactividad, en milisegundos, desde el inicio de la conexión.|  
|**CONNECTION_IN_USE**|**DBTYPE_I4**||Indica si la conexión está activa (1) o inactiva (0).|  
|**CONNECTION_LAST_COMMAND_END_TIME**|**DBTYPE_DBTIMESTAMP**||Fecha y hora UTC del servidor al finalizar la ejecución del último comando.|  
|**CONNECTION_LAST_COMMAND_START_TIME**|**DBTYPE_DBTIMESTAMP**||Fecha y hora UTC del servidor cuando se inició la ejecución del último comando.|  
|**CONNECTION_SERVER_NAME**|**DBTYPE_WSTR**||Nombre del servidor conectado actualmente.|  
|**CONNECTION_SPID**|**DBTYPE_I4**||Identificador de la sesión.|  
|**CONNECTION_START_TIME**|**DBTYPE_DBTIMESTAMP**||Fecha y hora UTC del servidor cuando se inició la conexión.|  
|**CONNECTION_USAGE_TIME_MS**|**DBTYPE_I8**||Tiempo activo de conexión, en milisegundos, desde el inicio de la conexión.|  
  
 Este conjunto de filas de esquema no está ordenado.  
  
> [!IMPORTANT]  
>  El conjunto de filas **DISCOVER_DB_CONNECTIONS** solamente mostrará información cuando el servicio se conecte a los orígenes de datos relacionales.  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El conjunto de filas **DISCOVER_DB_CONNECTIONS** puede tener restricciones en las columnas que se muestran en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|CONNECTION_ID|DBTYPE_I4|Opcional.|  
|CONNECTION_IN_USE|DBTYPE_I4|Opcional.|  
|CONNECTION_SERVER_NAME|DBTYPE_WSTR|Opcional.|  
|CONNECTION_CATALOG_NAME|DBTYPE_WSTR|Requerido.|  
|CONNECTION_SPID|DBTYPE_I4|Opcional.|  
  
## <a name="see-also"></a>Vea también  
 [XML para conjuntos de filas de esquema de análisis](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  

