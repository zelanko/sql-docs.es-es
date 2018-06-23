---
title: Permisos de invitado en bases de datos de usuario | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 540f1c6d-df51-497e-958a-3a0f429d2920
caps.latest.revision: 8
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: c8b5125b14bf772bc003af75aa819ae69ef3d8ff
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36103072"
---
# <a name="guest-permissions-on-user-databases"></a>Permisos de invitado en bases de datos de usuario
  Esta regla determina si el usuario invitado tiene permiso de acceso a la base de datos. Esta regla solo se aplica a las bases de datos de usuario.  
  
## <a name="best-practices-recommendations"></a>Prácticas recomendadas  
 Revoque el permiso del usuario invitado para tener acceso a la base de datos si no se requiere.  
  
 El usuario guest no puede quitarse, pero puede deshabilitarse si revoca su permiso CONNECT; para ello, ejecute REVOKE CONNECT FROM GUEST en cualquier base de datos que no sea master, tempdb ni msdb.  
  
## <a name="for-more-information"></a>Para obtener más información  
 [Proteger SQL Server](../security/securing-sql-server.md)  
  
## <a name="see-also"></a>Vea también  
 [Supervisar y aplicar las prácticas recomendadas usando la administración basada en directivas](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  