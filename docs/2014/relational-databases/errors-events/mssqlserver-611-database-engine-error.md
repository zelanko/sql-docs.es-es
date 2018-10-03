---
title: MSSQLSERVER_611 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 611 (Database Engine error)
ms.assetid: ac6a213f-5c38-44ad-bc85-a62863786614
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 634c86066508aae367f90ff6e00b452a81939967
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48060445"
---
# <a name="mssqlserver611"></a>MSSQLSERVER_611
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|611|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|VAR_SIZE_TOO_BIG|  
|Texto del mensaje|No se puede insertar ni actualizar una fila porque el tamaño total de columna variable, incluida la sobrecarga, es %d bytes más del límite.|  
  
## <a name="explanation"></a>Explicación  
 El tamaño máximo de la columna de variable e es mayor que el permitido por el esquema. El Error 611 se devuelve cuando la columna de variable está por encima del límite en el caso fijo cuando el formato de almacenamiento vardecimal está habilitado, o cuando el tamaño de la columna de variable está por encima del límite permitido en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para un registro de datos comprimido.  
  
## <a name="user-action"></a>Acción del usuario  
 Reduzca el tamaño del registro.  
  
  
