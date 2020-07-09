---
title: MSSQLSERVER_3437 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 3437 (Database Engine error)
ms.assetid: b38216e2-b650-43bd-97af-061d54f60031
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6e5b5d6fbed4c37d8e572b1c6e056f613e2152dd
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85723478"
---
# <a name="mssqlserver_3437"></a>MSSQLSERVER_3437
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalles  
  
| Atributo | Value |  
| :-------- | :---- |  
|Nombre de producto|SQL Server|  
|Id. de evento|3437|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|NODTC|  
|Texto del mensaje|Error al recuperar la base de datos '%.*ls'. No se puede conectar con Microsoft DTC (Coordinador de transacciones distribuidas) para comprobar el estado de finalización de la transacción %S_XID. Corrija MS DTC y vuelva a ejecutar la recuperación.|  
  
## <a name="explanation"></a>Explicación  
Una o más transacciones distribuidas que estaban usando el Coordinador de transacciones distribuidas de [!INCLUDE[msCoName](../../includes/msconame-md.md)] (MS DTC) estaban incompletas cuando se cerró la base de datos. Se originó un error al recuperar la base de datos debido a que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no se puede conectar a MS DTC para completar o revertir las transacciones.  
  
## <a name="user-action"></a>Acción del usuario  
Para recuperar esta base de datos, primero debe resolver el problema con MS DTC. Para estudiar el problema con MS DTC, examine los registros de eventos de Windows. Si no puede resolver el problema con MS DTC y recuperar la base de datos, restaure una copia de seguridad de la base de datos.  
  
