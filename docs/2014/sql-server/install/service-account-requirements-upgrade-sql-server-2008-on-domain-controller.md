---
title: Requisitos para la actualización a SQL Server 2008 en un controlador de dominio de la cuenta de servicio | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
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
ms.openlocfilehash: dc00c4195b54101c24bc05218e4ea7c3abac53e8
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/15/2019
ms.locfileid: "59582678"
---
# <a name="service-account-requirements-for-upgrading-to-sql-server-2008-on-a-domain-controller"></a>Requisitos de cuenta de servicio para actualizar a SQL Server 2008 en un controlador de dominio
  El Asesor de actualizaciones ha detectado una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se ejecuta bajo una cuenta de servicio de red o servicio Local en un [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] controlador de dominio. Cuando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se instala en un controlador de dominio [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)], los servicios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no se pueden ejecutar con los privilegios de una cuenta de servicio local o de servicio de red.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>Acción correctora  
 Asegúrese de que todas las cuentas de servicio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] están asignadas a cuentas de dominio o a cuentas de sistema locales. Si no se realiza esta modificación antes de actualizar, la instalación se bloqueará. Se exceptúan el Objeto de escritura de SQL de las cuentas de servicio y el Servicio del asistente de Active Directory de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ya que están codificados de forma rígida en la cuenta del servicio de red y no se pueden modificar.  
  
## <a name="see-also"></a>Vea también  
 [Problemas de actualización de motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Asesor de actualizaciones de SQL Server 2014 &#91;nuevo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
