---
title: MSSQLSERVER_50000 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- 50000 [SQL Server Native Client setup error]
ms.assetid: 5426d87a-d5d9-4984-b211-b07d69e834a2
caps.latest.revision: 16
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 5fd991d6e29d8061c551033a63a356c7e28a6de0
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2018
ms.locfileid: "39532395"
---
# <a name="sql-server-native-client-error-mssqlserver50000"></a>Error de SQL Server Native Client MSSQLSERVER_50000
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Versión del producto|11.0|  
|Identificador del evento|50000|  
|Origen del evento|SETUP|  
|Componente|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client|  
|Nombre simbólico||  
|Texto del mensaje|Error de red al intentar leer el archivo '%.*ls'.|  
  
## <a name="explanation"></a>Explicación  
 Se ha realizado un intento de instalación (o actualización) de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client en un equipo donde [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ya está instalado y donde la instalación existente se realizó desde un archivo MSI al que se le cambió el nombre desde sqlncli.msi.  
  
## <a name="user-action"></a>Acción del usuario  
 Para resolver este error, desinstale la versión existente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client. Para evitar este error, no instale [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client desde un archivo MSI que no se denomine sqlncli.msi.  
  
## <a name="internal-only"></a>Solo para uso interno  
  
