---
title: Sys.database_filestream_options (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
caps.latest.revision: 14
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c2bce5e81e3f2e68445af8dce97b038ea81b0c26
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sysdatabasefilestreamoptions-transact-sql"></a>sys.database_filestream_options (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Muestra información sobre el nivel de acceso no transaccional a los datos de FILESTREAM en los objetos FileTable habilitados. Contiene una fila por cada base de datos de la instancia de SQL Server.  
  
 Para más información sobre FileTables, vea [FileTables &#40;SQL Server&#41;](../../relational-databases/blob/filetables-sql-server.md).  
  
  
|Columna|Tipo|Description|  
|------------|----------|-----------------|  
|**database_id**|**int**|El Id. de la base de datos. Este valor es único dentro de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**directory_name**|**nvarchar(255)**|El directorio de base de datos para todos los espacios de nombres FileTable.|  
|**non_transacted_access**|**tinyint**|El nivel de acceso no transaccional a los datos de FILESTREAM habilitados. El nivel de acceso se define mediante la opción NON_TRANSACTED_ACCESS de la **CREATE DATABASE** o **ALTER DATABASE** instrucción.<br /><br /> Esta configuración tiene uno de los siguientes valores:<br /><br /> 0: no se ha habilitado. Es el valor predeterminado. Este nivel se establece proporcionando el valor **OFF** para el **NON_TRANSACTED_ACCESS** opción.<br /><br /> 1: acceso de solo lectura. Este nivel se establece proporcionando el valor **READ_ONLY** para el **NON_TRANSACTED_ACCESS** opción.<br /><br /> 3: acceso total. Este nivel se establece proporcionando el valor **completa** para el **NON_TRANSACTED_ACCESS** opción.<br /><br /> 5: en transición a READONLY<br /><br /> 6: en transición a OFF|  
|**non_transacted_access_desc**|**nvarchar(60)**|La descripción del nivel de acceso no transaccional identificado en non_transacted_access.<br /><br /> Esta configuración tiene uno de los siguientes valores:<br /><br /> NONE: es el valor predeterminado.<br /><br /> READ_ONLY<br /><br /> FULL<br /><br /> IN_TRANSITION_TO_READ_ONLY<br /><br /> IN_TRANSITION_TO_OFF|  
  
## <a name="see-also"></a>Vea también  
 [Habilitar los requisitos previos de FileTables](../../relational-databases/blob/enable-the-prerequisites-for-filetable.md)  
  
  
