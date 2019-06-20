---
title: Configuración de Winsock Proxy no se admite | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Winsock proxy configuration [SQL Server]
ms.assetid: abf71f7b-8bd7-49d2-92f7-9ddf72924d8c
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e7d5daa8042e53b9bf26ad507c4be1f361821909
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66090978"
---
# <a name="winsock-proxy-configuration-not-supported"></a>No se admite la configuración del proxy WinSock
  El proxy Winsock no se puede configurar mediante el uso de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herramientas.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descripción  
 Las herramientas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no pueden configurar los componentes de Windows.  
  
## <a name="corrective-action"></a>Acción correctora  
 Utilice Microsoft Internet Security and Acceleration (ISA) Server para publicar un equipo. Para obtener información sobre cómo configurar el proxy Winsock, vea la documentación del servidor proxy.  
  
## <a name="see-also"></a>Vea también  
 [Problemas de actualización de motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Asesor de actualizaciones de SQL Server 2014 &#91;nuevo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
