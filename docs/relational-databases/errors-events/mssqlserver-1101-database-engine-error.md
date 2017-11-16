---
title: MSSQLSERVER_1101 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 1101 (Database Engine error)
ms.assetid: d63b67d5-59f5-4f77-904e-5ba67f2dd850
caps.latest.revision: "18"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: e5928760fba84d8a2a7da76ef15026d7a0df4a36
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
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
  
