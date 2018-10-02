---
title: Permisos de invitado en bases de datos de usuario | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 540f1c6d-df51-497e-958a-3a0f429d2920
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 366ee3f80bacbd1cf17bcec7ed0c4e04ce892277
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47787983"
---
# <a name="guest-permissions-on-user-databases"></a>Permisos de invitado en bases de datos de usuario
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Esta regla determina si el usuario invitado tiene permiso de acceso a la base de datos. Esta regla solo se aplica a las bases de datos de usuario.  
  
## <a name="best-practices-recommendations"></a>Prácticas recomendadas  
 Revoque el permiso del usuario invitado para tener acceso a la base de datos si no se requiere.  
  
 El usuario guest no puede quitarse, pero puede deshabilitarse si revoca su permiso CONNECT; para ello, ejecute REVOKE CONNECT FROM GUEST en cualquier base de datos que no sea master, tempdb ni msdb.  
  
## <a name="for-more-information"></a>Para obtener más información  
 [Proteger SQL Server](../../relational-databases/security/securing-sql-server.md)  
  
## <a name="see-also"></a>Ver también  
 [Supervisar y aplicar las prácticas recomendadas usando la administración basada en directivas](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
