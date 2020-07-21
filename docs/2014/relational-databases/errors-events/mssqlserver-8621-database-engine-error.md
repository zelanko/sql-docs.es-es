---
title: MSSQLSERVER_8621 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 8621 (Database Engine error)
ms.assetid: 67f59865-becd-4999-8bb0-90aedd7effbf
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ec667184a2d59769573542f15b6fa9812b3d8e7e
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/21/2020
ms.locfileid: "86550880"
---
# <a name="mssqlserver_8621"></a>MSSQLSERVER_8621
    
## <a name="details"></a>Detalles  
  
|Atributo|Value|  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|8621|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|OPTIMIZER_STACK_OVERFLOW_ERR|  
|Texto del mensaje|El procesador de consultas se quedó sin espacio de pila durante la optimización de la consulta. Simplifique la consulta.|  
  
## <a name="explanation"></a>Explicación  
 La causa más probable del error es el tamaño de la consulta expandida. La consulta expandida sustituye en la consulta original las definiciones de cada una de las vistas, columnas calculadas, funciones de [!INCLUDE[tsql](../../includes/tsql-md.md)] y expresiones de tabla comunes a las que hace referencia, así como las acciones en cascada como actualizar los desencadenadores, vistas e índices secundarios.  
  
 Lo más probable es que la consulta sea grande en alguna dimensión; por ejemplo, el número de tablas al que se hace referencia en las definiciones de vista o una expresión escalar muy grande.  
  
## <a name="user-action"></a>Acción del usuario  
 Simplifique la consulta dividiéndola en varias a lo largo de la dimensión mayor. Primero quite cualquier elemento de la consulta que no sea realmente necesario y, a continuación, pruebe a agregar una tabla temporal y a dividir la consulta en dos.  No basta con mover simplemente una parte de la consulta a una subconsulta, función o expresión de tabla común porque el compilador de [!INCLUDE[tsql](../../includes/tsql-md.md)] las recombina.  
  
  
