---
title: No se admiten índices de texto completo en las bases de datos master, tempdb y model | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- full-text indexes
ms.assetid: f7992965-42c1-4eb8-a7fb-afb38b67c740
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 743c7153b034cf5e1267c6a0da1e585845800980
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66095197"
---
# <a name="full-text-indexes-on-master-tempdb-and-model-databases-are-not-supported"></a>Los índices de texto completo no se admiten en bases de datos maestras, tempdb ni modelo
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no admite índices de texto completo en ninguna base de datos del sistema.  
  
## <a name="description"></a>Descripción  
 En [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], se admitían índices de texto completo en las bases de datos maestras, tempdb y modelo.  
  
 Se quitan los catálogos de texto completo en master, tempdb y las bases de datos de modelo durante la actualización.  
  
## <a name="see-also"></a>Vea también  
 [Trabajar con el Asesor de actualizaciones](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
