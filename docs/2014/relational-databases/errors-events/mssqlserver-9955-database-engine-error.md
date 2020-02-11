---
title: MSSQLSERVER_9955 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 9955 (Database Engine error)
ms.assetid: 77f30570-7790-4747-b372-eac71c036e19
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a092a7228f5ec70247e38cf39073d946de0e56ea
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62761633"
---
# <a name="mssqlserver_9955"></a>MSSQLSERVER_9955
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|9955|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|FTXT2_MSSEARCHACCESSDENY|  
|Texto del mensaje|SQL Server no pudo crear la canalización con nombre '%ls' para comunicarse con el demonio de filtro de texto completo (error de Windows: %d). Quizá existe ya una canalización con nombre para un proceso de host de demonio de filtro, el sistema está bajo de recursos o la búsqueda del número de identificación de seguridad (SID) del grupo de cuentas de demonio de filtro dio error. Para resolver este error, termine los procesos de demonio de filtro de texto completo que se estén ejecutando y, si es necesario, configure de nuevo la cuenta de servicio del iniciador del demonio de texto completo.|  
  
## <a name="explanation"></a>Explicación  
 Este mensaje se produce porque [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no pudo crear una canalización con nombre para comunicarse con el demonio de filtro de texto completo. Quizá existe ya una canalización con nombre para un proceso de host de demonio de filtro, el sistema está bajo de recursos o la búsqueda del número de identificación de seguridad (SID) del grupo de cuentas de demonio de filtro dio error.  
  
## <a name="user-action"></a>Acción del usuario  
 Para resolver este error, termine los procesos de demonio de filtro de texto completo que se estén ejecutando y, si es necesario, configure de nuevo la cuenta host del demonio de texto completo con el Administrador de configuración de SQL Server.  
  
## <a name="see-also"></a>Consulte también  
 [Administrador de configuración de SQL Server](../sql-server-configuration-manager.md)   
 [Establecer la cuenta del servicio para el selector del demonio de filtro completo](../search/set-the-service-account-for-the-full-text-filter-daemon-launcher.md)   
 [Búsqueda de texto completo](../search/full-text-search.md)  
  
  
