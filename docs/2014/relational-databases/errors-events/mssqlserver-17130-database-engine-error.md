---
title: MSSQLSERVER_17130 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 17130 (Database Engine error)
ms.assetid: 7ce6afca-221d-402f-89df-da7e74a339a8
caps.latest.revision: 16
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: e4f8a2414ef1d1aba309bdbaffdbcce1d6494a87
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36105139"
---
# <a name="mssqlserver17130"></a>MSSQLSERVER_17130
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|17130|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|INIT_NOLOCKSPACE|  
|Texto del mensaje|Memoria insuficiente para el número de bloqueos configurado. Se está intentando iniciar con una tabla hash de bloqueos más pequeña, lo que puede afectar al rendimiento. Póngase en contacto con el administrador de la base de datos para configurar más memoria para esta instancia del motor de base de datos.|  
  
## <a name="explanation"></a>Explicación  
 No hay suficiente memoria para el tamaño de tabla hash del administrador de bloqueos deseado.  Se intentará asignar una tabla hash menor.  
  
## <a name="user-action"></a>Acción del usuario  
 Compruebe los parámetros de configuración de memoria del servidor (memoria de servidor máxima, memoria de servidor mínima) y si hay presiones de memoria. Proporcione más memoria para SQL Server.  
  
  