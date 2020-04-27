---
title: MSSQLSERVER_1101 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 1101 (Database Engine error)
ms.assetid: d63b67d5-59f5-4f77-904e-5ba67f2dd850
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d4468e85f8170ecb6b23abf5af8ee3a114a6bef3
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62870179"
---
# <a name="mssqlserver_1101"></a>MSSQLSERVER_1101
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|1101|  
|Origen de eventos|MSSQLSERVER|  
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
  
  
