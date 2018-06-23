---
title: MSSQLSERVER_9955 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 9955 (Database Engine error)
ms.assetid: 77f30570-7790-4747-b372-eac71c036e19
caps.latest.revision: 26
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: f3618984aaf0ee8b64ff73ed30c0fe88e5206c2f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36102871"
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
 [Administrador de configuración de SQL Server](../sql-server-configuration-manager.md)   
 [Establecer la cuenta del servicio para el selector del demonio de filtro completo](../search/set-the-service-account-for-the-full-text-filter-daemon-launcher.md)   
 [Búsqueda de texto completo](../search/full-text-search.md)  
  
  