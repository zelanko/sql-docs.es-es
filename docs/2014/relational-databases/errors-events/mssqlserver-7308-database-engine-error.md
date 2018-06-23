---
title: MSSQLSERVER_7308 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 7308 (Database Engine error)
- single-threaded apartment mode
ms.assetid: cca9eab9-afb9-463d-abfd-0802257e2c99
caps.latest.revision: 7
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 6a85c217cc88367f287b2d60ee56be4183ea1850
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36106964"
---
# <a name="mssqlserver7308"></a>MSSQLSERVER_7308
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|7308|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|RMT_STA_DISABLED|  
|Texto del mensaje|El proveedor OLE DB '%ls' no puede usarse para consultas distribuidas porque está configurado para ejecutarse en el modo de subprocesamiento controlado simple.|  
  
## <a name="explanation"></a>Explicación  
 Ha utilizado un proveedor OLE DB que está configurado para ejecutarse en modo de subprocesamiento controlado simple (STA). Los proveedores OLE DB que se ejecutan en modo de subprocesamiento controlado simple (STA) no se pueden utilizar para consultas distribuidas.  
  
## <a name="user-action"></a>Acción del usuario  
 Para resolver este error, configure el proveedor para ejecutarse en modo de contenedor multiproceso (MTA). Si el proveedor no admite MTA y no puede realizar una actualización a una versión que admita MTA, considere la posibilidad de configurarlo para ejecutarse fuera de proceso. El fabricante del proveedor debe indicarle si éste admite MTA o si se ha de ejecutar fuera de proceso.  
  
  