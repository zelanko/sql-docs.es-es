---
title: MSSQLSERVER_12304 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 12304 (Database Engine error)
ms.assetid: a2c252c2-e815-4ac8-a101-7af5b32e3233
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c50e4bdbfe6fd9af1c5e5a6d528a270c0b63c50f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62870356"
---
# <a name="mssqlserver12304"></a>MSSQLSERVER_12304
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|12304|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|HK_UNSUPPORTED_IDENTITY_TABLE_VAR|  
|Texto del mensaje|No se admite el uso de una tabla optimizada de memoria que utiliza la propiedad IDENTITY con ninguna de sus columnas cuando se usa el tipo fuera del contexto de un procedimiento almacenado compilado de forma nativa.|  
  
## <a name="user-action"></a>Acción del usuario  
 No utilice un tipo de tabla optimizada de memoria que utilice la propiedad de identidad con ninguna de sus columnas.  
  
## <a name="see-also"></a>Vea también  
 [OLTP en memoria &#40;optimización en memoria&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
