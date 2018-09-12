---
title: Permisos públicos de servidor | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 9a276caa-ea38-473d-92bc-26302bfcf660
caps.latest.revision: 11
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 1389d712ff00438a2e6251315e8ebcc55e7fbff2
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2018
ms.locfileid: "43813921"
---
# <a name="server-public-permissions"></a>Permisos públicos de servidor
  Esta regla determina si el rol de servidor public tiene permisos de servidor. Cada inicio de sesión que se crea en el servidor es miembro del rol de servidor public. Si esta condición se cumple, cada inicio de sesión en el servidor tendrá los permisos de servidor.  
  
## <a name="best-practices-recommendations"></a>Prácticas recomendadas  
 No conceda permisos de servidor al rol de servidor public.  
  
> [!IMPORTANT]  
>  Una vez completada la instalación la **pública** rol tiene `CONNECT` permiso en todos los extremos, salvo el **Dedicated Admin Connection**. Esto es normal y habitualmente no se debe cambiar. (El acceso se controla mediante el uso de la `CONNECT SQL` permiso que se concede automáticamente cuando se crean nuevos inicios de sesión.)  
  
### <a name="for-more-information"></a>Para obtener más información  
 [Proteger SQL Server](../security/securing-sql-server.md)  
  
  
