---
title: Restaurar base de datos (página Archivos) | Microsoft Docs
description: Al restaurar una base de datos en SQL Server, use la página Archivos del cuadro de diálogo Restaurar base de datos para administrar los archivos concretos que se van a restaurar en la base de datos.
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql13.swb.restoredb.files.f1
- sql13.swb.restoredb.files.f1 in the code
ms.assetid: 714c36ea-a9f9-43a4-99f9-a6f73d1baf8e
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: ab1cedc6960052ec8a9007b72d9062b8fc818ab7
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85737726"
---
# <a name="restore-database-files-page"></a>Restaurar base de datos (página Archivos)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Use la página **Archivos** del cuadro de diálogo **Restaurar base de datos** para administrar los archivos concretos que ha elegido restaurar dentro de la base de datos.  
  
## <a name="options"></a>Opciones  
  
### <a name="restore-database-files-as"></a>Restaurar archivos de base de datos como  
 Se usa para asignar y administrar la nueva ruta de acceso de archivo a los archivos restaurados.  
  
 **Reubicar todos los archivos a la carpeta**  
 Reubica los archivos restaurados.  
  
|Opción|Descripción|  
|------------|-----------------|  
|**Carpeta de archivos de datos**|Escriba o busque el nombre de la carpeta de archivos de datos donde se deben reubicar el archivo o los archivos de datos restaurados.|  
|**Carpeta del archivo de registro**|Escriba o busque la carpeta del archivo o los archivos de registro donde se debe reubicar el archivo de registro restaurado.|  
  
 **Nombre de archivo lógico**  
 Muestra una fila para cada archivo de base de datos que se va a restaurar.  
  
 **Tipo de archivo**  
 Muestra el tipo de archivo.  
  
 **Nombre del archivo original**  
 Muestra la ruta de acceso del archivo original para el archivo restaurado.  
  
 **Restaurar como**  
 Enumera los nombres de archivo como los que se guardarán los archivos restaurados. Escriba o busque el nombre de archivo adecuado.  
  
## <a name="see-also"></a>Consulte también  
 [Restaurar la base de datos &#40;página General&#41;](../../relational-databases/backup-restore/restore-database-general-page.md)   
 [Restaurar base de datos &#40;página Opciones&#41;](../../relational-databases/backup-restore/restore-database-options-page.md)   
 [Argumentos RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md)   
 [Definir un dispositivo lógico de copia de seguridad en una unidad de cinta &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-tape-drive-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
  
