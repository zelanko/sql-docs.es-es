---
title: MSSQLSERVER_9955 | Microsoft Docs
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
- 9955 (Database Engine error)
ms.assetid: 77f30570-7790-4747-b372-eac71c036e19
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 8c4d27af44152bb9b9816dbcdb0af7c75ea2f4db
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver9955"></a>MSSQLSERVER_9955
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|9955|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|FTXT2_MSSEARCHACCESSDENY|  
|Texto del mensaje|SQL Server no pudo crear la canalización con nombre '%ls' para comunicarse con el demonio de filtro de texto completo (error de Windows: %d). Quizá existe ya una canalización con nombre para un proceso de host de demonio de filtro, el sistema está bajo de recursos o la búsqueda del número de identificación de seguridad (SID) del grupo de cuentas de demonio de filtro dio error. Para resolver este error, termine los procesos de demonio de filtro de texto completo que se estén ejecutando y, si es necesario, configure de nuevo la cuenta de servicio del iniciador del demonio de texto completo.|  
  
## <a name="explanation"></a>Explicación  
Este mensaje se produce porque [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no pudo crear una canalización con nombre para comunicarse con el demonio de filtro de texto completo. Quizá existe ya una canalización con nombre para un proceso de host de demonio de filtro, el sistema está bajo de recursos o la búsqueda del número de identificación de seguridad (SID) del grupo de cuentas de demonio de filtro dio error.  
  
## <a name="user-action"></a>Acción del usuario  
Para resolver este error, termine los procesos de demonio de filtro de texto completo que se estén ejecutando y, si es necesario, configure de nuevo la cuenta host del demonio de texto completo con el Administrador de configuración de SQL Server.  
  
## <a name="see-also"></a>Vea también  
[Administrador de configuración de SQL Server](~/relational-databases/sql-server-configuration-manager.md)  
[Establecer la cuenta del servicio para el selector del demonio de filtro completo](~/relational-databases/search/set-the-service-account-for-the-full-text-filter-daemon-launcher.md)  
[Búsqueda de texto completo](~/relational-databases/search/full-text-search.md)  
  

