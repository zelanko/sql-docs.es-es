---
title: Agente SQL Server categoría de trabajo de trasvase de registros causa un error de actualización | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- log shipping [SQL Server Agent]
- job categories [SQL Server Agent]
ms.assetid: ef05ce53-c6ce-42ec-9df8-46c951626424
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 2f5947e8fc8d459388fe35d86c75666e25b5d907
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85036125"
---
# <a name="sql-server-agent-log-shipping-job-category-causes-upgrade-to-fail"></a>La categoría del trabajo de trasvase de registros del Agente SQL Server provoca errores en la actualización
  Se producirá un error en el proceso de actualización si existe una categoría de trabajo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] denominada Trasvase de registros.  
  
## <a name="component"></a>Componente  
 e[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
## <a name="description"></a>Description  
 Hay una categoría de trabajo de sistema denominada Trasvase de registros. Si una instalación que se está actualizando ya contiene una categoría de trabajo creada por el usuario denominada Trasvase de registros, deberá cambiar el nombre de dicha categoría antes de llevar a cabo la actualización; de lo contrario, se producirá un error en el proceso de actualización.  
  
## <a name="see-also"></a>Consulte también  
 [El trasvase de registros no se ejecutará después de la actualización](../../../2014/sql-server/install/log-shipping-will-not-run-after-upgrading.md)   
 [La actualización cambiará la Agente SQL Server cuenta de proxy de usuario a la UpgradedProxyAccount temporal](../../../2014/sql-server/install/upgrading-changes-sql-server-agent-user-proxy-account-to-temporary-account.md)   
 [Problemas de actualización del Agente SQL Server](../../../2014/sql-server/install/sql-server-agent-upgrade-issues.md)  
  
  
