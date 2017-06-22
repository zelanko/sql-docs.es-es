---
title: MSSQLSERVER_30089 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 9992 (Database Engine error)
ms.assetid: 188e5bde-6865-4740-a2b2-582be8f55c77
caps.latest.revision: 17
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: c42bbbb05ba2cb78628433815effb5ef7ce48132
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver30089"></a>MSSQLSERVER_30089
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|30089|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|IFTS_FDHOST_TERMINATEDABNORMAL|  
|Texto del mensaje|El proceso de host de demonio de filtro (FDHost) de texto completo se ha detenido de forma anormal. Esto puede ocurrir si un componente lingüístico mal configurado o con un funcionamiento incorrecto, como un separador de palabras, un lematizador o un filtro, ha causado un error irrecuperable durante la indización de texto completo o el procesamiento de consultas. El proceso se reiniciará de forma automática.|  
  
## <a name="explanation"></a>Explicación  
El host de demonio de filtro de texto completo ha encontrado algún problema que le ha obligado a detenerse de forma anómala. La causa del problema puede ser un documento con un formato incorrecto, un error en el filtro o en el separador de palabras, o un problema en el demonio de filtro.  
  
## <a name="user-action"></a>Acción del usuario  
Normalmente, el demonio se recuperará del error. Si el error se produce sistemáticamente, hay que investigar y solucionar el problema. Intente la siguiente acción para solucionarlo:  
  
1.  Si se ha instalado recientemente un nuevo componente lingüístico, quítelo del sistema.  
  
2.  Examine el registro de rastreo para identificar los documentos nuevos cuya indización de texto completo no ha sido posible y quítelos.  
  
## <a name="see-also"></a>Vea también  
[sp_help_fulltext_system_components &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-help-fulltext-system-components-transact-sql.md)  
[Configurar y administrar separadores de palabras y lematizadores para la búsqueda](~/relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)  
[Configurar y administrar filtros para búsquedas](~/relational-databases/search/configure-and-manage-filters-for-search.md)  
  

