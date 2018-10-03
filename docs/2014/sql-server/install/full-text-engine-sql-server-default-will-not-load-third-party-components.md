---
title: El motor de texto completo de Microsoft para SQL Server no cargará componentes de terceros sin firmar de forma predeterminada | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- Full-Text Engine for SQL service
- MSFTESQL service
ms.assetid: 029f9895-7232-4149-9362-3ab1a4133d21
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 46632ec66e9ae17351cb10a65efbac9cedfb084a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48125215"
---
# <a name="the-microsoft-full-text-engine-for-sql-server-will-not-load-unsigned-third-party-components-by-default"></a>De forma predeterminada, el motor de texto completo de Microsoft para SQL Server no cargará componentes de terceros sin firmar
  Igualmente, el motor de texto completo de [!INCLUDE[msCoName](../../includes/msconame-md.md)] para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no cargará componentes que no estén firmados por [!INCLUDE[msCoName](../../includes/msconame-md.md)].  
  
## <a name="component"></a>Componente  
 Búsqueda de texto completo  
  
## <a name="description"></a>Descripción  
 Tras la actualización, el motor de texto completo de [!INCLUDE[msCoName](../../includes/msconame-md.md)] para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no cargará, de forma predeterminada, ningún filtro de terceros, como puede ser el filtro PDF, que esté instalado actualmente en el servidor.  
  
## <a name="corrective-action"></a>Acción correctora  
 Para cargar un filtro de terceros, debe establecer *load_os_resource* y desactivar *verify_signature* en esa instancia.  
  
## <a name="see-also"></a>Vea también  
 [Trabajar con el Asesor de actualizaciones](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
