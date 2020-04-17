---
title: Conexiones regulares frente a contextos ( Regular vs. Microsoft Docs
description: En SQL ServerSQL Server, a veces debe usar conexiones regulares para instrucciones Transact-SQLTransact-SQL , pero las conexiones de contexto ofrecen ventajas de rendimiento y uso de recursos.
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
ms.openlocfilehash: 881b7463400665d22baaa9b19f13cb5949df0830
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2020
ms.locfileid: "81485283"
---
# <a name="context-connections-vs-regular-connections"></a>Conexiones de contexto frente a conexiones regulares
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Si se conecta a un servidor remoto, utilice siempre conexiones normales en lugar de conexiones de contexto. Si se debe conectar al mismo servidor donde se está ejecutando el procedimiento almacenado o la función, utilice la conexión de contexto en la mayoría de los casos. Entre las ventajas que esto presenta se encuentran la ejecución en el mismo espacio de la transacción y que no es necesario volver a autenticarse.  
  
 Además, la utilización de la conexión de contexto suele proporciona un mejor rendimiento y menos uso de recursos. La conexión de contexto es una conexión solo en proceso, por lo que puede ponerse en contacto con el servidor "directamente" omitiendo el protocolo de red y las capas de transporte para enviar instrucciones Transact-SQLTransact-SQL y recibir resultados. También se omite el proceso de autenticación. En la ilustración siguiente se muestran los componentes principales del proveedor administrado **SqlClient,** así como cómo interactúan entre sí los distintos componentes cuando se usa una conexión regular y cuando se usa la conexión de contexto.  
  
 ![Rutas de acceso al código de un contexto y una conexión normal.](../../../relational-databases/clr-integration/data-access/media/clrintdataaccess.gif "Rutas de acceso al código de un contexto y una conexión normal.")  
  
 La conexión de contexto sigue una ruta de acceso al código más corta e implica menos componentes, de modo que puede esperar que las solicitudes y los resultados se envíen al servidor y de éste más rápido que en una conexión normal. El tiempo de ejecución de consultas en el servidor es el mismo en las conexiones de contexto y normales.  
  
 Hay algunos casos en los que puede necesitar abrir una conexión normal independiente al mismo servidor. Por ejemplo, hay ciertas restricciones en el uso de la conexión de contexto, que se describen en [Restricciones en conexiones regulares y](../../../relational-databases/clr-integration/data-access/context-connections-and-regular-connections-restrictions.md)de contexto .  
  
## <a name="see-also"></a>Consulte también  
 [Conexión de contexto](../../../relational-databases/clr-integration/data-access/context-connection.md)  
  
  
