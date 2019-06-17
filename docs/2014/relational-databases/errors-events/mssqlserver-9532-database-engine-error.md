---
title: MSSQLSERVER_9532 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 9532 (Database Engine error)
ms.assetid: ab95cce8-4f97-4aea-a746-a73eea7c9aab
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f811d554ea59539bd558e1c22c19fb118e54820f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62912412"
---
# <a name="mssqlserver9532"></a>MSSQLSERVER_9532
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|9532|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|XMLERR_COLUMNSET_CANNOT_CONVERT_FROM_TO|  
|Texto del mensaje|En la operación consulta/DML que implica al conjunto de columnas "%.*ls", no se pudo convertir el tipo de datos "%ls" al tipo "%ls" para la columna "%.\*ls".|  
  
## <a name="explanation"></a>Explicación  
 Un conjunto de columnas es una representación XML sin tipo que combina algunas columnas de una tabla en una salida estructurada. Cuando se insertan o actualizan valores de columnas dispersas mediante el conjunto de columnas XML, los valores que se insertan en las columnas dispersas subyacentes se convierten de manera implícita del tipo de datos `xml`. Se proporcionó un valor que no se puede convertir al tipo de datos de la columna.  
  
## <a name="user-action"></a>Acción del usuario  
 Dado que el valor proporcionado no se pudo convertir de manera implícita, podría ser una entrada no válida. Corrija el error e inténtelo de nuevo. Si el valor es correcto, modifique la instrucción para utilizar las columnas individuales en lugar del conjunto de columnas. Esto permitirá convertir de manera explícita el valor al tipo de datos correcto.  
  
  
