---
title: Conjunto de filas DISCOVER_DB_CONNECTIONS | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- DISCOVER_DB_CONNECTIONS rowset
ms.assetid: 12a51a4e-5f3d-4449-9d94-7836fea1bc8b
caps.latest.revision: 18
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f22c330fcc1deef1e86f4442ed8524235a3ba5c0
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37295555"
---
# <a name="discoverdbconnections-rowset"></a>DISCOVER_DB_CONNECTIONS, conjunto de filas
  Proporciona información sobre el uso de los recursos y la actividad en las conexiones abiertas actualmente desde el servidor a una base de datos.  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El `DISCOVER_DB_CONNECTIONS` conjunto de filas contiene las siguientes columnas.  
  
|Nombre de columna|Indicador de tipo|Longitud|Descripción|  
|-----------------|--------------------|------------|-----------------|  
|`CONNECTION_CATALOG_NAME`|`DBTYPE_WSTR`||Nombre de la base de datos conectada actualmente.|  
|`CONNECTION_ID`|`DBTYPE_I4`||Número único que identifica la conexión.|  
|`CONNECTION_IDLE_TIME_MS`|`DBTYPE_I8`||Tiempo de inactividad, en milisegundos, desde el inicio de la conexión.|  
|`CONNECTION_IN_USE`|`DBTYPE_I4`||Indica si la conexión está activa (1) o inactiva (0).|  
|`CONNECTION_LAST_COMMAND_END_TIME`|`DBTYPE_DBTIMESTAMP`||Fecha y hora UTC del servidor al finalizar la ejecución del último comando.|  
|`CONNECTION_LAST_COMMAND_START_TIME`|`DBTYPE_DBTIMESTAMP`||Fecha y hora UTC del servidor cuando se inició la ejecución del último comando.|  
|`CONNECTION_SERVER_NAME`|`DBTYPE_WSTR`||Nombre del servidor conectado actualmente.|  
|`CONNECTION_SPID`|`DBTYPE_I4`||Identificador de la sesión.|  
|`CONNECTION_START_TIME`|`DBTYPE_DBTIMESTAMP`||Fecha y hora UTC del servidor cuando se inició la conexión.|  
|`CONNECTION_USAGE_TIME_MS`|`DBTYPE_I8`||Tiempo activo de conexión, en milisegundos, desde el inicio de la conexión.|  
  
 Este conjunto de filas de esquema no está ordenado.  
  
> [!IMPORTANT]  
>  El conjunto de filas `DISCOVER_DB_CONNECTIONS` solamente mostrará información cuando el servicio se conecte a los orígenes de datos relacionales.  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El `DISCOVER_DB_CONNECTIONS` conjunto de filas puede tener restricciones en las columnas enumeradas en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|CONNECTION_ID|DBTYPE_I4|Opcional.|  
|CONNECTION_IN_USE|DBTYPE_I4|Opcional.|  
|CONNECTION_SERVER_NAME|DBTYPE_WSTR|Opcional.|  
|CONNECTION_CATALOG_NAME|DBTYPE_WSTR|Requerido.|  
|CONNECTION_SPID|DBTYPE_I4|Opcional.|  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de filas de esquema de XML for Analysis](xml-for-analysis-schema-rowsets.md)  
  
  
