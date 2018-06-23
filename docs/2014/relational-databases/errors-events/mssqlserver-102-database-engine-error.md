---
title: MSSQLSERVER_102 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 102 (Database Engine error)
ms.assetid: 264dc1a2-c8a0-4c89-b5f6-951baf950299
caps.latest.revision: 7
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: ea5648a886a9b3e9c0ea2e1a9f7cdb04565444e2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36196475"
---
# <a name="mssqlserver102"></a>MSSQLSERVER_102
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|102|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|P_SYNTAXERR2|  
|Texto del mensaje|Sintaxis incorrecta cerca de '%.*ls'.|  
  
## <a name="explanation"></a>Explicación  
 Indica un error de sintaxis. La información adicional no está disponible porque el error impide que [!INCLUDE[ssDE](../../includes/ssde-md.md)] procese la instrucción.  
  
 Puede deberse a un intento de crear una clave simétrica mediante el cifrado RC4 desusado o RC4_128, cuando no está en el modo de compatibilidad 90 o 100.  
  
## <a name="user-action"></a>Acción del usuario  
 Busque la instrucción de [!INCLUDE[tsql](../../includes/tsql-md.md)] para los errores de sintaxis.  
  
 Si creó una clave simétrica mediante RC4 o RC4_128, seleccione un cifrado más reciente como, por ejemplo, uno de los algoritmos de AES. (Se recomienda). Si debe usar RC4, emplee ALTER DATABASE SET COMPATIBILITY_LEVEL para establecer el nivel de compatibilidad de la base de datos en 90 o 100. (No se recomienda).  
  
  