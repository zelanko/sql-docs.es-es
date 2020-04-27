---
title: Cancelar comandos (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 80bddac8f800c1b9394c1ed605007ab0f2137b88
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62727469"
---
# <a name="canceling-commands-xmla"></a>Cancelar comandos (XMLA)
  En función de los permisos administrativos del usuario que emite el comando, el comando [Cancelar](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/cancel-element-xmla) en XML for Analysis (XMLA) puede cancelar un comando en una sesión, una sesión, una conexión, un proceso de servidor o una sesión o conexión asociada.  
  
## <a name="canceling-commands"></a>Cancelar comandos  
 Un usuario puede cancelar el comando actualmente en ejecución en el contexto de la sesión explícita actual mediante el envío de un comando `Cancel` sin propiedades especificadas.  
  
> [!NOTE]  
>  Un usuario no puede cancelar un comando que se ejecuta en una sesión implícita.  
  
### <a name="canceling-batch-commands"></a>Cancelar comandos Batch  
 Si un usuario cancela un comando `Batch`, se cancelan todos los comandos restantes del comando `Batch` que no se hayan ejecutado aún. Si el comando `Batch` es de tipo transaccional, se revierten los comandos ejecutados con anterioridad al comando `Cancel`.  
  
## <a name="canceling-sessions"></a>Cancelar sesiones  
 Al especificar un identificador de sesión para una sesión explícita en la propiedad [SessionID](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/id-element-xmla) del `Cancel` comando, un administrador de base de datos o un administrador del servidor puede cancelar una sesión, incluido el comando que se está ejecutando actualmente. Un administrador de bases de datos solamente puede cancelar sesiones de las bases de datos en las que tiene permisos administrativos.  
  
 Un administrador de bases de datos puede recuperar las sesiones activas de una base de datos especificada mediante la recuperación del conjunto de filas de esquema DISCOVER_SESSIONS. Para recuperar el conjunto de filas de esquema DISCOVER_SESSIONS, el administrador de `Discover` bases de datos utiliza el método XMLA y especifica el identificador de base de datos adecuado para la columna `Discover` de restricción SESSION_CURRENT_DATABASE en la propiedad [restrictions](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/restrictions-element-xmla) del método.  
  
## <a name="canceling-connections"></a>Cancelar conexiones  
 Al especificar un identificador de conexión en la propiedad [ConnectionID](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/connectionid-element-xmla) del `Cancel` comando, un administrador del servidor puede cancelar todas las sesiones asociadas a una conexión determinada, incluidos todos los comandos en ejecución, y cancelar la conexión.  
  
> [!NOTE]  
>  Si la instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no puede localizar y cancelar las sesiones asociadas a una conexión, por ejemplo, cuando el bombeo de datos abre varias sesiones mientras proporciona conectividad http, la instancia no puede cancelar la conexión. Si esto ocurriera durante la ejecución de un comando `Cancel`, se produce un error.  
  
 Un administrador de servidor puede recuperar las conexiones activas de una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] mediante la recuperación del conjunto de filas de esquema DISCOVER_CONNECTIONS con el método `Discover` de XMLA.  
  
## <a name="canceling-server-processes"></a>Cancelar procesos de servidor  
 Al especificar un identificador de proceso de servidor (SPID) en la propiedad [SPID](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/id-element-xmla) del `Cancel` comando, un administrador del servidor puede cancelar los comandos asociados a un SPID determinado.  
  
## <a name="canceling-associated-sessions-and-connections"></a>Cancelar sesiones y conexiones asociadas  
 Puede establecer la propiedad [CancelAssociated](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/cancelassociated-element-xmla) en true para cancelar las conexiones, las sesiones y los comandos asociados a la conexión, la sesión o el SPID especificado en `Cancel` el comando.  
  
## <a name="see-also"></a>Consulte también  
 [Método Discover &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-discover)   
 [Desarrollar con XMLA en Analysis Services](developing-with-xmla-in-analysis-services.md)  
  
  
