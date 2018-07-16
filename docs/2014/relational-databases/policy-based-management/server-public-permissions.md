---
title: Permisos públicos de servidor | Microsoft Docs
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
ms.assetid: 9a276caa-ea38-473d-92bc-26302bfcf660
caps.latest.revision: 11
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 13efadee3de21493d979f800f40a279581cadd03
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37246385"
---
# <a name="server-public-permissions"></a>Permisos públicos de servidor
  Esta regla determina si el rol de servidor public tiene permisos de servidor. Cada inicio de sesión que se crea en el servidor es miembro del rol de servidor public. Si esta condición se cumple, cada inicio de sesión en el servidor tendrá los permisos de servidor.  
  
## <a name="best-practices-recommendations"></a>Prácticas recomendadas  
 No conceda permisos de servidor al rol de servidor public.  
  
> [!IMPORTANT]  
>  Una vez completada la instalación la **pública** rol tiene `CONNECT` permiso en todos los extremos, salvo el **Dedicated Admin Connection**. Esto es normal y habitualmente no se debe cambiar. (El acceso se controla mediante el uso de la `CONNECT SQL` permiso que se concede automáticamente cuando se crean nuevos inicios de sesión.)  
  
### <a name="for-more-information"></a>Para obtener más información  
 [Proteger SQL Server](../security/securing-sql-server.md)  
  
  
