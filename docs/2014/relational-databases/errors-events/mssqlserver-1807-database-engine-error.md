---
title: MSSQLSERVER_1807 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 1807 (Database Engine error)
ms.assetid: 13c1b240-098b-4d9e-89aa-21599548e074
caps.latest.revision: 17
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4a9df8969a0dbae5dbdb2959c621f287d08c9f75
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37420704"
---
# <a name="mssqlserver1807"></a>MSSQLSERVER_1807
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|1807|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|CANNOT_EX_LOCK|  
|Texto del mensaje|No se puede obtener un bloqueo exclusivo en la base de datos '%.*ls'. Intente la operación en otro momento.|  
  
## <a name="explanation"></a>Explicación  
 Una operación que necesita acceso exclusivo a la base de datos no pudo obtenerlo.  
  
## <a name="user-action"></a>Acción del usuario  
 Desconecte todas las conexiones a esa base de datos o vuelva a intentar ejecutar la consulta en otro momento.  
  
  
