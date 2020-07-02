---
title: Restricciones en las conexiones normales y de contexto | Microsoft Docs
description: En este artículo se describen las restricciones asociadas al código que se ejecuta en el Microsoft SQL Server proceso a través de las conexiones de contexto y normales.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- context connections [CLR integration]
- regular connections [CLR integration]
ms.assetid: 0c6fe4cb-d846-40b5-8884-35a9c770f5e8
author: rothja
ms.author: jroth
ms.openlocfilehash: 5491e736bfa075c4cc9f001bc2515184de865ee2
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85717909"
---
# <a name="context-connections-and-regular-connections---restrictions"></a>Conexiones de contexto y conexiones normales: restricciones
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/applies-to-version/sqlserver.md)]
  En este tema se describen las restricciones asociadas al código que se ejecuta en el [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proceso a través de las conexiones de contexto y normales.  
  
## <a name="restrictions-on-context-connections"></a>Restricciones en conexiones de contexto  
 Al desarrollar su aplicación, tenga en cuenta las siguientes restricciones que se aplican a las conexiones de contexto:  
  
-   Solo puede tener una conexión de contexto abierta a una hora determinada para una conexión determinada. Si tiene varias instrucciones ejecutándose simultáneamente en conexiones independientes, cada una de ellas puede obtener su propia conexión de contexto. La restricción no afecta a solicitudes simultáneas de conexiones distintas; solo afecta a una solicitud determinada en una conexión determinada.  
  
-   No se admiten conjuntos de resultados activos múltiples (MARS) en una conexión de contexto.  
  
-   La clase **SqlBulkCopy** no funciona en una conexión de contexto.  
  
-   No se admite el procesamiento por lotes de actualizaciones en una conexión de contexto  
  
-   No se puede utilizar **SqlNotificationRequest** con comandos que se ejecutan en una conexión de contexto.  
  
-   No se admite la cancelación de comandos que están ejecutándose en la conexión de contexto. El método **SqlCommand. Cancel** omite la solicitud de forma silenciosa.  
  
-   No puede usarse ninguna otra palabra clave de cadena de conexión cuando se utiliza "context connection=true".  
  
-   La propiedad **SqlConnection. DataSource** devuelve NULL si la cadena de conexión para **SqlConnection** es "context Connection = true", en lugar del nombre de la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
-   El establecimiento de la propiedad **SqlCommand. CommandTimeout** no tiene ningún efecto cuando el comando se ejecuta en una conexión de contexto.  
  
## <a name="restrictions-on-regular-connections"></a>Restricciones en conexiones normales  
 Al desarrollar su aplicación, tenga en cuenta las siguientes restricciones que se aplican a las conexiones normales:  
  
-   No se admite la ejecución de comandos asincrónica en servidores internos. Si se incluye "Async = true" en la cadena de conexión de un comando y, a continuación, se ejecuta el comando, se produce una excepción en **System. NotSupportedException** . Aparece este mensaje: "No se admite el procesamiento asincrónico  al ejecutar el proceso de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]".  
  
-   No se admite el objeto **SqlDependency** .  
  
## <a name="see-also"></a>Consulte también  
 [Conexión de contexto](../../../relational-databases/clr-integration/data-access/context-connection.md)  
  
  
