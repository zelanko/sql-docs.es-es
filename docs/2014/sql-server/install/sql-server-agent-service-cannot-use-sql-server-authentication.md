---
title: Servicio Agente SQL Server no se puede usar la autenticación de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- authentication [SQL Server Agent]
- SQL Server Authentication [SQL Server Agent]
ms.assetid: c39f3ec3-fc2c-4c12-940f-60d8d3d17660
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e16882247a123b32ba07fbbae0d1f3573fd2d678
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66092067"
---
# <a name="sql-server-agent-service-cannot-use-sql-server-authentication"></a>El servicio del Agente SQL Server no puede utilizar la autenticación de SQL Server
  El Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solo es compatible con la autenticación de Windows cuando el servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se conecta a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="component"></a>Componente  
 e[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
## <a name="description"></a>Descripción  
 En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solo puede sesión en la base de datos utilizando la autenticación de Windows. Esto significa que la cuenta del servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe corresponder a un usuario de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Para obtener más información, consulte los temas "Seguridad para la administración automática" e "Implementar la seguridad del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]" en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vea también  
 [Problemas de actualización del Agente SQL Server](../../../2014/sql-server/install/sql-server-agent-upgrade-issues.md)  
  
  
