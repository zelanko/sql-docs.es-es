---
title: Restricciones en las conexiones normales y de contexto | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- context connections [CLR integration]
- regular connections [CLR integration]
ms.assetid: 0c6fe4cb-d846-40b5-8884-35a9c770f5e8
author: rothja
ms.author: jroth
ms.openlocfilehash: 2ebf188db7213b26264d66bad7e2a4ca9f0a09af
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84970675"
---
# <a name="restrictions-on-regular-and-context-connections"></a>Restricciones en las conexiones normales y de contexto
  En este tema se describen las restricciones asociadas al código que se ejecuta en el [!INCLUDE[msCoName](../../../includes/ssnoversion-md.md)] proceso a través de las conexiones de contexto y normales.  
  
## <a name="restrictions-on-context-connections"></a>Restricciones en conexiones de contexto  
 Al desarrollar su aplicación, tenga en cuenta las siguientes restricciones que se aplican a las conexiones de contexto:  
  
-   Solo puede tener una conexión de contexto abierta a una hora determinada para una conexión determinada. Si tiene varias instrucciones ejecutándose simultáneamente en conexiones independientes, cada una de ellas puede obtener su propia conexión de contexto. La restricción no afecta a solicitudes simultáneas de conexiones distintas; solo afecta a una solicitud determinada en una conexión determinada.  
  
-   No se admiten conjuntos de resultados activos múltiples (MARS) en una conexión de contexto.  
  
-   La clase `SqlBulkCopy` no funciona en una conexión de contexto.  
  
-   No se admite el procesamiento por lotes de actualizaciones en una conexión de contexto  
  
-   `SqlNotificationRequest` no puede utilizarse con comandos que se ejecutan en una conexión de contexto.  
  
-   No se admite la cancelación de comandos que están ejecutándose en la conexión de contexto. El método `SqlCommand.Cancel` omite automáticamente la solicitud.  
  
-   No puede usarse ninguna otra palabra clave de cadena de conexión cuando se utiliza "context connection=true".  
  
-   La propiedad `SqlConnection.DataSource` devuelve NULL si la cadena de conexión para `SqlConnection` es "context connection=true", en lugar del nombre de la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   El establecimiento de la propiedad `SqlCommand.CommandTimeout` no tiene ningún efecto cuando el comando se ejecuta en una conexión de contexto.  
  
## <a name="restrictions-on-regular-connections"></a>Restricciones en conexiones normales  
 Al desarrollar su aplicación, tenga en cuenta las siguientes restricciones que se aplican a las conexiones normales:  
  
-   No se admite la ejecución de comandos asincrónica en servidores internos. Si se incluye "async=true" en la cadena de conexión de un comando y después se ejecuta el comando, se inicia una excepción `System.NotSupportedException`. Aparece este mensaje: "No se admite el procesamiento asincrónico  al ejecutar el proceso de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]".  
  
-   No se admite el objeto `SqlDependency`.  
  
## <a name="see-also"></a>Consulte también  
 [Conexión de contexto](context-connection.md)  
  
  
