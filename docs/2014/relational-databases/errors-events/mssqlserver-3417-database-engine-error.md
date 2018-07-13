---
title: MSSQLSERVER_3417 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 3417 (Database Engine error)
ms.assetid: 005829c8-cf57-4828-818a-bbe8ee2e00f0
caps.latest.revision: 17
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4776337b4d4fbbed7c2ac11cb76372dae7bd9b95
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37414794"
---
# <a name="mssqlserver3417"></a>MSSQLSERVER_3417
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|3417|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|REC_BADMASTER|  
|Texto del mensaje|No se puede recuperar la base de datos maestra. SQL Server no se puede ejecutar. Restaure la base de datos maestra desde una copia de seguridad completa, repárela o vuelva a crearla. Para obtener más información acerca de cómo volver a crear la base de datos maestra, vea los Libros en pantalla de SQL Server.|  
  
## <a name="explanation"></a>Explicación  
 SQL Server no puede iniciar la base de datos **master**. Si no se pueden poner en línea **master** o **tempdb**, SQL Server no puede ejecutarse. Este error suele ir precedido de otros errores. Revise los registros de errores para localizar el motivo original.  
  
## <a name="user-action"></a>Acción del usuario  
 Restaure la copia de seguridad de la base de datos o repare la base de datos.  
  
  
