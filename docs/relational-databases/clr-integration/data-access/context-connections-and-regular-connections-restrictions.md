---
title: Restricciones en las conexiones regulares y de contexto Microsoft Docs
description: En este artículo se describen las restricciones asociadas con el código que se ejecuta en el proceso de Microsoft SQL Server a través del contexto y las conexiones regulares.
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
ms.openlocfilehash: fac92658366cceffc3d4fac5ba650f9a14501185
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2020
ms.locfileid: "81485374"
---
# <a name="context-connections-and-regular-connections---restrictions"></a>Conexiones de contexto y conexiones normales: restricciones
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  En este tema se describen las restricciones asociadas con la ejecución de código en el [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proceso a través del contexto y las conexiones regulares.  
  
## <a name="restrictions-on-context-connections"></a>Restricciones en conexiones de contexto  
 Al desarrollar su aplicación, tenga en cuenta las siguientes restricciones que se aplican a las conexiones de contexto:  
  
-   Solo puede tener una conexión de contexto abierta a una hora determinada para una conexión determinada. Si tiene varias instrucciones ejecutándose simultáneamente en conexiones independientes, cada una de ellas puede obtener su propia conexión de contexto. La restricción no afecta a solicitudes simultáneas de conexiones distintas; solo afecta a una solicitud determinada en una conexión determinada.  
  
-   No se admiten conjuntos de resultados activos múltiples (MARS) en una conexión de contexto.  
  
-   La clase **SqlBulkCopy** no funciona en una conexión de contexto.  
  
-   No se admite el procesamiento por lotes de actualizaciones en una conexión de contexto  
  
-   **SqlNotificationRequest** no se puede utilizar con comandos que se ejecutan en una conexión de contexto.  
  
-   No se admite la cancelación de comandos que están ejecutándose en la conexión de contexto. El **método SqlCommand.Cancel** omite silenciosamente la solicitud.  
  
-   No puede usarse ninguna otra palabra clave de cadena de conexión cuando se utiliza "context connection=true".  
  
-   La propiedad **SqlConnection.DataSource** devuelve null si la cadena de conexión de **SqlConnection** es "context [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]connection-true", en lugar del nombre de la instancia de .  
  
-   Establecer el **SqlCommand.CommandTimeout** propiedad no tiene ningún efecto cuando el comando se ejecuta en una conexión de contexto.  
  
## <a name="restrictions-on-regular-connections"></a>Restricciones en conexiones normales  
 Al desarrollar su aplicación, tenga en cuenta las siguientes restricciones que se aplican a las conexiones normales:  
  
-   No se admite la ejecución de comandos asincrónica en servidores internos. La inclusión de "async-true" en la cadena de conexión de un comando y, a continuación, la ejecución del comando, da como resultado **System.NotSupportedException** que se produce. Aparece este mensaje: "No se admite el procesamiento asincrónico  al ejecutar el proceso de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]".  
  
-   No se admite el objeto **SqlDependency.**  
  
## <a name="see-also"></a>Consulte también  
 [Conexión de contexto](../../../relational-databases/clr-integration/data-access/context-connection.md)  
  
  
