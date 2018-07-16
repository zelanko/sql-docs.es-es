---
title: No se permiten índices de texto completo en columnas calculadas no persistentes | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- full-text indexes
ms.assetid: cba737f7-b187-47d0-8458-23dc18d18aca
caps.latest.revision: 19
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2abb3dba12ec76a4acd5c94998fad69274495203
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37303625"
---
# <a name="full-text-indexes-on-nonpersisted-computed-columns-are-not-allowed"></a>Los índices de texto completo no están permitidos en columnas calculadas no persistentes
  No puede crear índices de texto completo en columnas calculadas no deterministas e imprecisas. Estas columnas no se pueden usar como columnas de tipo o de clave de texto completo.  
  
## <a name="description"></a>Descripción  
 En [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], se puede crear un índice de texto completo utilizando una columna calculada imprecisa y no determinista como columna de tipo o como columna de clave de texto completo. No se admite el uso de esta funcionalidad. Al actualizar, quedarán deshabilitados los índices de texto completo antiguos, incompatibles o no admitidos.  
  
## <a name="corrective-action"></a>Acción correctora  
 Para habilitar estos índices de texto completo, modifique las definiciones de las columnas para que estas sean precisas y deterministas.  
  
## <a name="see-also"></a>Vea también  
 [Trabajar con el Asesor de actualizaciones](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
