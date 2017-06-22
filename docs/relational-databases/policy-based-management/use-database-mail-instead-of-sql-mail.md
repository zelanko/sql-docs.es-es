---
title: "Usar Correo electrónico de base de datos en lugar de SQL Mail | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: b08df7be-d8be-4184-a661-38ec0ac85cd1
caps.latest.revision: 9
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 81e3e1ee2e090e7c87ad910430846be372f9267e
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="use-database-mail-instead-of-sql-mail"></a>Usar Correo electrónico de base de datos en lugar de SQL Mail
  Esta regla comprueba la vista de catálogo sys.configurations para determinar si la opción de configuración de todo el servidor SQL Mail XPs está establecida en ON.  
  
## <a name="best-practices-recommendations"></a>Prácticas recomendadas  
 SQL Mail se quitará en una versión futura de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Para enviar correo, utilice el Correo electrónico de base de datos.  
  
 SQL Mail se ejecuta en proceso para el servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Si SQL Mail se bloquea, también se bloquea el servidor. Correo electrónico de base de datos se ejecuta fuera de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en un proceso independiente, es escalable y no requiere instalar los componentes de cliente MAPI extendido en el servidor de producción.  
  
## <a name="for-more-information"></a>Para obtener más información  
 [Correo electrónico de base de datos](../../relational-databases/database-mail/database-mail.md)  
  
## <a name="see-also"></a>Vea también  
 [Supervisar y aplicar las prácticas recomendadas usando la administración basada en directivas](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
