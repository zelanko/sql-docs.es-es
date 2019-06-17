---
title: MSSQLSERVER_360 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 360 (Database Engine error)
ms.assetid: e2b7c1b2-3679-4206-9b25-6bd55ef96a2c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: bc46a5cf1252df209243623a63ec9bdc68e71873
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62867960"
---
# <a name="mssqlserver360"></a>MSSQLSERVER_360
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|360|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DML_UPDATE_SPARSE_AND_COLSET|  
|Texto del mensaje|La lista de columnas de destino de una instrucción INSERT, UPDATE o MERGE no puede contener una columna dispersa y el conjunto de columnas que la contiene. Escriba de nuevo la instrucción para incluir la columna dispersa o el conjunto de columnas, pero no ambos.|  
  
## <a name="explanation"></a>Explicación  
 Un conjunto de columnas es una representación XML sin tipo que combina algunas columnas de una tabla en una salida estructurada. Se ha intentado modificar tanto el conjunto de columnas como una columna incluida en dicho conjunto, produciendo dos referencias a la misma columna.  
  
## <a name="user-action"></a>Acción del usuario  
 Vuelva a escribir la instrucción para incluir referencias a la columna o al conjunto de columnas, pero no incluya ambos en la instrucción.  
  
  
