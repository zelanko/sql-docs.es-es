---
title: MSSQLSERVER_11409 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 11409 (Database Engine error)
ms.assetid: 99b71a1c-a72d-4ca9-9d00-4230c9042ba5
caps.latest.revision: 9
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 5c75da8c58a1540759eb502b49e5bf6d57abc210
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36105632"
---
# <a name="mssqlserver11409"></a>MSSQLSERVER_11409
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|11409|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|ALTERCOL_COLSET_DROP|  
|Texto del mensaje|No se puede quitar el conjunto de columnas '%.*ls' de la tabla '%.\*ls' porque la tabla contiene más de 1025 columnas.|  
  
## <a name="explanation"></a>Explicación  
 Las tablas pueden contener 1024 columnas, como máximo, que no estén designadas como dispersas o calculadas. Cuando las columnas dispersas hacen que la tabla supere el número de 1024 columnas, se debe definir un conjunto de columnas para la tabla. La tabla a la que se hace referencia tiene más de 1024 columnas y se ha intentado quitar el conjunto de columnas.  
  
## <a name="user-action"></a>Acción del usuario  
 Con las columnas actuales en la tabla, debe conservar el conjunto de columnas.  
  
 Para quitar el conjunto de columnas, primero debe quitar columnas de la tabla, hasta que haya menos de 1024. A continuación, puede quitar el conjunto de columnas.  
  
  