---
title: Permisos públicos de servidor | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 9a276caa-ea38-473d-92bc-26302bfcf660
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: ffdcfcecf88bfaa12a9d1defee2fc40ef3900c0b
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85774213"
---
# <a name="server-public-permissions"></a>Permisos públicos de servidor
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Esta regla determina si el rol de servidor public tiene permisos de servidor. Cada inicio de sesión que se crea en el servidor es miembro del rol de servidor public. Si esta condición se cumple, cada inicio de sesión en el servidor tendrá los permisos de servidor.  
  
## <a name="best-practices-recommendations"></a>Prácticas recomendadas  
 No conceda permisos de servidor al rol de servidor public.  
  
> [!IMPORTANT]  
>  Una vez completada la instalación, el rol **PUBLIC** tiene permiso **CONNECT** en todos los extremos, salvo **Conexión de administrador dedicada**. Esto es normal y habitualmente no se debe cambiar. (El acceso se controla a través del permiso **CONNECT SQL** , que se concede automáticamente cuando se crean nuevos inicios de sesión).  
  
### <a name="for-more-information"></a>Para obtener más información  
 [Proteger SQL Server](../../relational-databases/security/securing-sql-server.md)  
  
  
