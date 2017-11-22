---
title: MSSQLSERVER_905 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 905 (Database Engine error)
ms.assetid: c828bb2e-e554-4f81-b76c-2b3740d2b944
caps.latest.revision: "14"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 648f373a5e1054ae72a462914072391f5560dce0
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver905"></a>MSSQLSERVER_905
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|905|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DBSTARTUP_EE_PARTITIONING|  
|Texto del mensaje|La base de datos '%. * ls' no se puede iniciar en esta edición de SQL Server porque contiene una función de partición '%.\*ls'. Únicamente la edición Enterprise de SQL Server admite particionamiento.|  
  
## <a name="explanation"></a>Explicación  
La base de datos contiene una o varias tablas o índices con particiones. Esta edición de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no puede utilizar particionamiento. En consecuencia, la base de datos no se puede iniciar correctamente. Las tablas e índices con particiones no están disponibles en todas las ediciones de [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener una lista de las características admitidas por las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Características compatibles con las ediciones de SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
## <a name="user-action"></a>Acción del usuario  
Separe la base de datos mediante el procedimiento almacenado sp_detach_db. Mueva los archivos si es necesario, y, a continuación, asocie la base de datos a una instancia de una edición [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizando CREATE DATABASE con las opciones FOR ATTACH o FOR ATTACH_REBUILD_LOG. Deshabilite el particionamiento en todas las tablas y quite las funciones de particionamiento. Desasocie la base de datos de nuevo y vuelva a adjuntarla al servidor actual.  
  
