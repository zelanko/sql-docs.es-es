---
title: MSSQLSERVER_17130 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 17130 (Database Engine error)
ms.assetid: 7ce6afca-221d-402f-89df-da7e74a339a8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4f8d62a98d39a65db78f79fdfaf3ecdb2921408e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62915377"
---
# <a name="mssqlserver_17130"></a>MSSQLSERVER_17130
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|17130|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|INIT_NOLOCKSPACE|  
|Texto del mensaje|Memoria insuficiente para el número de bloqueos configurado. Se está intentando iniciar con una tabla hash de bloqueos más pequeña, lo que puede afectar al rendimiento. Póngase en contacto con el administrador de la base de datos para configurar más memoria para esta instancia del motor de base de datos.|  
  
## <a name="explanation"></a>Explicación  
 No hay suficiente memoria para el tamaño de tabla hash del administrador de bloqueos deseado.  Se intentará asignar una tabla hash menor.  
  
## <a name="user-action"></a>Acción del usuario  
 Compruebe los parámetros de configuración de memoria del servidor (memoria de servidor máxima, memoria de servidor mínima) y si hay presiones de memoria. Proporcione más memoria para SQL Server.  
  
  
