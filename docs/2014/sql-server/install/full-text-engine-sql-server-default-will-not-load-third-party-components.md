---
title: De forma predeterminada, el motor de texto completo de Microsoft para SQL Server no cargará componentes de terceros sin firmar. Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Full-Text Engine for SQL service
- MSFTESQL service
ms.assetid: 029f9895-7232-4149-9362-3ab1a4133d21
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 12ff188fb6aa6ac286817a7cc1c3ad726483c886
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85012482"
---
# <a name="the-microsoft-full-text-engine-for-sql-server-will-not-load-unsigned-third-party-components-by-default"></a>De forma predeterminada, el motor de texto completo de Microsoft para SQL Server no cargará componentes de terceros sin firmar
  Igualmente, el motor de texto completo de [!INCLUDE[msCoName](../../includes/msconame-md.md)] para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no cargará componentes que no estén firmados por [!INCLUDE[msCoName](../../includes/msconame-md.md)].  
  
## <a name="component"></a>Componente  
 Búsqueda de texto completo  
  
## <a name="description"></a>Description  
 Tras la actualización, el motor de texto completo de [!INCLUDE[msCoName](../../includes/msconame-md.md)] para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no cargará, de forma predeterminada, ningún filtro de terceros, como puede ser el filtro PDF, que esté instalado actualmente en el servidor.  
  
## <a name="corrective-action"></a>Acción correctora  
 Para cargar un filtro de terceros, debe establecer *load_os_resource* y desactivar *verify_signature* en esa instancia.  
  
## <a name="see-also"></a>Consulte también  
 [Trabajar con el Asesor de actualizaciones](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
