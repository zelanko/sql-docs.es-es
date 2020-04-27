---
title: Requisitos de la cuenta de servicio para actualizar a SQL Server 2008 en un controlador de dominio | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- domain controllers
- service accounts
- network service accounts
- local service accounts
ms.assetid: 574245b6-11e2-4849-b0ca-836d673ecd0d
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: bb703e42edcbf128ff78ca294e08fc487f06d8f8
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66092254"
---
# <a name="service-account-requirements-for-upgrading-to-sql-server-2008-on-a-domain-controller"></a>Requisitos de cuenta de servicio para actualizar a SQL Server 2008 en un controlador de dominio
  El asesor de actualizaciones ha detectado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] una instancia de que se ejecuta bajo una cuenta de servicio [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] de red o de servicio local en un controlador de dominio. Cuando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se instala en un controlador de dominio [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)], los servicios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no se pueden ejecutar con los privilegios de una cuenta de servicio local o de servicio de red.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>Acción correctora  
 Asegúrese de que todas las cuentas de servicio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] están asignadas a cuentas de dominio o a cuentas de sistema locales. Si no se realiza esta modificación antes de actualizar, la instalación se bloqueará. Se exceptúan el Objeto de escritura de SQL de las cuentas de servicio y el Servicio del asistente de Active Directory de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ya que están codificados de forma rígida en la cuenta del servicio de red y no se pueden modificar.  
  
## <a name="see-also"></a>Consulte también  
 [Problemas de actualización Motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server el asesor de actualizaciones de 2014 &#91;nuevo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
