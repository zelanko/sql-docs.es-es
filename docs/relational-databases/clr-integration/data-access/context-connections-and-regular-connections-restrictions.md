---
title: Restricciones en conexiones de contexto y normales | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- context connections [CLR integration]
- regular connections [CLR integration]
ms.assetid: 0c6fe4cb-d846-40b5-8884-35a9c770f5e8
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 01a520c613a93806736d8e11fd1d451fe67b4eb0
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="context-connections-and-regular-connections---restrictions"></a>Conexiones de contexto y las conexiones normales - restricciones
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
En este tema se describe las restricciones asociadas a la ejecución de código en el [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] procesos a través de conexiones normales y de contexto.  
  
## <a name="restrictions-on-context-connections"></a>Restricciones en conexiones de contexto  
 Al desarrollar su aplicación, tenga en cuenta las siguientes restricciones que se aplican a las conexiones de contexto:  
  
-   Solo puede tener una conexión de contexto abierta a una hora determinada para una conexión determinada. Si tiene varias instrucciones ejecutándose simultáneamente en conexiones independientes, cada una de ellas puede obtener su propia conexión de contexto. La restricción no afecta a solicitudes simultáneas de conexiones distintas; solo afecta a una solicitud determinada en una conexión determinada.  
  
-   No se admiten conjuntos de resultados activos múltiples (MARS) en una conexión de contexto.  
  
-   El **SqlBulkCopy** clase no funciona en una conexión de contexto.  
  
-   No se admite el procesamiento por lotes de actualizaciones en una conexión de contexto  
  
-   **SqlNotificationRequest** no se puede usar con los comandos que se ejecuta en una conexión de contexto.  
  
-   No se admite la cancelación de comandos que están ejecutándose en la conexión de contexto. El **SqlCommand.Cancel** método omite automáticamente la solicitud.  
  
-   No puede usarse ninguna otra palabra clave de cadena de conexión cuando se utiliza "context connection=true".  
  
-   El **SqlConnection.DataSource** propiedad devuelve null si la cadena de conexión para el **SqlConnection** es "conexión de contexto = true", en lugar del nombre de la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Establecer el **SqlCommand.CommandTimeout** propiedad no tiene ningún efecto cuando el comando se ejecuta en una conexión de contexto.  
  
## <a name="restrictions-on-regular-connections"></a>Restricciones en conexiones normales  
 Al desarrollar su aplicación, tenga en cuenta las siguientes restricciones que se aplican a las conexiones normales:  
  
-   No se admite la ejecución de comandos asincrónica en servidores internos. Incluido "async = true" en la cadena de conexión de un comando y, a continuación, ejecutar el comando, da como resultado **System.NotSupportedException** que se producen. Aparece este mensaje: "No se admite el procesamiento asincrónico  al ejecutar el proceso de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]".  
  
-   **SqlDependency** no admite el objeto.  
  
## <a name="see-also"></a>Vea también  
 [Conexión de contexto](../../../relational-databases/clr-integration/data-access/context-connection.md)  
  
  
