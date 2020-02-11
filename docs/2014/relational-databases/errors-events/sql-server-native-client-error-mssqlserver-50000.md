---
title: MSSQLSERVER_50000 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: reference
helpviewer_keywords:
- 50000 [SQL Server Native Client setup error]
ms.assetid: 5426d87a-d5d9-4984-b211-b07d69e834a2
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 741420467a50aff6cdd0486c91dbf69224b160e7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62761625"
---
# <a name="mssqlserver_50000"></a>MSSQLSERVER_50000
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre de producto|SQL Server|  
|Versión del producto|11.0|  
|Id. de evento|50000|  
|Origen de eventos|SETUP|  
|Componente|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client|  
|Nombre simbólico||  
|Texto del mensaje|Error de red al intentar leer el archivo '%.*ls'.|  
  
## <a name="explanation"></a>Explicación  
 Se ha realizado un intento de instalación (o actualización) de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client en un equipo donde [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ya está instalado y donde la instalación existente se realizó desde un archivo MSI al que se le cambió el nombre desde sqlncli.msi.  
  
## <a name="user-action"></a>Acción del usuario  
 Para resolver este error, desinstale la versión existente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client. Para evitar este error, no instale [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client desde un archivo MSI que no se denomine sqlncli.msi.  
  
## <a name="internal-only"></a>Solo para uso interno  
  
