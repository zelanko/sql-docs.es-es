---
title: Agente SQL Server servicio no puede usar la autenticación de SQL Server | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66092067"
---
# <a name="sql-server-agent-service-cannot-use-sql-server-authentication"></a>El servicio del Agente SQL Server no puede utilizar la autenticación de SQL Server
  El Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solo es compatible con la autenticación de Windows cuando el servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se conecta a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Directivas  
  
## <a name="description"></a>Descripción  
 En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solo puede sesión en la base de datos utilizando la autenticación de Windows. Esto significa que la cuenta del servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe corresponder a un usuario de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Para obtener más información, consulte los temas "Seguridad para la administración automática" e "Implementar la seguridad del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]" en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte también  
 [Problemas de actualización del Agente SQL Server](../../../2014/sql-server/install/sql-server-agent-upgrade-issues.md)  
  
  
