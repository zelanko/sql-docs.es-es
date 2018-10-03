---
title: Cmdlet de PowerShell para la evaluación de la migración | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 117250d3-9982-47fe-94fd-6f29f6159940
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ea10ab18048ed4c9482874db26b4f981e66e2cc7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47661833"
---
# <a name="powershell-cmdlet-for-migration-evaluation"></a>Cmdlet de PowerShell para la evaluación de la migración
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
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
|Servidor|El nombre de la instancia de SQL Server de destino. Obligatorio en el entorno de Windows Powershell si no se proporciona el parámetro -InputObject. En SQLPS es opcional.|  
|Base de datos|El nombre de la base de datos de SQL Server de destino. Obligatorio en el entorno de Windows Powershell si no se proporciona el parámetro -InputObject. En SQLPS es opcional.|  
|Objeto|El nombre del objeto de base de datos de destino. Puede ser una tabla o un procedimiento almacenado.|  
|InputObject|El objeto SMO al que se debe dirigir el cmdlet. Obligatorio en el entorno de Windows Powershell si no se proporcionan -Server y -Database. En SQLPS es opcional.|  
|FolderPath|La carpeta en la que el cmdlet debe depositar los informes generados. Requerido.|  
  
## <a name="results"></a>Resultado  
 En la carpeta especificada en el parámetro -FolderPath, habrá dos nombres de carpeta: Tablas y Procedimientos almacenados. Si el objeto de destino es una tabla, su informe estará dentro de la carpeta Tablas. De lo contrario, estará dentro de la carpeta Procedimientos almacenados.  
  
  
