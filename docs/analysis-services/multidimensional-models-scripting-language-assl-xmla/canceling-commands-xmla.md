---
title: Cancelar comandos (XMLA) | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0894379d301cc38084c3ee5e8d48e181d9d91dd4
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="canceling-commands-xmla"></a>Cancelar comandos (XMLA)
  Dependiendo de los permisos administrativos del usuario que emite el comando, el [cancelar](../../analysis-services/xmla/xml-elements-commands/cancel-element-xmla.md) de comandos en XML para Analysis (XMLA) puede cancelar un comando en una sesión, una sesión, una conexión, un proceso de servidor o una sesión asociada o conexión.  
  
## <a name="canceling-commands"></a>Cancelar comandos  
 Un usuario puede cancelar el comando actualmente en ejecución en el contexto de la sesión explícita actual mediante el envío de un **cancelar** comando sin propiedades especificadas.  
  
> [!NOTE]  
>  Un usuario no puede cancelar un comando que se ejecuta en una sesión implícita.  
  
### <a name="canceling-batch-commands"></a>Cancelar comandos Batch  
 Si un usuario cancela una **lote** comando y, a continuación, todos los demás comandos que no se hayan ejecutado los **lote** se cancela el comando. Si el **lote** comando es transaccional, los comandos ejecutados con anterioridad la **cancelar** comando se revierten.  
  
## <a name="canceling-sessions"></a>Cancelar sesiones  
 Mediante la especificación de un identificador de sesión para una sesión explícita en la [SessionID](../../analysis-services/xmla/xml-elements-properties/sessionid-element-xmla.md) propiedad de la **cancelar** de comandos, un administrador de base de datos o el administrador del servidor puede cancelar una sesión, incluido el está ejecutando el comando. Un administrador de bases de datos solamente puede cancelar sesiones de las bases de datos en las que tiene permisos administrativos.  
  
 Un administrador de bases de datos puede recuperar las sesiones activas de una base de datos especificada mediante la recuperación del conjunto de filas de esquema DISCOVER_SESSIONS. Para recuperar el conjunto de filas de esquema DISCOVER_SESSIONS, el Administrador de base de datos utiliza el XMLA **Discover** método y especifica el identificador de base de datos adecuada para la restricción de session_current_database en la [Restricciones](../../analysis-services/xmla/xml-elements-properties/restrictions-element-xmla.md) propiedad de la **Discover** método.  
  
## <a name="canceling-connections"></a>Cancelar conexiones  
 Si especifica un identificador de conexión en el [ConnectionID](../../analysis-services/xmla/xml-elements-properties/connectionid-element-xmla.md) propiedad de la **cancelar** de comandos, un administrador del servidor puede cancelar todas las sesiones asociadas a una conexión determinada, todos los incluidos ejecutar comandos y cancelar la conexión.  
  
> [!NOTE]  
>  Si la instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no se puede ubicar y cancelar las sesiones asociadas a una conexión, como cuando el bombeo de datos abre varias sesiones mientras proporcionan conectividad HTTP, la instancia no puede cancelar la conexión. Si esto ocurriera durante la ejecución de un **cancelar** comando, se produce un error.  
  
 Un administrador del servidor puede recuperar las conexiones activas para un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instancia al recuperar el conjunto de filas de esquema DISCOVER_CONNECTIONS con XMLA **Discover** método.  
  
## <a name="canceling-server-processes"></a>Cancelar procesos de servidor  
 Mediante la especificación de un identificador de proceso de servidor (SPID) en el [SPID](../../analysis-services/xmla/xml-elements-properties/spid-element-xmla.md) propiedad de la **cancelar** de comandos, un administrador del servidor puede cancelar los comandos asociados a un SPID determinado.  
  
## <a name="canceling-associated-sessions-and-connections"></a>Cancelar sesiones y conexiones asociadas  
 Puede establecer la [CancelAssociated](../../analysis-services/xmla/xml-elements-properties/cancelassociated-element-xmla.md) propiedad en true para cancelar las conexiones, sesiones y comandos asociados a la conexión, sesión o SPID especificados en la **cancelar** comando.  
  
## <a name="see-also"></a>Vea también  
 [Método Discover &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-methods-discover.md)   
 [Desarrollar con XMLA en Analysis Services](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
