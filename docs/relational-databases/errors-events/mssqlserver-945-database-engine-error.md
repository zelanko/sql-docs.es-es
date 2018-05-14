---
title: MSSQLSERVER_945 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 945 (Database Engine error)
ms.assetid: ee501d13-0bd9-4627-896c-ed5b1bdb88b3
caps.latest.revision: 20
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4a1689953c7d91894df13e93503eda1bc1b4d0cb
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver945"></a>MSSQLSERVER_945
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|945|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DB_IS_SHUTDOWN|  
|Texto del mensaje|No se puede abrir la base de datos '%.*ls', porque no es posible tener acceso a archivos, o la memoria o el espacio en disco son insuficientes.  Compruebe el registro de errores de SQL Server para obtener más información.|  
  
## <a name="explanation"></a>Explicación  
No se pudo obtener acceso a la base de datos porque faltan archivos u otros recursos.  
  
## <a name="user-action"></a>Acción del usuario  
Compruebe el registro de errores para obtener información adicional acerca del error de memoria, espacio en disco o permiso. Confirme la ubicación de los archivos .mdf y .ndf de la base de datos afectada y confirme que la cuenta usada por [!INCLUDE[ssDE](../../includes/ssde-md.md)] tiene permiso de acceso a esos archivos. Después de corregir el problema, reinicie la base de datos usando ALTER DATABASE para establecerla en ONLINE.  
  
