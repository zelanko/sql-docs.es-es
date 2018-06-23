---
title: No se admiten índices de texto completo en las bases de datos master, tempdb y model | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- full-text indexes
ms.assetid: f7992965-42c1-4eb8-a7fb-afb38b67c740
caps.latest.revision: 21
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 1d334a3626c11050418df3fae483f5b9029adeb4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36104632"
---
# <a name="full-text-indexes-on-master-tempdb-and-model-databases-are-not-supported"></a>Los índices de texto completo no se admiten en bases de datos maestras, tempdb ni modelo
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no admite índices de texto completo en ninguna base de datos del sistema.  
  
## <a name="description"></a>Descripción  
 En [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], se admitían índices de texto completo en las bases de datos maestras, tempdb y modelo.  
  
 Los catálogos de texto completo en master, tempdb y las bases de datos de modelo se quitan durante la actualización.  
  
## <a name="see-also"></a>Vea también  
 [Trabajar con el Asesor de actualizaciones](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  