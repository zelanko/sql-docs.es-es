---
title: MSSQLSERVER_1101 | Microsoft Docs
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
- 1101 (Database Engine error)
ms.assetid: d63b67d5-59f5-4f77-904e-5ba67f2dd850
caps.latest.revision: 18
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 1b4fefd76bdbdb7fbd2ce3ea041f626b7b1842d3
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver1101"></a>MSSQLSERVER_1101
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|1101|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|NOALLOCPG|  
|Texto del mensaje|No se pudo asignar una nueva página para la base de datos '%.*ls' porque el grupo de archivos '%.\*ls' tiene espacio insuficiente en el disco. Quite objetos del grupo de archivos, agregue archivos adicionales al grupo de archivos o establezca la opción de crecimiento automático para los archivos existentes en el grupo de archivos con el fin de crear el espacio necesario.|  
  
## <a name="explanation"></a>Explicación  
No hay espacio en disco disponible en un grupo de archivos.  
  
## <a name="user-action"></a>Acción del usuario  
Las siguientes acciones pueden crear espacio disponible en el grupo de archivos.  
  
-   Active AUTOGROW.  
  
-   Agregue más archivos al grupo de archivos.  
  
-   Libere espacio en disco quitando los índices o las tablas que no sean necesarios del grupo de archivos.  
  

