---
title: MSSQLSERVER_8621 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 8621 (Database Engine error)
ms.assetid: 67f59865-becd-4999-8bb0-90aedd7effbf
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e4aa55a321f4eea99643ec39cbf5b72682ec7929
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62912885"
---
# <a name="mssqlserver8621"></a>MSSQLSERVER_8621
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|8621|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|OPTIMIZER_STACK_OVERFLOW_ERR|  
|Texto del mensaje|El procesador de consultas se quedó sin espacio de pila durante la optimización de la consulta. Simplifique la consulta.|  
  
## <a name="explanation"></a>Explicación  
La causa más probable del error es el tamaño de la consulta expandida. La consulta expandida sustituye en la consulta original las definiciones de cada una de las vistas, columnas calculadas, funciones de [!INCLUDE[tsql](../../includes/tsql-md.md)] y expresiones de tabla comunes a las que hace referencia, así como las acciones en cascada como actualizar los desencadenadores, vistas e índices secundarios.  
  
Lo más probable es que la consulta sea grande en alguna dimensión; por ejemplo, el número de tablas al que se hace referencia en las definiciones de vista o una expresión escalar muy grande.  
  
## <a name="user-action"></a>Acción del usuario  
Simplifique la consulta dividiéndola en varias a lo largo de la dimensión mayor. Primero quite cualquier elemento de la consulta que no sea realmente necesario y, a continuación, pruebe a agregar una tabla temporal y a dividir la consulta en dos.  No basta con mover simplemente una parte de la consulta a una subconsulta, función o expresión de tabla común porque el compilador de [!INCLUDE[tsql](../../includes/tsql-md.md)] las recombina.  
  
