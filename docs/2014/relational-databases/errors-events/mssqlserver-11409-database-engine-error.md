---
title: MSSQLSERVER_11409 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 11409 (Database Engine error)
ms.assetid: 99b71a1c-a72d-4ca9-9d00-4230c9042ba5
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 3afbea77db6fa0685644ed7a55ef31a9050b0cfc
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84968035"
---
# <a name="mssqlserver_11409"></a>MSSQLSERVER_11409
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|11409|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|ALTERCOL_COLSET_DROP|  
|Texto del mensaje|No se puede quitar el conjunto de columnas '%.*ls' de la tabla '%.\*ls' porque la tabla contiene más de 1025 columnas.|  
  
## <a name="explanation"></a>Explicación  
 Las tablas pueden contener 1024 columnas, como máximo, que no estén designadas como dispersas o calculadas. Cuando las columnas dispersas hacen que la tabla supere el número de 1024 columnas, se debe definir un conjunto de columnas para la tabla. La tabla a la que se hace referencia tiene más de 1024 columnas y se ha intentado quitar el conjunto de columnas.  
  
## <a name="user-action"></a>Acción del usuario  
 Con las columnas actuales en la tabla, debe conservar el conjunto de columnas.  
  
 Para quitar el conjunto de columnas, primero debe quitar columnas de la tabla, hasta que haya menos de 1024. A continuación, puede quitar el conjunto de columnas.  
  
  
