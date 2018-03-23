---
title: sysssispackagefolders (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sysdtspackagefolders90
- sysdtspackagefolders90_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysssispackagefolders system table
ms.assetid: ddc4833f-27bf-4610-b739-d257961d17ac
caps.latest.revision: ''
author: douglasl
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2c623e7e486022804b8b9722c1ec5201dd64c8a1
ms.sourcegitcommit: 34766933e3832ca36181641db4493a0d2f4d05c6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/22/2018
---
# <a name="sysssispackagefolders-transact-sql"></a>sysssispackagefolders (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una fila por cada carpeta lógica en la jerarquía de carpetas que [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usa. Estas carpetas se enumeran en el Explorador de objetos de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] al conectar con [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Una carpeta enumera paquetes que se guardan en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o en el sistema de archivos.  
  
 El **parentfolderid** columna describe la jerarquía de carpetas. La carpeta en la parte superior de la jerarquía de carpetas contiene un valor null en **parentfolderid**.  
  
 El **nombreDeCarpeta** columna contiene el nombre de las carpetas que aparecen en el Explorador de objetos.  
  
 Esta tabla se almacena en la **msdb** base de datos.  

  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**folderid**|**uniqueidentifier**|Identificador único global (GUID) de la carpeta.|  
|**parentfolderid**|**uniqueidentifier**|GUID de la carpeta primaria.|  
|**foldername**|**sysname**|Nombre de la carpeta. Este nombre aparece en la jerarquía de carpetas de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].|  
  
  
