---
title: No se admiten los índices de texto completo en las bases de datos maestra, tempdb y modelo | Microsoft Docs
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
ms.openlocfilehash: fbd5e3133ed87fed9bdaf6d668df62c6471df766
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85012457"
---
# <a name="full-text-indexes-on-master-tempdb-and-model-databases-are-not-supported"></a>Los índices de texto completo no se admiten en bases de datos maestras, tempdb ni modelo
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no admite índices de texto completo en ninguna base de datos del sistema.  
  
## <a name="description"></a>Description  
 En [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], se admitían índices de texto completo en las bases de datos maestras, tempdb y modelo.  
  
 Los catálogos de texto completo de las bases de datos maestra, tempdb y modelo se quitan durante la actualización.  
  
## <a name="see-also"></a>Consulte también  
 [Trabajar con el Asesor de actualizaciones](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
