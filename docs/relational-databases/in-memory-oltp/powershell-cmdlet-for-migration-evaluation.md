---
title: "Cmdlet de PowerShell para la evaluación de la migración | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 117250d3-9982-47fe-94fd-6f29f6159940
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 618784e57397aaff751a602ddabab4687e3f229e
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="powershell-cmdlet-for-migration-evaluation"></a>Cmdlet de PowerShell para la evaluación de la migración
  El cmdlet Save-SqlMigrationReport es una herramienta que evalúa la idoneidad de la migración de varios objetos en una base de datos de SQL Server. Actualmente, se limita a evaluar la idoneidad de la migración para OLTP en memoria. El cmdlet puede ejecutarse en un entorno de Windows PowerShell con privilegios elevados y sqlps.  
  
## <a name="syntax"></a>Sintaxis  
  
```powershell  
Save-SqlMigrationReport [ -MigrationType OLTP ] [ -Server server -Database database [ -Object object_name ] ]  |  [ -InputObject smo_object ] -FolderPath path  
```  
  
#### <a name="parameters"></a>Parámetros  
 En la siguiente tabla se describen los parámetros.  
  
|Parámetros|Descripción|  
|----------------|-----------------|  
|MigrationType|El tipo de escenario de migración al que se dirige el cmdlet. Actualmente, el único valor es el OLTP predeterminado. Opcional.|  
|Server|El nombre de la instancia de SQL Server de destino. Obligatorio en el entorno de Windows Powershell si no se proporciona el parámetro -InputObject. En SQLPS es opcional.|  
|Base de datos|El nombre de la base de datos de SQL Server de destino. Obligatorio en el entorno de Windows Powershell si no se proporciona el parámetro -InputObject. En SQLPS es opcional.|  
|Object|El nombre del objeto de base de datos de destino. Puede ser una tabla o un procedimiento almacenado.|  
|InputObject|El objeto SMO al que se debe dirigir el cmdlet. Obligatorio en el entorno de Windows Powershell si no se proporcionan -Server y -Database. En SQLPS es opcional.|  
|FolderPath|La carpeta en la que el cmdlet debe depositar los informes generados. Requerido.|  
  
## <a name="results"></a>Resultado  
 En la carpeta especificada en el parámetro -FolderPath, habrá dos nombres de carpeta: Tablas y Procedimientos almacenados. Si el objeto de destino es una tabla, su informe estará dentro de la carpeta Tablas. De lo contrario, estará dentro de la carpeta Procedimientos almacenados.  
  
  
