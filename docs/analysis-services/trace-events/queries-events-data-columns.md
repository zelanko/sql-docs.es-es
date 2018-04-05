---
title: Consulta las columnas de datos de eventos | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- Queries Events event category
ms.assetid: 28aa7df5-3e1f-4f4f-8a1c-8bbd29d5da13
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: f329c73f2fbfd0b99e45c2012fb90b90ec52f879
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="queries-events-data-columns"></a>Columnas de datos de Eventos de consultas
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]La categoría de eventos de eventos de consultas tiene las siguientes clases de evento:  
  
|**Identificador del evento**|**Nombre del evento**|**Descripción del evento**|  
|------------------|--------------------|---------------------------|  
|9|Query Begin|Inicio de la consulta.|  
|10|Query End|Final de la consulta.|  
  
 En las siguientes tablas se muestran las columnas de datos de cada una de estas clases de eventos.  
  
## <a name="query-begin-classdata-columns"></a>Columnas de datos de la clase Query Begin  
  
|**Nombre de la columna**|**Identificador de la columna**|**Tipo de columna**|**Descripción de la columna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|EventClass se usa para clasificar los eventos.|  
|EventSubclass|1|1|EventSubclass proporciona información adicional sobre cada clase de eventos.<br /><br /> 0: MDXQuery<br /><br /> 1: DMXQuery<br /><br /> 2: SQLQuery<br /><br /> 3: DAXQuery|  
|CurrentTime|2|5|Contiene la hora actual del evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|StartTime|3|5|Contiene la hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|ConnectionID|25|1|Contiene el identificador único de conexión asociado al evento de consulta.|  
|DatabaseName|28|8|Contiene el nombre de la base de datos en la que se está ejecutando la consulta.|  
|NTUserName|32|8|Contiene el nombre de usuario de Windows asociado al evento de consulta.|  
|NTDomainName|33|8|Contiene la cuenta de dominio de Windows asociada al evento de consulta.|  
|ClientProcessID|36|1|Contiene el identificador del proceso de la aplicación cliente.|  
|ApplicationName|37|8|Contiene el nombre de la aplicación cliente que ha creado la conexión con el servidor. Esta columna se rellena con los valores que pasa la aplicación, en lugar de con el nombre que se muestra para el programa.|  
|SessionID|39|8|Contiene el identificador único de sesión de la solicitud XMLA.|  
|NTCanonicalUserName|40|8|Contiene el nombre de usuario de Windows asociado al evento de consulta. El nombre de usuario está en formato canónico. Por ejemplo, engineering.microsoft.com/software/user.|  
|SPID|41|1|Contiene el identificador de proceso de servidor (SPID) que define unívocamente la sesión de usuario asociada al evento de consulta. El SPID se corresponde directamente con el GUID de sesión utilizado por XMLA.|  
|TextData|42|9|Contiene los datos de texto asociados al evento de consulta.|  
|ServerName|43|8|Contiene el nombre de la instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en la que se ha producido el evento de consulta.|  
|RequestParameters|44|9|Contiene los parámetros de las consultas con parámetros y los comandos asociados al evento de consulta.|  
|RequestProperties|45|9|Contiene las propiedades de las solicitudes de XMLA.|  
  
## <a name="query-end-classdata-columns"></a>Columnas de datos de la clase Query End  
  
|**Nombre de la columna**|**Identificador de la columna**|**Tipo de columna**|**Descripción de la columna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|EventClass se usa para clasificar los eventos.|  
|EventSubclass|1|1|EventSubclass proporciona información adicional sobre cada clase de eventos.<br /><br /> 0: MDXQuery<br /><br /> 1: DMXQuery<br /><br /> 2: SQLQuery<br /><br /> 3: DAXQuery|  
|CurrentTime|2|5|Contiene la hora actual del evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|StartTime|3|5|Contiene la hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|EndTime|4|5|Contiene la hora a la que finalizó el evento. Esta columna no se llena para las clases de eventos de inicio, como SQL:BatchStarting o SP:Starting. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|Duration|5|2|Contiene la cantidad de tiempo transcurrido (en milisegundos) que duró el evento.|  
|CPUTime|6|2|Contiene la cantidad de tiempo de CPU (en milisegundos) usada por el evento.|  
|Severity|22|1|Contiene el nivel de gravedad de una excepción asociada al evento de consulta. Los valores son:<br /><br /> 0 = Correcto.<br /><br /> 1 = De información<br /><br /> 2 = Advertencia<br /><br /> 3 = Error|  
|Success|23|1|Contiene el éxito o el fracaso de un evento de consulta. Los valores son:<br /><br /> 0 = Error<br /><br /> 1 = Correcto|  
|Error|24|1|Contiene el número de error de cualquier error asociado al evento de consulta.|  
|ConnectionID|25|1|Contiene el identificador único de conexión asociado al evento de consulta.|  
|DatabaseName|28|8|Contiene el nombre de la base de datos en la que se está ejecutando la consulta.|  
|NTUserName|32|8|Contiene el nombre de usuario de Windows asociado al evento de consulta.|  
|NTDomainName|33|8|Contiene la cuenta de dominio de Windows asociada al evento de consulta.|  
|ClientProcessID|36|1|Contiene el identificador del proceso de la aplicación cliente.|  
|ApplicationName|37|8|Contiene el nombre de la aplicación cliente que ha creado la conexión con el servidor. Esta columna se rellena con los valores que pasa la aplicación, en lugar de con el nombre que se muestra para el programa.|  
|SessionID|39|8|Contiene el identificador único de sesión de la solicitud XMLA.|  
|NTCanonicalUserName|40|8|Contiene el nombre de usuario de Windows asociado al evento de consulta. El nombre de usuario está en formato canónico. Por ejemplo, engineering.microsoft.com/software/user.|  
|SPID|41|1|Contiene el identificador de proceso de servidor (SPID) que define unívocamente la sesión de usuario asociada al evento de consulta. El SPID se corresponde directamente con el GUID de sesión utilizado por XMLA.|  
|TextData|42|9|Contiene los datos de texto asociados al evento de consulta.|  
|ServerName|43|8|Contiene el nombre de la instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en la que se ha producido el evento de consulta.|  
  
## <a name="see-also"></a>Vea también  
 [Categoría Eventos de consultas](../../analysis-services/trace-events/queries-events-category.md)  
  
  
