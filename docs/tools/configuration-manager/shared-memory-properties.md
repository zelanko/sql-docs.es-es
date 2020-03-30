---
title: Propiedades de Memoria compartida
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- shared memory [SQL Server]
ms.assetid: dc1704da-eacd-4d26-b529-c996f958ca4b
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: f7c8a4dd37c0283fa6c122a7be4a7eb1f6b849fa
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "75306925"
---
# <a name="shared-memory-properties"></a>Propiedades de Memoria compartida
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  Utilice la página **Protocolo**del cuadro de diálogo **Propiedades de Memoria compartida** para habilitar o deshabilitar el protocolo de memoria compartida. El protocolo de memoria compartida es el más sencillo de utilizar y no tiene ningún valor configurable. Dado que los clientes que utilizan el protocolo de memoria compartida solo se pueden conectar a una instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se ejecute en el mismo equipo, no es útil para la mayoría de las actividades de la base de datos. Utilice el protocolo de memoria compartida para la solución de problemas cuando sospeche que los demás protocolos no están configurados correctamente.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="options"></a>Opciones  
 **Enabled**  
 Los valores posibles son **Yes** y **No**. El protocolo de memoria compartida está habilitado de manera predeterminada.  
  
## <a name="see-also"></a>Consulte también  
 [Elegir un protocolo de red](https://msdn.microsoft.com/library/6565fb7d-b076-4447-be90-e10d0dec359a)   
 [Crear una cadena de conexión válida con el protocolo de memoria compartida](../../tools/configuration-manager/creating-a-valid-connection-string-using-shared-memory-protocol.md)  
  
  
