---
description: MSSQLSERVER_7308
title: MSSQLSERVER_7308 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 7308 (Database Engine error)
- single-threaded apartment mode
ms.assetid: cca9eab9-afb9-463d-abfd-0802257e2c99
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 568cf7ae707b3e0b8da28b0a6c0ae9b076267c6f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487050"
---
# <a name="mssqlserver_7308"></a>MSSQLSERVER_7308
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalles  
  
| Atributo | Value |  
| :-------- | :---- |  
|Nombre de producto|SQL Server|  
|Id. de evento|7308|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|RMT_STA_DISABLED|  
|Texto del mensaje|El proveedor OLE DB '%ls' no puede usarse para consultas distribuidas porque está configurado para ejecutarse en el modo de subprocesamiento controlado simple.|  
  
## <a name="explanation"></a>Explicación  
Ha utilizado un proveedor OLE DB que está configurado para ejecutarse en modo de subprocesamiento controlado simple (STA). Los proveedores OLE DB que se ejecutan en modo de subprocesamiento controlado simple (STA) no se pueden utilizar para consultas distribuidas.  
  
## <a name="user-action"></a>Acción del usuario  
Para resolver este error, configure el proveedor para ejecutarse en modo de contenedor multiproceso (MTA). Si el proveedor no admite MTA y no puede realizar una actualización a una versión que admita MTA, considere la posibilidad de configurarlo para ejecutarse fuera de proceso. El fabricante del proveedor debe indicarle si éste admite MTA o si se ha de ejecutar fuera de proceso.  
  
