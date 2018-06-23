---
title: Servicio Agente SQL Server no se puede usar la autenticación de SQL Server | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- authentication [SQL Server Agent]
- SQL Server Authentication [SQL Server Agent]
ms.assetid: c39f3ec3-fc2c-4c12-940f-60d8d3d17660
caps.latest.revision: 19
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: ddda041de230fb13e2f743edc2c3867f9716c180
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36203565"
---
# <a name="sql-server-agent-service-cannot-use-sql-server-authentication"></a>El servicio del Agente SQL Server no puede utilizar la autenticación de SQL Server
  El Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solo es compatible con la autenticación de Windows cuando el servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se conecta a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="component"></a>Componente  
 e[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]   
  
## <a name="description"></a>Descripción  
 En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solo puede sesión en la base de datos utilizando la autenticación de Windows. Esto significa que la cuenta del servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe corresponder a un usuario de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Para obtener más información, consulte los temas "Seguridad para la administración automática" e "Implementar la seguridad del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]" en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vea también  
 [Problemas de actualización de agente SQL Server](../../../2014/sql-server/install/sql-server-agent-upgrade-issues.md)  
  
  