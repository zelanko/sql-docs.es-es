---
title: Categoría de trabajo de trasvase de agente SQL Server produce un error de actualización | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- log shipping [SQL Server Agent]
- job categories [SQL Server Agent]
ms.assetid: ef05ce53-c6ce-42ec-9df8-46c951626424
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 61b488250267e497541f15033b347074648d3c9d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48086155"
---
# <a name="sql-server-agent-log-shipping-job-category-causes-upgrade-to-fail"></a>La categoría del trabajo de trasvase de registros del Agente SQL Server provoca errores en la actualización
  Se producirá un error en el proceso de actualización si existe una categoría de trabajo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] denominada Trasvase de registros.  
  
## <a name="component"></a>Componente  
 e[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]   
  
## <a name="description"></a>Descripción  
 Hay una categoría de trabajo de sistema denominada Trasvase de registros. Si una instalación que se está actualizando ya contiene una categoría de trabajo creada por el usuario denominada Trasvase de registros, deberá cambiar el nombre de dicha categoría antes de llevar a cabo la actualización; de lo contrario, se producirá un error en el proceso de actualización.  
  
## <a name="see-also"></a>Vea también  
 [El trasvase de registros no se ejecutará después de actualizar](../../../2014/sql-server/install/log-shipping-will-not-run-after-upgrading.md)   
 [Actualización cambiará la cuenta de Proxy de usuario de agente de SQL Server a la cuenta temporal UpgradedProxyAccount](../../../2014/sql-server/install/upgrading-changes-sql-server-agent-user-proxy-account-to-temporary-account.md)   
 [Problemas de actualización del Agente SQL Server](../../../2014/sql-server/install/sql-server-agent-upgrade-issues.md)  
  
  
