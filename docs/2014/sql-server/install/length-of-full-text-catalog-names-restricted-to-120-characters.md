---
title: Longitud de los nombres de catálogo de texto completo restringida a 120 caracteres | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- full-text catalogs names
ms.assetid: 50633373-83f6-4ed9-99b9-71f92479a14f
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5cce05426fdff2aacf40612738ad80b07d9ec0e2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66094059"
---
# <a name="length-of-full-text-catalog-names-restricted-to-120-characters"></a>La longitud de los nombres del catálogo de texto completo está restringida a 120 caracteres
  La longitud de los nombres de catálogos de texto completo se limita a 120 caracteres, lo que representa una reducción con respecto a la limitación de 128 caracteres de versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="description"></a>Descripción  
 Este cambio no afecta a los nombres del catálogo existentes; sin embargo, los scripts que crean catálogos de texto completo con nombres con más de 120 caracteres producirán un error. Los nombres de catálogo se utilizan para generar nombres de archivo lógicos que se corresponden con los catálogos.  
  
## <a name="corrective-action"></a>Acción correctora  
 Modifique todos aquellos scripts que creen catálogos de texto completo para asegurarse de que restringen los nombres a 120 caracteres.  
  
## <a name="see-also"></a>Vea también  
 [Trabajar con el Asesor de actualizaciones](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
