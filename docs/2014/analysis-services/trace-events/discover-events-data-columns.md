---
title: Columnas de datos de eventos de detección | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Discover Events event category
ms.assetid: 10ec598e-5b51-4767-b4f7-42e261d96a40
caps.latest.revision: 29
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3437445c242c2e6ab759119ceb644807eea0cfd1
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37265391"
---
# <a name="discover-events-data-columns"></a>Columnas de datos de eventos de detección
  La categoría Eventos de detección tiene las siguientes clases de eventos:  
  
-   Clase Discover Begin  
  
-   Clase Discover End  
  
 En las siguientes tablas se muestran las columnas de datos de cada una de estas clases de eventos.  
  
## <a name="discover-begin-classdata-columns"></a>Columnas de datos de la clase Discover Begin  
  
|||||  
|-|-|-|-|  
|**Nombre de la columna**|**Identificador de la columna**|**Tipo de columna**|**Descripción de la columna**|  
|EventClass|0|1|EventClass se usa para clasificar los eventos.|  
|EventSubclass|1|1|EventSubclass proporciona información adicional sobre cada clase de eventos. Los siguientes son un valor válido: pares de nombre:<br /><br /> 0: **DBSCHEMA_CATALOGS**<br />1: **DBSCHEMA_TABLES**<br />2: **DBSCHEMA_COLUMNS**<br />3: **DBSCHEMA_PROVIDER_TYPES**<br />4: **MDSCHEMA_CUBES**<br />5: **MDSCHEMA_DIMENSIONS**<br />6: **MDSCHEMA_HIERARCHIES**<br />7: **MDSCHEMA_LEVELS**<br />8: **MDSCHEMA_MEASURES**<br />9: **MDSCHEMA_PROPERTIES**<br />10: **MDSCHEMA_MEMBERS**<br />11: **MDSCHEMA_FUNCTIONS**<br />12: **MDSCHEMA_ACTIONS**<br />13: **MDSCHEMA_SETS**<br />14: **DISCOVER_INSTANCES**<br />15: **MDSCHEMA_KPIS**<br />16: **MDSCHEMA_MEASUREGROUPS**<br />17: **MDSCHEMA_COMMANDS**<br />18: **DMSCHEMA_MINING_SERVICES**<br />19: **DMSCHEMA_MINING_SERVICE_PARAMETERS**<br />20: **DMSCHEMA_MINING_FUNCTIONS**<br />21: **DMSCHEMA_MINING_MODEL_CONTENT**<br />22: **DMSCHEMA_MINING_MODEL_XML**<br />23: **DMSCHEMA_MINING_MODELS**<br />24: **DMSCHEMA_MINING_COLUMNS**<br />25: **DISCOVER_DATASOURCES**<br />26: **DISCOVER_PROPERTIES**<br />27: **DISCOVER_SCHEMA_ROWSETS**<br />28: **DISCOVER_ENUMERATORS**<br />29: **DISCOVER_KEYWORDS**<br />30: **DISCOVER_LITERALS**<br />31: **DISCOVER_XML_METADATA**<br />32: **DISCOVER_TRACES**<br />33: **DISCOVER_TRACE_DEFINITION_PROVIDERINFO**<br />34: **DISCOVER_TRACE_COLUMNS**<br />35: **DISCOVER_TRACE_EVENT_CATEGORIES**<br />36: **DMSCHEMA_MINING_STRUCTURES**<br />37: **DMSCHEMA_MINING_STRUCTURE_COLUMNS**<br />38: **DISCOVER_MASTER_KEY**<br />39: **MDSCHEMA_INPUT_DATASOURCES**<br />40: **DISCOVER_LOCATIONS**<br />41: **DISCOVER_PARTITION_DIMENSION_STAT**<br />42: **DISCOVER_PARTITION_STAT**<br />43: **DISCOVER_DIMENSION_STAT**<br />44: **MDSCHEMA_MEASUREGROUP_DIMENSIONS**<br />45: **DISCOVER_XEVENT_TRACE_DEFINITION**|  
|CurrentTime|2|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|StartTime|3|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|ConnectionID|25|1|Contiene el identificador único de conexión asociado al evento de detección.|  
|DatabaseName|28|8|Nombre de la base de datos en la que se ejecuta la instrucción del usuario.|  
|NTUserName|32|8|Contiene el nombre de usuario de Windows asociado al evento de detección. El nombre de usuario está en formato canónico. Por ejemplo, engineering.microsoft.com/software/user.|  
|NTDomainName|33|8|Contiene la cuenta de dominio de Windows asociada al evento de detección.|  
|ClientProcessID|36|1|Contiene el identificador del proceso de la aplicación cliente.|  
|ApplicationName|37|8|Nombre de la aplicación cliente que ha creado la conexión con el servidor. Esta columna se rellena con los valores que pasa la aplicación, en lugar de con el nombre que se muestra para el programa.|  
|SessionID|39|8|Contiene el identificador de sesión asociado al evento de detección.|  
|NTCanonicalUserName|40|8|Contiene el nombre de usuario de Windows asociado al evento de detección. El nombre de usuario está en formato canónico. Por ejemplo, engineering.microsoft.com/software/user.|  
|SPID|41|1|Contiene el identificador de proceso de servidor (SPID) que define unívocamente la sesión de usuario asociada al evento de detección. El SPID se corresponde directamente con el GUID de sesión utilizado por XMLA.|  
|TextData|42|9|Contiene los datos de texto asociados al evento.|  
|ServerName|43|8|Contiene el nombre de la instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en la que se ha producido el evento de detección.|  
|RequestProperties|45|9|Contiene las propiedades de la solicitud de XML for Analysis (XMLA) asociadas al evento de detección.|  
  
## <a name="discover-end-classdata-columns"></a>Columnas de datos de la clase Discover End  
  
|||||  
|-|-|-|-|  
|**Nombre de la columna**|**Identificador de la columna**|**Tipo de columna**|**Descripción de la columna**|  
|EventClass|0|1|Contiene la clase de evento, que se usa para clasificar eventos.|  
|EventSubclass|1|1|EventSubclass proporciona información adicional sobre cada clase de eventos. Los siguientes son un valor válido: pares de nombre:<br /><br /> 0: **DBSCHEMA_CATALOGS**<br />1: **DBSCHEMA_TABLES**<br />2: **DBSCHEMA_COLUMNS**<br />3: **DBSCHEMA_PROVIDER_TYPES**<br />4: **MDSCHEMA_CUBES**<br />5: **MDSCHEMA_DIMENSIONS**<br />6: **MDSCHEMA_HIERARCHIES**<br />7: **MDSCHEMA_LEVELS**<br />8: **MDSCHEMA_MEASURES**<br />9: **MDSCHEMA_PROPERTIES**<br />10: **MDSCHEMA_MEMBERS**<br />11: **MDSCHEMA_FUNCTIONS**<br />12: **MDSCHEMA_ACTIONS**<br />13: **MDSCHEMA_SETS**<br />14: **DISCOVER_INSTANCES**<br />15: **MDSCHEMA_KPIS**<br />16: **MDSCHEMA_MEASUREGROUPS**<br />17: **MDSCHEMA_COMMANDS**<br />18: **DMSCHEMA_MINING_SERVICES**<br />19: **DMSCHEMA_MINING_SERVICE_PARAMETERS**<br />20: **DMSCHEMA_MINING_FUNCTIONS**<br />21: **DMSCHEMA_MINING_MODEL_CONTENT**<br />22: **DMSCHEMA_MINING_MODEL_XML**<br />23: **DMSCHEMA_MINING_MODELS**<br />24: **DMSCHEMA_MINING_COLUMNS**<br />25: **DISCOVER_DATASOURCES**<br />26: **DISCOVER_PROPERTIES**<br />27: **DISCOVER_SCHEMA_ROWSETS**<br />28: **DISCOVER_ENUMERATORS**<br />29: **DISCOVER_KEYWORDS**<br />30: **DISCOVER_LITERALS**<br />31: **DISCOVER_XML_METADATA**<br />32: **DISCOVER_TRACES**<br />33: **DISCOVER_TRACE_DEFINITION_PROVIDERINFO**<br />34: **DISCOVER_TRACE_COLUMNS**<br />35: **DISCOVER_TRACE_EVENT_CATEGORIES**<br />36: **DMSCHEMA_MINING_STRUCTURES**<br />37: **DMSCHEMA_MINING_STRUCTURE_COLUMNS**<br />38: **DISCOVER_MASTER_KEY**<br />39: **MDSCHEMA_INPUT_DATASOURCES**<br />40: **DISCOVER_LOCATIONS**<br />41: **DISCOVER_PARTITION_DIMENSION_STAT**<br />42: **DISCOVER_PARTITION_STAT**<br />43: **DISCOVER_DIMENSION_STAT**<br />44: **MDSCHEMA_MEASUREGROUP_DIMENSIONS**<br />45: **DISCOVER_XEVENT_TRACE_DEFINITION**|  
|CurrentTime|2|5|Contiene la hora actual del evento de detección, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|StartTime|3|5|Contiene la hora (si está disponible) a la que se ha iniciado el evento final de detección. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|EndTime|4|5|Contiene la hora a la que finalizó el evento. Esta columna no se llena para las clases de eventos de inicio, como SQL:BatchStarting o SP:Starting. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|Duration|5|2|Contiene el tiempo aproximado (en milisegundos) usado por el evento de detección.|  
|CPUTime|6|2|Contiene la cantidad de tiempo de CPU (en milisegundos) usada por el evento.|  
|Severity|22|1|Contiene el nivel de gravedad de una excepción.|  
|Correcto|23|1|Contiene el éxito o el fracaso de un evento de detección. Los valores son:<br /><br /> 0 = Error<br /><br /> 1 = Correcto|  
|Error|24|1|Contiene el número de error de cualquier error asociado al evento de detección.|  
|ConnectionID|25|1|Contiene el identificador único de conexión asociado al evento de detección.|  
|DatabaseName|28|8|Contiene el nombre de la base de datos en la que se ha producido el evento de detección.|  
|NTUserName|32|8|Contiene el nombre de usuario de Windows asociado al evento de permiso de objeto.|  
|NTDomainName|33|8|Contiene la cuenta de dominio de Windows asociada al evento de detección.|  
|ClientProcessID|36|1|Contiene el identificador de proceso de la aplicación cliente que inició el evento.|  
|ApplicationName|37|8|Contiene el nombre de la aplicación cliente que ha creado la conexión con el servidor. Esta columna se rellena con los valores que pasa la aplicación, en lugar de con el nombre que se muestra para el programa.|  
|SessionID|39|8|Contiene el identificador de sesión asociado al evento de detección.|  
|NTCanonicalUserName|40|8|Contiene el nombre de usuario de Windows asociado al evento de permiso de objeto. El nombre de usuario está en formato canónico. Por ejemplo, engineering.microsoft.com/software/user.|  
|SPID|41|1|Contiene el identificador de proceso de servidor (SPID) que define unívocamente la sesión de usuario asociada al evento final de detección. El SPID se corresponde directamente con el GUID de sesión utilizado por XMLA.|  
|TextData|42|9|Contiene los datos de texto asociados al evento.|  
|ServerName|43|8|Contiene el nombre de la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en la que se ha producido el evento de detección.|  
|RequestProperties|45|9|Contiene las propiedades de la solicitud de XMLA.|  
  
## <a name="see-also"></a>Vea también  
 [Categoría de eventos eventos de detección](discover-events-event-category.md)  
  
  
