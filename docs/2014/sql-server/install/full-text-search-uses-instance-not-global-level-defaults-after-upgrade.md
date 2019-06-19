---
title: La actualización hará que la búsqueda de texto completo usar los filtros y separadores de palabras de nivel de instancia, no globales, de forma predeterminada | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- filters [Full-Text Search]
- word breakers [Full-Text Search]
ms.assetid: 93ee8fcb-d11c-49fa-8fac-51ed31a8f008
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9c81892d6b83cef87a27a836d9691779a841104a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66095059"
---
# <a name="upgrading-will-cause-full-text-search-to-use-instance-level-not-global-word-breakers-and-filters-by-default"></a>La actualización provocará que, de forma predeterminada, la búsqueda de texto completo utilice separadores y filtros de palabras de nivel de instancia, no globales
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona una manera de registrar, a nivel de instancia, nuevos separadores y filtros de palabras.  
  
## <a name="component"></a>Componente  
 Búsqueda de texto completo  
  
## <a name="description"></a>Descripción  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite el registro de nivel de instancia de nuevos separadores y filtros de palabras. Este registro de nivel de instancia proporciona un grado de aislamiento, tanto funcional como de seguridad, entre las instancias.  
  
## <a name="corrective-action"></a>Acción correctora  
 Tras realizar la actualización, utilice `sp_fulltext_service` para establecer la propiedad de servicio y `load_os_resources`, que permiten cargar los componentes. Debe ejecutar las siguientes instrucciones:  
  
 `sp_fulltext_service 'load_os_resources', 1`  
  
## <a name="see-also"></a>Vea también  
 [Trabajar con el Asesor de actualizaciones](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
