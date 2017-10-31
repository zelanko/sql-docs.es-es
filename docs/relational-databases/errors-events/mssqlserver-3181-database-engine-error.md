---
title: MSSQLSERVER_3181 | Microsoft Docs
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
- 3181 (Database Engine error)
ms.assetid: e6d2e716-5263-477c-ad0e-7bcbfef4c1f3
caps.latest.revision: 13
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 745311b0a43b588bc1aead412a0c47c9ba943bb3
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver3181"></a>MSSQLSERVER_3181
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Identificador del evento|3181|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|LDDB_STORAGE_VERIFY|  
|Texto del mensaje|Si intenta restaurar esta copia de seguridad, podría sufrir problemas de espacio de almacenamiento. Los mensajes siguientes proporcionarán más detalles.|  
  
## <a name="explanation"></a>Explicación  
La instrucción RESTORE VERIFYONLY comprueba el espacio de almacenamiento disponible en el disco en el que se restaurará la base de datos.  
  
### <a name="possible-causes"></a>Posibles causas  
El espacio en disco disponible puede ser insuficiente para restaurar la copia de seguridad comprobada.  
  
## <a name="user-action"></a>Acción del usuario  
Restaure la copia de seguridad en una ubicación con suficiente espacio en disco o libere más espacio en el disco.  
  
## <a name="see-also"></a>Vea también  
[Restaurar una base de datos a una nueva ubicación &#40;SQL Server&#41;](~/relational-databases/backup-restore/restore-a-database-to-a-new-location-sql-server.md)  
[Restaurar archivos en una nueva ubicación &#40;SQL Server&#41;](~/relational-databases/backup-restore/restore-files-to-a-new-location-sql-server.md)  
[RESTORE &#40;Transact-SQL&#41;](~/t-sql/statements/restore-statements-transact-sql.md)  
[RESTORE VERIFYONLY &#40;Transact-SQL&#41;](~/t-sql/statements/restore-statements-verifyonly-transact-sql.md)  
  

