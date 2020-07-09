---
title: MSSQLSERVER_3181 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 3181 (Database Engine error)
ms.assetid: e6d2e716-5263-477c-ad0e-7bcbfef4c1f3
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 2201c81cfc4d4f5f31fb3ab107262d0825274858
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85723685"
---
# <a name="mssqlserver_3181"></a>MSSQLSERVER_3181
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalles  
  
| Atributo | Value |  
| :-------- | :---- |  
|Nombre de producto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Id. de evento|3181|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|LDDB_STORAGE_VERIFY|  
|Texto del mensaje|Si intenta restaurar esta copia de seguridad, podría sufrir problemas de espacio de almacenamiento. Los mensajes siguientes proporcionarán más detalles.|  
  
## <a name="explanation"></a>Explicación  
La instrucción RESTORE VERIFYONLY comprueba el espacio de almacenamiento disponible en el disco en el que se restaurará la base de datos.  
  
### <a name="possible-causes"></a>Causas posibles  
El espacio en disco disponible puede ser insuficiente para restaurar la copia de seguridad comprobada.  
  
## <a name="user-action"></a>Acción del usuario  
Restaure la copia de seguridad en una ubicación con suficiente espacio en disco o libere más espacio en el disco.  
  
## <a name="see-also"></a>Consulte también  
[Restaurar una base de datos a una nueva ubicación &#40;SQL Server&#41;](~/relational-databases/backup-restore/restore-a-database-to-a-new-location-sql-server.md)  
[Restaurar archivos en una nueva ubicación &#40;SQL Server&#41;](~/relational-databases/backup-restore/restore-files-to-a-new-location-sql-server.md)  
[RESTORE &#40;Transact-SQL&#41;](~/t-sql/statements/restore-statements-transact-sql.md)  
[RESTORE VERIFYONLY &#40;Transact-SQL&#41;](~/t-sql/statements/restore-statements-verifyonly-transact-sql.md)  
  
