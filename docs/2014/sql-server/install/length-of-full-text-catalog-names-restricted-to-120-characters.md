---
title: La longitud de los nombres de catálogo de texto completo está restringida a 120 caracteres | Microsoft Docs
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
ms.openlocfilehash: fa9b06fa6fe4acd79782c19a8814357721e59c24
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85045214"
---
# <a name="length-of-full-text-catalog-names-restricted-to-120-characters"></a>La longitud de los nombres del catálogo de texto completo está restringida a 120 caracteres
  La longitud de los nombres de catálogos de texto completo se limita a 120 caracteres, lo que representa una reducción con respecto a la limitación de 128 caracteres de versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="description"></a>Description  
 Este cambio no afecta a los nombres del catálogo existentes; sin embargo, los scripts que crean catálogos de texto completo con nombres con más de 120 caracteres producirán un error. Los nombres de catálogo se utilizan para generar nombres de archivo lógicos que se corresponden con los catálogos.  
  
## <a name="corrective-action"></a>Acción correctora  
 Modifique todos aquellos scripts que creen catálogos de texto completo para asegurarse de que restringen los nombres a 120 caracteres.  
  
## <a name="see-also"></a>Consulte también  
 [Trabajar con el Asesor de actualizaciones](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
