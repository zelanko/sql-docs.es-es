---
title: Supervisar los seguimientos (XMLA) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
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
- XML for Analysis, traces
- XMLA, traces
- monitoring traces [XMLA]
- traces [Analysis Services]
ms.assetid: cdbfb984-18bd-4c4e-8fb7-d64ce298ed35
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d63e2b7e07c01d0f937618cfc521921e9d16dc43
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="monitoring-traces-xmla"></a>Supervisar los seguimientos (XMLA)
  Puede usar el [suscribir](../../analysis-services/xmla/xml-elements-commands/subscribe-element-xmla.md) comando XML for Analysis (XMLA) para supervisar un seguimiento existente definido en una instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. El **suscribir** comando devuelve los resultados de un seguimiento como un conjunto de filas.  
  
## <a name="specifying-a-trace"></a>Especificar un seguimiento  
 El [objeto](../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md) propiedad de la **suscribir** comando debe contener una referencia de objeto a una [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instancia o un seguimiento en un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instancia. Si el **objeto** no se especifica la propiedad o un identificador de seguimiento no se especifica en el **objeto** propiedad, el **suscribir** comando supervisa el seguimiento de sesión predeterminada para la sesión explícita especificada en el encabezado SOAP para el comando.  
  
## <a name="returning-results"></a>Devolver resultados  
 El **suscribir** comando devuelve un conjunto de filas que contiene los eventos de seguimiento capturados por el seguimiento especificado. El **suscribir** comando devuelve los resultados de seguimiento hasta que se cancela el comando por el [cancelar](../../analysis-services/xmla/xml-elements-commands/cancel-element-xmla.md) comando.  
  
 El conjunto de filas contiene las columnas que se muestran en la tabla siguiente.  
  
|Columna|Data type|Description|  
|------------|---------------|-----------------|  
|EventClass|Integer|Clase del evento que recibe el seguimiento.|  
|EventSubclass|Entero largo|Subclase del evento que recibe el seguimiento.|  
|CurrentTime|Fecha y hora|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|StartTime|Fecha y hora|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|EndTime|Fecha y hora|Hora a la que finalizó el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".<br /><br /> Esta columna no se rellena para las clases de eventos que describen el inicio de un proceso o acción.|  
|Duración|Entero largo|Tiempo total transcurrido (en milisegundos) para el evento.|  
|CPUTime|Entero largo|Tiempo de procesador transcurrido (en milisegundos) para el evento.|  
|JobID|Entero largo|Identificador de trabajo para el proceso.|  
|SessionID|String|Identificador de la sesión para la que se produjo el evento.|  
|SessionType|String|Tipo de sesión para la que se produjo el evento.|  
|ProgressTotal|Entero largo|Número o cantidad total de progreso que notifica el evento.|  
|IntegerData|Entero largo|Datos enteros asociados al evento. El contenido de esta columna depende de la clase y subclase de evento.|  
|ObjectID|String|Identificador del objeto para el que se produjo el evento.|  
|ObjectType|String|Tipo del objeto especificado en ObjectName.|  
|ObjectName|String|Nombre del objeto para el que se produjo el evento.|  
|ObjectPath|String|Ruta de acceso jerárquica del objeto para el que se produjo el evento. La ruta de acceso se representa como una cadena delimitada por comas de identificadores de objeto para los elementos primarios del objeto especificado en ObjectName.|  
|ObjectReference|String|Representación XML de la referencia de objeto para el objeto especificado en ObjectName.|  
|NestLevel|Integer|Nivel de la transacción para la que se produjo el evento.|  
|NumSegments|Entero largo|Número de segmentos de datos afectados por el comando para el que se produjo el evento o a los que éste tuvo acceso.|  
|Severity|Integer|Nivel de gravedad de una excepción del evento La columna puede contener uno de los siguientes valores:<br /><br /> <br /><br /> 0: correcto<br /><br /> <br /><br /> 1: información<br /><br /> <br /><br /> 2: advertencia<br /><br /> <br /><br /> 3: error|  
|Success|Boolean|Indica si un comando se ha ejecutado correctamente o no.|  
|Error|Entero largo|Número de error del evento, si procede.|  
|ConnectionID|String|Identificador de la conexión para la que se produjo el evento.|  
|DatabaseName|String|Nombre de la base de datos para la que se produjo el evento.|  
|NTUserName|String|Nombre de usuario de Windows del usuario asociado al evento.|  
|NTDomainName|String|Dominio de Windows del usuario asociado al evento.|  
|ClientHostName|String|Nombre del equipo en el que se está ejecutando la aplicación cliente. Esta columna se rellena con los valores que pasa la aplicación cliente.|  
|ClientProcessID|Entero largo|El identificador de proceso de la aplicación cliente.|  
|ApplicationName|String|Nombre de la aplicación cliente que ha creado la conexión a la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Esta columna se rellena con los valores que pasa la aplicación cliente, en lugar de con el nombre mostrado del programa.|  
|NTCanonicalUserName|String|Nombre de usuario de Windows en forma canónica del usuario asociado al evento.|  
|SPID|String|Id. de proceso de servidor (SPID) de la sesión para la que se produjo el evento. El valor de esta columna se corresponde directamente con el id. de sesión especificado en el encabezado SOAP del mensaje XMLA para el que se produjo el evento.|  
|TextData|String|Los datos de texto asociados al evento. El contenido de esta columna depende de la clase y subclase de evento.|  
|ServerName|String|Nombre de la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para la que se produjo el evento.|  
|RequestParameters|String|Parámetros del comando XMLA o la consulta con parámetros para los que se produjo el evento.|  
|RequestProperties|String|Propiedades del método XMLA para el que se produjo el evento.|  
  
## <a name="see-also"></a>Vea también  
 [Desarrollar con XMLA en Analysis Services](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
