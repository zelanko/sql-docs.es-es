---
title: GetPathLocator (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- GetPathLocator
- GetPathLocator_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- GetPathLocator function
ms.assetid: 78b7e220-445b-4fdf-811b-7253f4f2b058
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a94f9be78e3acf4d5ea91ec3f538a021890aff16
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="getpathlocator-transact-sql"></a>GetPathLocator (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Devuelve el valor del identificador del localizador de ruta de acceso para el archivo o directorio especificado en un objeto FileTable.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
GetPathLocator(filenamespace_path)  
```  
  
## <a name="arguments"></a>Argumentos  
 *filenamespace_path*  
 Ruta de acceso del espacio de nombres en el objeto FileTable. La ruta de acceso del espacio de nombres es de tipo **nvarchar (max)**.  
  
 Cuando la base de datos pertenece a un grupo de disponibilidad AlwaysOn, la **GetPathLocator** función acepta el nombre de red virtual (VNN) o el nombre del equipo.  
  
## <a name="return-type"></a>Tipo devuelto  
 **hierarchyid**  
  
## <a name="general-remarks"></a>Notas generales  
 Para más información, consulte [Work with Directories and Paths in FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md).  
  
## <a name="examples"></a>Ejemplos  
 Puede usar el **GetPathLocator** funciona cuando hay migrar archivos desde un servidor de archivos a una FileTable. En este escenario, puede mover los archivos al objeto FileTable y reemplazar después la ruta de acceso UNC original para cada archivo por la ruta de acceso UNC del objeto FileTable. Para obtener un ejemplo completo, vea [para cargar archivos en FileTables](../../relational-databases/blob/load-files-into-filetables.md).  
  
## <a name="see-also"></a>Vea también  
 [Trabajar con directorios y rutas de acceso de FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)  
  
  
