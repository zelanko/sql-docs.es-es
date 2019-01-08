---
title: MSSQLSERVER_824 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 824 (Database Engine error)
ms.assetid: 2aa22246-2712-4fdb-9744-36e7e6f3175e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ad5619983fbbaf390c756bb21a66f80487f1c076
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/13/2018
ms.locfileid: "53370257"
---
# <a name="mssqlserver824"></a>MSSQLSERVER_824
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|824|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|B_HARDSSERR|  
|Texto del mensaje|SQL Server detectó un error de E/S de coherencia lógico: %ls. Ocurrió durante %S_MSG de la página %S_PGID en la base de datos con id. %d, desplazamiento %#016I64x, archivo '%ls'.  El registro de errores de SQL Server o el registro de eventos del sistema pueden contener mensajes adicionales con más detalles.|  
  
## <a name="explanation"></a>Explicación  
 Este error indica que Windows informa de que la página se lee correctamente desde el disco, pero [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ha detectado algún problema en ella. Este error es similar al error 823, solo que Windows no detectó el error. Normalmente, suele indicar un problema en el subsistema de E/S, como errores en la unidad de disco, problemas de firmware, un controlador de dispositivo defectuoso, etc. Para obtener más información sobre los errores de E/S, vea el [capítulo 2 del documento sobre conceptos básicos de E/S de Microsoft SQL Server](https://go.microsoft.com/fwlink/?LinkId=69370).  
  
## <a name="user-action"></a>Acción del usuario  
  
### <a name="look-for-hardware-failure"></a>Busque un error de hardware  
 Ejecute un diagnóstico de hardware y corrija cualquier problema. Examine también los registros del sistema y de aplicación de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows, así como el registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para ver si el error se produjo como resultado de un error de hardware. Arregle cualquier problema relacionado con el hardware que encuentre en estos registros.  
  
 Si sigue teniendo problemas de datos dañados, intente intercambiar diferentes componentes de hardware para aislar el problema. Asegúrese de que el sistema no tiene habilitada la memoria caché de escritura en el controlador de disco. Si cree que el problema se debe a la caché de escritura, póngase en contacto con su proveedor de hardware.  
  
 Finalmente, puede resultarle útil cambiar a un nuevo sistema de hardware. Este cambio puede incluir volver a formatear las unidades de disco y volver a instalar el sistema operativo.  
  
### <a name="restore-from-backup"></a>Restaure mediante la copia de seguridad  
 Si el problema no está relacionado con el hardware y tiene una copia de seguridad limpia disponible, úsela para restaurar la base de datos.  
  
 Pruebe a cambiar las bases de datos para utilizar la opción PAGE_VERIFY CHECKSUM. Para obtener más información sobre cómo habilitar PAGE_VERIFY, vea [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql).  
  
## <a name="see-also"></a>Vea también  
 [Administrar la tabla suspect_pages &#40;SQL Server&#41;](../backup-restore/manage-the-suspect-pages-table-sql-server.md)  
  
  
