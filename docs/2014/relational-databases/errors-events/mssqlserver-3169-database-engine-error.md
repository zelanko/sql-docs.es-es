---
title: MSSQLSERVER_3169 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- "3169"
helpviewer_keywords:
- 3169 (Database Engine error)
ms.assetid: 7d4dbed6-bb94-4908-bc03-2040a9cf63bc
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d50a3041c874cb0afbcfe430459f3fb4eed3885a
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/21/2020
ms.locfileid: "86551822"
---
# <a name="mssqlserver_3169"></a>MSSQLSERVER_3169
    
## <a name="details"></a>Detalles  
  
|Atributo|Value|  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|3169|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|N/D|  
|Texto del mensaje|Se realizó una copia de seguridad de la base de datos en una versión de servidor %ls. Esta versión no es compatible con este servidor, que utiliza la versión %ls. Restaure la base de datos en un servidor que admita la copia de seguridad, o utilice una copia de seguridad que sea compatible con este servidor.|  
  
## <a name="explanation"></a>Explicación  
 Algunas características de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] afectan a la estructura de los archivos de base de datos. Al restaurar la base de datos en otra instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], es posible que el formato de archivo no sea compatible con una versión distinta de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
 Por ejemplo, este error puede deberse al uso del formato de almacenamiento vardecimal en una versión posterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y a un intento posterior de restaurar los archivos de base de datos a una versión anterior al Service Pack 2 de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
## <a name="user-action"></a>Acción del usuario  
 Determine la versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está ejecutándose en el servidor de origen. En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , haga clic con el botón secundario en el servidor y, a continuación, haga clic en **propiedades** o escriba `SELECT @@VERSION` en una ventana de consulta. Abra la base de datos utilizando la versión original de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Examine las características que están habilitadas en la base de datos original en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Modifique esta configuración para trabajar con la versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] donde se restaurará la base de datos.  
  
  
