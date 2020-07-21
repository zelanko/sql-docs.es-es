---
title: Permisos públicos de servidor | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 9a276caa-ea38-473d-92bc-26302bfcf660
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 7913c4715f47b8105b72b1c817dbe77e52d40539
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85066709"
---
# <a name="server-public-permissions"></a>Permisos públicos de servidor
  Esta regla determina si el rol de servidor public tiene permisos de servidor. Cada inicio de sesión que se crea en el servidor es miembro del rol de servidor public. Si esta condición se cumple, cada inicio de sesión en el servidor tendrá los permisos de servidor.  
  
## <a name="best-practices-recommendations"></a>Prácticas recomendadas  
 No conceda permisos de servidor al rol de servidor public.  
  
> [!IMPORTANT]  
>  Una vez completada la instalación, el rol **Public** tiene `CONNECT` permiso en todos los extremos excepto en la **conexión de administrador dedicada**. Esto es normal y habitualmente no se debe cambiar. (El acceso se controla mediante el permiso `CONNECT SQL` que se concede automáticamente cuando se crean nuevos inicios de sesión).  
  
### <a name="for-more-information"></a>Para obtener más información  
 [Proteger SQL Server](../security/securing-sql-server.md)  
  
  
