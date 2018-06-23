---
title: No admitida la configuración de Winsock Proxy | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Winsock proxy configuration [SQL Server]
ms.assetid: abf71f7b-8bd7-49d2-92f7-9ddf72924d8c
caps.latest.revision: 20
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 9b8af65a848d21fd04de9fe28d11160f3007a6d7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36197078"
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
 [Asesor de actualizaciones de SQL Server 2014 &#91;nuevo&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
