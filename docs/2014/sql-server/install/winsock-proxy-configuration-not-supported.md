---
title: No se admite la configuración del proxy Winsock | Microsoft Docs
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
ms.openlocfilehash: 359399852224923d0512372d13058535fdca3c7c
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85065059"
---
# <a name="winsock-proxy-configuration-not-supported"></a>No se admite la configuración del proxy WinSock
  El proxy Winsock no se puede configurar mediante [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herramientas.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descripción  
 Las herramientas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no pueden configurar los componentes de Windows.  
  
## <a name="corrective-action"></a>Acción correctora  
 Utilice Microsoft Internet Security and Acceleration (ISA) Server para publicar un equipo. Para obtener información sobre cómo configurar el proxy Winsock, vea la documentación del servidor proxy.  
  
## <a name="see-also"></a>Consulte también  
 [Problemas de actualización Motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server el asesor de actualizaciones de 2014 &#91;nuevo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
