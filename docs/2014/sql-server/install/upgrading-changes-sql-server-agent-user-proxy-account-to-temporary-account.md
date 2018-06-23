---
title: Actualización cambiará la cuenta de Proxy de usuario de agente de SQL Server a la cuenta temporal UpgradedProxyAccount | Documentos de Microsoft
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
- log shipping [SQL Server Agent]
ms.assetid: cd2d08c3-4e56-4034-8b68-0c78df8b5471
caps.latest.revision: 18
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 9bae867b97a9fc63b97506fd8900e68b670b8013
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36103945"
---
# <a name="upgrading-will-change-the-sql-server-agent-user-proxy-account-to-the-temporary-upgradedproxyaccount"></a>La actualización cambiará la cuenta de proxy de usuario del Agente SQL Server a la cuenta temporal UpgradedProxyAccount
  Los planes de mantenimiento de bases de datos que tengan habilitado el trasvase de registros no estarán habilitados tras la actualización.  
  
## <a name="component"></a>Componente  
 e[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]   
  
## <a name="description"></a>Descripción  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona un conjunto nuevo de funciones de trasvase de registros que no son directamente compatibles con los planes de mantenimiento de bases de datos.  
  
## <a name="corrective-action"></a>Acción correctora  
 Los usuarios de [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] que tienen planes de mantenimiento de bases de datos que contienen funciones de trasvase de registros deberían configurar el trasvase de registros utilizando las nuevas funciones. Para obtener más información, busque "trasvase de registros" en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vea también  
 [Categoría del trabajo de trasvase del registro de agente SQL Server provoca un error de actualización](../../../2014/sql-server/install/sql-server-agent-log-shipping-job-category-causes-upgrade-to-fail.md)   
 [Trasvase de registros no se ejecutará después de actualizar](../../../2014/sql-server/install/log-shipping-will-not-run-after-upgrading.md)  
  
  