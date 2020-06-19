---
title: Conexiones regulares y de contexto | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- context connections [CLR integration]
- regular connections [CLR integration]
ms.assetid: a1dead02-be88-4b16-8cb2-db1284856764
author: rothja
ms.author: jroth
ms.openlocfilehash: ce531129099a8f4908bdc4b29920696d4ba3c505
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84970638"
---
# <a name="regular-vs-context-connections"></a>Conexiones normales y conexiones de contexto
  Si se conecta a un servidor remoto, utilice siempre conexiones normales en lugar de conexiones de contexto. Si se debe conectar al mismo servidor donde se está ejecutando el procedimiento almacenado o la función, utilice la conexión de contexto en la mayoría de los casos. Entre las ventajas que esto presenta se encuentran la ejecución en el mismo espacio de la transacción y que no es necesario volver a autenticarse.  
  
 Además, la utilización de la conexión de contexto suele proporciona un mejor rendimiento y menos uso de recursos. La conexión de contexto es una conexión solo en proceso, por lo que puede ponerse en contacto con el servidor "directamente" omitiendo el protocolo de red y los niveles de transporte para enviar instrucciones Transact-SQL y recibir resultados. También se omite el proceso de autenticación. En la figura siguiente se muestran los componentes principales del proveedor administrado de `SqlClient`, así como la forma en que interactúan los diferentes componentes entre sí al utilizar una conexión normal y al utilizar la conexión de contexto.  
  
 ![Rutas de acceso al código de un contexto y una conexión normal.](../../../database-engine/dev-guide/media/clrintdataaccess.gif "Rutas de acceso al código de un contexto y una conexión normal.")  
  
 La conexión de contexto sigue una ruta de acceso al código más corta e implica menos componentes, de modo que puede esperar que las solicitudes y los resultados se envíen al servidor y de éste más rápido que en una conexión normal. El tiempo de ejecución de consultas en el servidor es el mismo en las conexiones de contexto y normales.  
  
 Hay algunos casos en los que puede necesitar abrir una conexión normal independiente al mismo servidor. Por ejemplo, hay ciertas restricciones en el uso de la conexión de contexto, descrita en [restricciones de las conexiones normales y de contexto](context-connections-and-regular-connections-restrictions.md).  
  
## <a name="see-also"></a>Consulte también  
 [Conexión de contexto](context-connection.md)  
  
  
