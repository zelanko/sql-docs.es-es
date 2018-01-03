---
title: Propiedades de memoria compartida | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: configuration-manager
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: shared memory [SQL Server]
ms.assetid: dc1704da-eacd-4d26-b529-c996f958ca4b
caps.latest.revision: "21"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e7998acc434cff611bd7312d4edcdcd6dc3af8be
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="shared-memory-properties"></a>Propiedades de Memoria compartida
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Use la **protocolo**página en el **propiedades de memoria compartida** cuadro de diálogo para habilitar o deshabilitar el protocolo de memoria compartida. El protocolo de memoria compartida es el más sencillo de utilizar y no tiene ningún valor configurable. Dado que los clientes que utilizan el protocolo de memoria compartida solo se pueden conectar a una instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se ejecute en el mismo equipo, no es útil para la mayoría de las actividades de la base de datos. Utilice el protocolo de memoria compartida para la solución de problemas cuando sospeche que los demás protocolos no están configurados correctamente.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="options"></a>.  
 **Enabled**  
 Los valores posibles son **Yes** y **No**. El protocolo de memoria compartida está habilitado de manera predeterminada.  
  
## <a name="see-also"></a>Vea también  
 [Elegir un protocolo de red](http://msdn.microsoft.com/library/6565fb7d-b076-4447-be90-e10d0dec359a)   
 [Crear una cadena de conexión válida con el protocolo de memoria compartida](../../tools/configuration-manager/creating-a-valid-connection-string-using-shared-memory-protocol.md)  
  
  
