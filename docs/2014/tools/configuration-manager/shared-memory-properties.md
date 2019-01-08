---
title: Propiedades de memoria compartida | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- shared memory [SQL Server]
ms.assetid: dc1704da-eacd-4d26-b529-c996f958ca4b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bea56ada3ef490225fd08892128abb482b9342a8
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52803385"
---
# <a name="shared-memory-properties"></a>Propiedades de Memoria compartida
  Utilice la página **Protocolo**del cuadro de diálogo **Propiedades de Memoria compartida** para habilitar o deshabilitar el protocolo de memoria compartida. El protocolo de memoria compartida es el más sencillo de utilizar y no tiene ningún valor configurable. Dado que los clientes que utilizan el protocolo de memoria compartida solo se pueden conectar a una instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se ejecute en el mismo equipo, no es útil para la mayoría de las actividades de la base de datos. Utilice el protocolo de memoria compartida para la solución de problemas cuando sospeche que los demás protocolos no están configurados correctamente.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="options"></a>Opciones  
 **Enabled**  
 Los valores posibles son **Yes** y **No**. El protocolo de memoria compartida está habilitado de manera predeterminada.  
  
## <a name="see-also"></a>Vea también  
 [Elegir un protocolo de red](../../../2014/tools/configuration-manager/choosing-a-network-protocol.md)   
 [Crear una cadena de conexión válida con el protocolo de memoria compartida](../../../2014/tools/configuration-manager/creating-a-valid-connection-string-using-shared-memory-protocol.md)  
  
  
