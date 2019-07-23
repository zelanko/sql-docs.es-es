---
title: Usar Correo electrónico de base de datos en lugar de SQL Mail | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: b08df7be-d8be-4184-a661-38ec0ac85cd1
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: c029883591c49c1be52d23a025ff522b4095a6f5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68069154"
---
# <a name="use-database-mail-instead-of-sql-mail"></a>Usar Correo electrónico de base de datos en lugar de SQL Mail
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Esta regla comprueba la vista de catálogo sys.configurations para determinar si la opción de configuración de todo el servidor SQL Mail XPs está establecida en ON.  
  
## <a name="best-practices-recommendations"></a>Prácticas recomendadas  
 SQL Mail se quitará en una versión futura de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Para enviar correo, utilice el Correo electrónico de base de datos.  
  
 SQL Mail se ejecuta en proceso para el servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Si SQL Mail se bloquea, también se bloquea el servidor. Correo electrónico de base de datos se ejecuta fuera de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en un proceso independiente, es escalable y no requiere instalar los componentes de cliente MAPI extendido en el servidor de producción.  
  
## <a name="for-more-information"></a>Para obtener más información  
 [Correo electrónico de base de datos](../../relational-databases/database-mail/database-mail.md)  
  
## <a name="see-also"></a>Consulte también  
 [Supervisar y aplicar las prácticas recomendadas usando la administración basada en directivas](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
