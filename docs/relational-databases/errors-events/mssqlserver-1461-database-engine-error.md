---
title: MSSQLSERVER_1461 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 1461 (Database Engine error)
ms.assetid: fce10907-4753-441b-b624-f28e00ed7520
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6411b8eaf64daf16bc42636950f43fd37104629a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68033452"
---
# <a name="mssqlserver1461"></a>MSSQLSERVER_1461
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|1461|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DBM_SAFETY_MISMATCH|  
|Texto del mensaje|Se detectaron distintos niveles de seguridad en los servidores para la creación de reflejo de la base de datos "%.*ls". Se utilizará el nivel de seguridad FULL.|  
  
## <a name="explanation"></a>Explicación  
Las conexiones de creación de reflejo se interrumpieron cuando el nivel de seguridad de la transacción se modificó porque la configuración de seguridad de la transacción era incoherente en las bases de datos principal y reflejada. Se usará la configuración de seguridad predeterminada de seguridad de transacciones completa. La sesión se ejecutará en modo de alta seguridad.  
  
## <a name="user-action"></a>Acción del usuario  
Para desactivar la seguridad de transacciones, vuelva a ejecutar la instrucción ALTER DATABASE *nombreDeBaseDeDatos* SET PARTNER SAFETY OFF en la base de datos principal.  
  
