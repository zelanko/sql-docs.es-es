---
title: Conexiones de contexto frente a Conexiones de contexto | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- context connections [CLR integration]
- regular connections [CLR integration]
ms.assetid: a1dead02-be88-4b16-8cb2-db1284856764
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 63fd25aa796be6f0fce27bfbfa5b7da36d35e2d8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47619603"
---
# <a name="context-connections-vs-regular-connections"></a>Conexiones de contexto frente a conexiones normales
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Si se conecta a un servidor remoto, utilice siempre conexiones normales en lugar de conexiones de contexto. Si se debe conectar al mismo servidor donde se está ejecutando el procedimiento almacenado o la función, utilice la conexión de contexto en la mayoría de los casos. Entre las ventajas que esto presenta se encuentran la ejecución en el mismo espacio de la transacción y que no es necesario volver a autenticarse.  
  
 Además, la utilización de la conexión de contexto suele proporciona un mejor rendimiento y menos uso de recursos. La conexión de contexto es una conexión solo en proceso, por lo que puede ponerse en contacto "directamente" con el servidor omitiendo los niveles de transporte y protocolo de red para enviar las instrucciones Transact-SQL y recibir los resultados. También se omite el proceso de autenticación. La siguiente ilustración muestra los principales componentes de la **SqlClient** administrada proveedor, así como cómo los distintos componentes interactúan entre sí cuando se usa una conexión normal y cuando se usa la conexión de contexto.  
  
 ![Rutas de código de un contexto y una conexión normal. ](../../../relational-databases/clr-integration/data-access/media/clrintdataaccess.gif "Código rutas de acceso de un contexto y una conexión normal.")  
  
 La conexión de contexto sigue una ruta de acceso al código más corta e implica menos componentes, de modo que puede esperar que las solicitudes y los resultados se envíen al servidor y de éste más rápido que en una conexión normal. El tiempo de ejecución de consultas en el servidor es el mismo en las conexiones de contexto y normales.  
  
 Hay algunos casos en los que puede necesitar abrir una conexión normal independiente al mismo servidor. Por ejemplo, hay ciertas restricciones sobre el uso de la conexión de contexto, se describe en [restricciones en conexiones de contexto y normales](../../../relational-databases/clr-integration/data-access/context-connections-and-regular-connections-restrictions.md).  
  
## <a name="see-also"></a>Vea también  
 [Conexión de contexto](../../../relational-databases/clr-integration/data-access/context-connection.md)  
  
  
