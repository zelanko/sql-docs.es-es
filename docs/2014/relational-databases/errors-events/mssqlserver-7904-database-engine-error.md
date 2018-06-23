---
title: MSSQLSERVER_7904 | Microsoft Docs
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
- 7904 (Database Engine error)
ms.assetid: d047920c-f864-4338-b15f-49820886fbc5
caps.latest.revision: 16
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 754b32656fc885fde2403297c818b5476d58f395
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36204814"
---
# <a name="mssqlserver7904"></a>MSSQLSERVER_7904
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|7904|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DBCC2_FS_MISSING_FILE|  
|Texto del mensaje|Error de tabla: no se encontró el archivo de Filestream para el Id. de columna C_ID, ROWGUID RG_ID, en el Id. de objeto O_ID, Id. de índice I_ID, Id. de partición PN_ID.|  
  
## <a name="explanation"></a>Explicación  
 Un valor de columna de una partición no tiene un archivo de FILESTREAM coincidente en el directorio de columna de FILESTREAM correspondiente.  
  
## <a name="user-action"></a>Acción del usuario  
  
### <a name="look-for-hardware-failure"></a>Busque un error de hardware  
 Ejecute un diagnóstico de hardware y corrija cualquier problema. Examine también los registros del sistema y de aplicación de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows así como el registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para ver si el error se produjo como resultado de un error de hardware. Arregle cualquier problema relacionado con el hardware que encuentre en estos registros.  
  
 Si sigue teniendo problemas de datos dañados, intente intercambiar diferentes componentes de hardware para aislar el problema. Asegúrese de que el sistema no tiene habilitada la memoria caché de escritura en el controlador de disco. Si cree que el problema se debe a la caché de escritura, póngase en contacto con su proveedor de hardware.  
  
 Finalmente, puede resultarle útil cambiar a un nuevo sistema de hardware. Este cambio puede incluir volver a formatear las unidades de disco y volver a instalar el sistema operativo.  
  
### <a name="restore-from-backup"></a>Restaure mediante la copia de seguridad  
 Si el problema no está relacionado con el hardware y tiene una copia de seguridad limpia disponible, úsela para restaurar la base de datos.  
  
### <a name="run-dbcc-checkdb"></a>Ejecute DBCC CHECKDB  
 No aplicable. Este error no se puede reparar. Si no puede restaurar la base de datos a partir de una copia de seguridad, póngase en contacto con el servicio de soporte técnico y atención al cliente (CSS) de [!INCLUDE[msCoName](../../includes/msconame-md.md)].  
  
  