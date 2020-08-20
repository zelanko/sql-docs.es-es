---
description: MSSQLSERVER_948
title: MSSQLSERVER_948 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
f1_keywords:
- "948"
helpviewer_keywords:
- 948 (Database Engine error)
ms.assetid: 95c4ad45-a518-4165-a5c4-6e6b932b0570
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 76aaccfb8651792af76ff674c352f9fd9b8c6c28
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88460912"
---
# <a name="mssqlserver_948"></a>MSSQLSERVER_948
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalles  
  
| Atributo | Value |  
| :-------- | :---- |  
|Nombre de producto|SQL Server|  
|Id. de evento|948|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|N/D|  
|Texto del mensaje|No se puede abrir la base de datos "%.*ls" por tener la versión %d. Este servidor es compatible con la versión %d y anteriores. No se admite esta ruta de actualización.|  
  
## <a name="explanation"></a>Explicación  
Algunas características de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] afectan a la estructura de los archivos de base de datos. Al adjuntar una base de datos a otra instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], es posible que el formato de archivo no sea compatible con una versión distinta de [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
Por ejemplo, este error puede deberse al uso del formato de almacenamiento vardecimal en una versión posterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y a un intento posterior de adjuntar los archivos de base de datos a una versión anterior al Service Pack 2 de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
## <a name="user-action"></a>Acción del usuario  
Determine la versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está ejecutándose en el servidor de origen. En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], haga clic con el botón derecho en el servidor y, a continuación, haga clic en **Propiedades** o escriba **SELECT @@VERSION** en una ventana de consulta. Abra la base de datos utilizando la versión original de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Examine las características que están habilitadas en la base de datos original en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Modifique esta configuración para trabajar con la versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] donde se adjuntará la base de datos.  
  
