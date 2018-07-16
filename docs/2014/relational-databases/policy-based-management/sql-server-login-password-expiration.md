---
title: Expiración de contraseña de inicio de sesión de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 7e3bf9da-a436-433d-847a-47c30428cad3
caps.latest.revision: 8
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 233df4a6c2827ede45d915d975a6d3e311e921dc
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37251867"
---
# <a name="sql-server-login-password-expiration"></a>Expiración de contraseña de inicio de sesión de SQL Server
  Esta regla comprueba si la "expiración de contraseña" de cada inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está habilitada. Si la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está habilitada y la versión del sistema operativo es anterior a [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)], un atacante podría aprovechar varias veces una contraseña de inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conocida.  
  
## <a name="best-practices-recommendations"></a>Prácticas recomendadas  
 Recomendamos que actualice el sistema operativo a [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)].  
  
 Si la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no se requiere en el entorno, utilice la autenticación de Windows. Para obtener más información, vea [Elegir un modo de autenticación](../security/choose-an-authentication-mode.md).  
  
 Habilite la "expiración de contraseña" para todos los inicios de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Use [ALTER LOGIN](/sql/t-sql/statements/alter-login-transact-sql) con el fin de configurar la directiva de contraseñas para el inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="for-more-information"></a>Para obtener más información  
 [Directiva de contraseñas](../security/password-policy.md)  
  
## <a name="see-also"></a>Vea también  
 [Supervisar y aplicar las prácticas recomendadas usando la administración basada en directivas](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
