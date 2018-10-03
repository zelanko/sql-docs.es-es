---
title: Copia de seguridad y restauración de las tablas (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- system tables [SQL Server], backup tables
- backup system tables [SQL Server]
- system tables [SQL Server], restore tables
- restore system tables [SQL Server]
ms.assetid: aa615add-54e6-40f5-8b55-3728b26884ee
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 021077a7e127f9c93ee752dea7f87aa12e792d02
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47596413"
---
# <a name="backup-and-restore-tables-transact-sql"></a>Tablas de copias de seguridad y restauración (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Los temas de esta sección describen las tablas del sistema que almacenan la información que utilizan las operaciones de copias de seguridad y restauración de bases de datos.  
  
## <a name="in-this-section"></a>En esta sección  
 [backupfile](../../relational-databases/system-tables/backupfile-transact-sql.md)  
 Contiene una fila por cada archivo de datos o de registro de una base de datos.  
  
 [backupfilegroup](../../relational-databases/system-tables/backupfilegroup-transact-sql.md)  
 Contiene una fila por cada grupo de archivos de una base de datos en el momento de crear la copia de seguridad.  
  
 [backupmediafamily](../../relational-databases/system-tables/backupmediafamily-transact-sql.md)  
 Contiene una fila por cada familia de medios.  
  
 [backupmediaset](../../relational-databases/system-tables/backupmediaset-transact-sql.md)  
 Contiene una fila por cada conjunto de medios de copia de seguridad.  
  
 [backupset](../../relational-databases/system-tables/backupset-transact-sql.md)  
 Contiene una fila por cada conjunto de copia de seguridad.  
  
 [logmarkhistory](../../relational-databases/system-tables/logmarkhistory-transact-sql.md)  
 Contiene una fila por cada transacción marcada que se ha confirmado.  
  
 [restorefile](../../relational-databases/system-tables/restorefile-transact-sql.md)  
 Contiene una fila por cada archivo restaurado. Estos incluyen los archivos restaurados indirectamente por nombre de grupo de archivos.  
  
 [restorefilegroup](../../relational-databases/system-tables/restorefilegroup-transact-sql.md)  
 Contiene una fila por cada grupo de archivos restaurado.  
  
 [restorehistory](../../relational-databases/system-tables/restorehistory-transact-sql.md)  
 Contiene una fila por cada operación de restauración.  
  
 [suspect_pages](../../relational-databases/system-tables/suspect-pages-transact-sql.md)  
 Contiene una fila por cada página que dio el error 824 (con un límite de 1.000 filas).  
  
 [sysopentapes](../../relational-databases/system-tables/sysopentapes-transact-sql.md)  
 Contiene una fila por cada dispositivo de cinta abierto.  
  
  
