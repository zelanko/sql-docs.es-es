---
title: Requisitos para la actualización a SQL Server 2008 en un controlador de dominio de la cuenta de servicio | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- domain controllers
- service accounts
- network service accounts
- local service accounts
ms.assetid: 574245b6-11e2-4849-b0ca-836d673ecd0d
caps.latest.revision: 16
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9cc2ec39bee7f9a64d75ccf4753220f69693155b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37301665"
---
# <a name="service-account-requirements-for-upgrading-to-sql-server-2008-on-a-domain-controller"></a>Requisitos de cuenta de servicio para actualizar a SQL Server 2008 en un controlador de dominio
  El Asesor de actualizaciones ha detectado una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se ejecuta bajo una cuenta de servicio de red o servicio Local en un [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] controlador de dominio. Cuando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se instala en un controlador de dominio [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)], los servicios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no se pueden ejecutar con los privilegios de una cuenta de servicio local o de servicio de red.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>Acción correctora  
 Asegúrese de que todas las cuentas de servicio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] están asignadas a cuentas de dominio o a cuentas de sistema locales. Si no se realiza esta modificación antes de actualizar, la instalación se bloqueará. Se exceptúan el Objeto de escritura de SQL de las cuentas de servicio y el Servicio auxiliar de Active Directory de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ya que están codificados de forma rígida en la cuenta del servicio de red y no se pueden modificar.  
  
## <a name="see-also"></a>Vea también  
 [Problemas de actualización de motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Asesor de actualizaciones de SQL Server 2014 &#91;nuevo&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
