---
title: MSSQLSERVER_824 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 824 (Database Engine error)
ms.assetid: 2aa22246-2712-4fdb-9744-36e7e6f3175e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b5dc0afe70b6f83e458d3e132e156982f82b7e50
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/15/2018
ms.locfileid: "51664984"
---
# <a name="mssqlserver824"></a>MSSQLSERVER_824
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
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
  
Pruebe a cambiar las bases de datos para utilizar la opción PAGE_VERIFY CHECKSUM. Para obtener más información sobre cómo habilitar PAGE_VERIFY, vea [ALTER DATABASE &#40;Transact-SQL&#41;](~/t-sql/statements/alter-database-transact-sql-set-options.md).  
  
## <a name="see-also"></a>Ver también  
[Administrar la tabla suspect_pages &#40;SQL Server&#41;](~/relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)  
  
