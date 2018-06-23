---
title: Restricciones en conexiones de contexto y normales | Documentos de Microsoft
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- context connections [CLR integration]
- regular connections [CLR integration]
ms.assetid: 0c6fe4cb-d846-40b5-8884-35a9c770f5e8
caps.latest.revision: 25
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: f0d266b75dad229a0784606af112c249728a112c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36199906"
---
# <a name="restrictions-on-regular-and-context-connections"></a>Restricciones en las conexiones normales y de contexto
  En este tema se describe las restricciones asociadas a la ejecución de código en el [!INCLUDE[msCoName](../../../includes/ssnoversion-md.md)] procesos a través de conexiones normales y de contexto.  
  
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
  
## <a name="see-also"></a>Vea también  
 [Conexión de contexto](context-connection.md)  
  
  