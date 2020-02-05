---
title: MSSQLSERVER_1462 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 1462 (Database Engine error)
ms.assetid: 680e9c1c-a9d6-4765-b601-956d0a83324c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d53f3e8a00d0f93ac9c1738479cec05d2f01a602
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "67908571"
---
# <a name="mssqlserver_1462"></a>MSSQLSERVER_1462
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|1462|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DBM_DISABLED_DUE_TO_FAILED_REDO|  
|Texto del mensaje|La creación de reflejo de la base de datos está deshabilitada debido a una operación de puesta al día con errores. No se puede reanudar.|  
  
## <a name="explanation"></a>Explicación  
La creación de reflejo de la base de datos no puede poner al día una entrada de registro en el reflejo.  
  
### <a name="possible-causes"></a>Causas posibles  
La causa más probable es que se haya completado una operación de agregar archivos en la base de datos principal pero que haya generado un error en la base de datos reflejada al ser diferentes los nombres de archivo o estructuras de directorio en el servidor principal y reflejado.  
  
## <a name="user-action"></a>Acción del usuario  
Busque la causa de este error en el registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Intente resolver la causa y reanude la creación de reflejo de la base de datos.  
  
## <a name="see-also"></a>Consulte también  
[Solucionar problemas de configuración de creación de reflejo de la base de datos &#40;SQL Server&#41;](~/database-engine/database-mirroring/troubleshoot-database-mirroring-configuration-sql-server.md)  
  
