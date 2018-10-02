---
title: Seguridad de la contraseña de inicio de sesión de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: b0862c3a-926b-490c-a37f-382e50146a3e
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c57a5e8ca82cd24d8cc9c1e532905eb1bd830e2d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47807373"
---
# <a name="sql-server-login-password-strength"></a>Seguridad de la contraseña de inicio de sesión de SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Esta regla comprueba si "Exigir directivas de contraseñas" de cada inicio de sesión [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está habilitada. Si la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está habilitada y la versión del sistema operativo es anterior a [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)], un atacante podría aprovechar varias veces una contraseña de inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conocida.  
  
## <a name="best-practices-recommendations"></a>Prácticas recomendadas  
 Recomendamos que actualice el sistema operativo a [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)].  
  
 Si la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no se requiere en el entorno, utilice la autenticación de Windows.  
  
 Habilite "Exigir directivas de contraseña" para todos los inicios de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Use [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md) con el fin de configurar la directiva de contraseñas para el inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="for-more-information"></a>Para obtener más información  
 [Directiva de contraseñas](../../relational-databases/security/password-policy.md)  
  
## <a name="see-also"></a>Ver también  
 [Supervisar y aplicar las prácticas recomendadas usando la administración basada en directivas](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
