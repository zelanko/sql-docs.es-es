---
title: Cancelar comandos (XMLA) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- connections [XML for Analysis]
- associated connections [XML for Analysis]
- XML for Analysis, canceling
- associated sessions [XML for Analysis]
- canceling connections
- canceling commands
- canceling sessions
- SPID
- XMLA, canceling
- server process IDs [XML for Analysis]
- sessions [XML for Analysis]
ms.assetid: b59f8197-c33d-4e65-9022-848ccba540f5
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 5129dd84cdd120b778fb55986374d27055b5904c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36105966"
---
# <a name="canceling-commands-xmla"></a>Cancelar comandos (XMLA)
  Dependiendo de los permisos administrativos del usuario que emite el comando, el [cancelar](../xmla/xml-elements-commands/cancel-element-xmla.md) de comandos en XML para Analysis (XMLA) puede cancelar un comando en una sesión, una sesión, una conexión, un proceso de servidor o una sesión asociada o conexión.  
  
## <a name="canceling-commands"></a>Cancelar comandos  
 Un usuario puede cancelar el comando actualmente en ejecución en el contexto de la sesión explícita actual mediante el envío de un comando `Cancel` sin propiedades especificadas.  
  
> [!NOTE]  
>  Un usuario no puede cancelar un comando que se ejecuta en una sesión implícita.  
  
### <a name="canceling-batch-commands"></a>Cancelar comandos Batch  
 Si un usuario cancela un comando `Batch`, se cancelan todos los comandos restantes del comando `Batch` que no se hayan ejecutado aún. Si el comando `Batch` es de tipo transaccional, se revierten los comandos ejecutados con anterioridad al comando `Cancel`.  
  
## <a name="canceling-sessions"></a>Cancelar sesiones  
 Mediante la especificación de un identificador de sesión para una sesión explícita en la [SessionID](../xmla/xml-elements-properties/id-element-xmla.md) propiedad de la `Cancel` de comandos, un administrador de base de datos o el administrador del servidor puede cancelar una sesión, incluido el comando actualmente en ejecución . Un administrador de bases de datos solamente puede cancelar sesiones de las bases de datos en las que tiene permisos administrativos.  
  
 Un administrador de bases de datos puede recuperar las sesiones activas de una base de datos especificada mediante la recuperación del conjunto de filas de esquema DISCOVER_SESSIONS. Para recuperar el conjunto de filas de esquema DISCOVER_SESSIONS, el Administrador de base de datos utiliza el XMLA `Discover` método y especifica el identificador de base de datos adecuada para la restricción de session_current_database en la [restricciones](../xmla/xml-elements-properties/restrictions-element-xmla.md) propiedad de la `Discover` método.  
  
## <a name="canceling-connections"></a>Cancelar conexiones  
 Si especifica un identificador de conexión en el [ConnectionID](../xmla/xml-elements-properties/connectionid-element-xmla.md) propiedad de la `Cancel` de comandos, un administrador del servidor puede cancelar todas las sesiones asociadas a una conexión determinada, incluidos todos los comandos de ejecución, y Cancelar la conexión.  
  
> [!NOTE]  
>  Si la instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no se puede ubicar y cancelar las sesiones asociadas a una conexión, como cuando el bombeo de datos abre varias sesiones mientras proporcionan conectividad HTTP, la instancia no puede cancelar la conexión. Si esto ocurriera durante la ejecución de un comando `Cancel`, se produce un error.  
  
 Un administrador de servidor puede recuperar las conexiones activas de una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] mediante la recuperación del conjunto de filas de esquema DISCOVER_CONNECTIONS con el método `Discover` de XMLA.  
  
## <a name="canceling-server-processes"></a>Cancelar procesos de servidor  
 Mediante la especificación de un identificador de proceso de servidor (SPID) en el [SPID](../xmla/xml-elements-properties/spid-element-xmla.md) propiedad de la `Cancel` de comandos, un administrador del servidor puede cancelar los comandos asociados a un SPID determinado.  
  
## <a name="canceling-associated-sessions-and-connections"></a>Cancelar sesiones y conexiones asociadas  
 Puede establecer la [CancelAssociated](../xmla/xml-elements-properties/cancelassociated-element-xmla.md) propiedad en true para cancelar las conexiones, sesiones y comandos asociados a la conexión, sesión o SPID especificados en la `Cancel` comando.  
  
## <a name="see-also"></a>Vea también  
 [Método Discover &#40;XMLA&#41;](../xmla/xml-elements-methods-discover.md)   
 [Desarrollo con XMLA en Analysis Services](developing-with-xmla-in-analysis-services.md)  
  
  