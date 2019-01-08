---
title: Cancelar comandos (XMLA) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 313708ad1575c7b9922ac796791d0d623c51b54b
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/11/2018
ms.locfileid: "53207524"
---
# <a name="canceling-commands-xmla"></a>Cancelar comandos (XMLA)
  Dependiendo de los permisos administrativos del usuario que emite el comando, el [cancelar](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/cancel-element-xmla) de comandos en XML para Analysis (XMLA) puede cancelar un comando en una sesión, una sesión, una conexión, un proceso de servidor o en una sesión asociada o conexión.  
  
## <a name="canceling-commands"></a>Cancelar comandos  
 Un usuario puede cancelar el comando actualmente en ejecución en el contexto de la sesión explícita actual mediante el envío de un **cancelar** comando sin propiedades especificadas.  
  
> [!NOTE]  
>  Un usuario no puede cancelar un comando que se ejecuta en una sesión implícita.  
  
### <a name="canceling-batch-commands"></a>Cancelar comandos Batch  
 Si un usuario cancela una **Batch** comando y, a continuación, todos los demás comandos aún no se han ejecutado dentro de la **Batch** se puede cancelar el comando. Si el **Batch** comando fuera transaccional, los comandos ejecutados con anterioridad el **cancelar** comando se revierten.  
  
## <a name="canceling-sessions"></a>Cancelar sesiones  
 Especificando un identificador de sesión para una sesión explícita en el [SessionID](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/id-element-xmla) propiedad de la **cancelar** de comandos, un administrador de base de datos o el administrador del servidor puede cancelar una sesión, incluido el ejecutando comando. Un administrador de bases de datos solamente puede cancelar sesiones de las bases de datos en las que tiene permisos administrativos.  
  
 Un administrador de bases de datos puede recuperar las sesiones activas de una base de datos especificada mediante la recuperación del conjunto de filas de esquema DISCOVER_SESSIONS. Para recuperar el conjunto de filas de esquema DISCOVER_SESSIONS, el Administrador de base de datos utiliza XMLA **Discover** método y especifica el identificador de la base de datos adecuada para la restricción de session_current_database en la [Restricciones](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/restrictions-element-xmla) propiedad de la **Discover** método.  
  
## <a name="canceling-connections"></a>Cancelar conexiones  
 Especificando un identificador de conexión en el [ConnectionID](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/connectionid-element-xmla) propiedad de la **cancelar** de comandos, un administrador del servidor puede cancelar todas las sesiones asociadas con una conexión determinada, todos los incluidos ejecución de comandos y cancelar la conexión.  
  
> [!NOTE]
>  Si la instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no se puede ubicar y cancelar las sesiones asociadas a una conexión, como cuando el bombeo de datos abre varias sesiones al tiempo que proporciona conectividad HTTP, la instancia no puede cancelar la conexión. Si esto ocurriera durante la ejecución de un **cancelar** comando, se produce un error.  
  
 Un administrador del servidor puede recuperar las conexiones activas para un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instancia recuperando el conjunto de filas de esquema DISCOVER_CONNECTIONS con XMLA **Discover** método.  
  
## <a name="canceling-server-processes"></a>Cancelar procesos de servidor  
 Especificando un identificador de proceso de servidor (SPID) en el [SPID](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/id-element-xmla) propiedad de la **cancelar** de comandos, un administrador del servidor puede cancelar los comandos asociados a un SPID determinado.  
  
## <a name="canceling-associated-sessions-and-connections"></a>Cancelar sesiones y conexiones asociadas  
 Puede establecer el [CancelAssociated](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/cancelassociated-element-xmla) propiedad en true para cancelar las conexiones, sesiones y comandos asociados a la conexión, sesión o SPID especificados en el **cancelar** comando.  
  
## <a name="see-also"></a>Vea también  
 [Método Discover &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-discover)   
 [Desarrollo con XMLA en Analysis Services](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
