---
title: Sys.database_filestream_options (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- database_filestream_options
- sys.database_filestream_options_TSQL
- database_filestream_options_TSQL
- sys.database_filestream_options
dev_langs:
- TSQL
helpviewer_keywords:
- sys.database_filestream_options catalog view
ms.assetid: 3383c607-0bbc-456a-ab37-7230f4cbf0e9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3038b27084dce6a84436e658c66b77dc61ead49e
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52543009"
---
# <a name="sysdatabasefilestreamoptions-transact-sql"></a>sys.database_filestream_options (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Muestra información sobre el nivel de acceso no transaccional a los datos de FILESTREAM en los objetos FileTable habilitados. Contiene una fila por cada base de datos de la instancia de SQL Server.  
  
 Para más información sobre FileTables, vea [FileTables &#40;SQL Server&#41;](../../relational-databases/blob/filetables-sql-server.md).  
  
  
|columna|Tipo|Descripción|  
|------------|----------|-----------------|  
|**database_id**|**int**|El Id. de la base de datos. Este valor es único dentro de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**directory_name**|**nvarchar(255)**|El directorio de base de datos para todos los espacios de nombres FileTable.|  
|**non_transacted_access**|**tinyint**|El nivel de acceso no transaccional a los datos de FILESTREAM habilitados. El nivel de acceso se define mediante la opción NON_TRANSACTED_ACCESS de la **CREATE DATABASE** o **ALTER DATABASE** instrucción.<br /><br /> Esta configuración tiene uno de los siguientes valores:<br /><br /> 0: no habilitado. Este es el valor predeterminado. Este nivel se establece especificando el valor **OFF** para el **NON_TRANSACTED_ACCESS** opción.<br /><br /> 1 - acceso de solo lectura. Este nivel se establece especificando el valor **READ_ONLY** para el **NON_TRANSACTED_ACCESS** opción.<br /><br /> 3 - acceso completo. Este nivel se establece especificando el valor **completa** para el **NON_TRANSACTED_ACCESS** opción.<br /><br /> 5: en transición a READONLY<br /><br /> 6: en transición a OFF|  
|**non_transacted_access_desc**|**nvarchar(60)**|La descripción del nivel de acceso no transaccional identificado en non_transacted_access.<br /><br /> Esta configuración tiene uno de los siguientes valores:<br /><br /> NONE: este es el valor predeterminado.<br /><br /> READ_ONLY<br /><br /> FULL<br /><br /> IN_TRANSITION_TO_READ_ONLY<br /><br /> IN_TRANSITION_TO_OFF|  
  
## <a name="see-also"></a>Vea también  
 [Habilitar los requisitos previos de FileTables](../../relational-databases/blob/enable-the-prerequisites-for-filetable.md)  
  
  
