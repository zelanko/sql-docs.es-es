---
title: MSSQLSERVER_1461 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 1461 (Database Engine error)
ms.assetid: fce10907-4753-441b-b624-f28e00ed7520
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0af23b53c60ffeafcbaa99a7a499fe0a71cd551b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62869837"
---
# <a name="mssqlserver_1461"></a>MSSQLSERVER_1461
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|1461|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DBM_SAFETY_MISMATCH|  
|Texto del mensaje|Se detectaron distintos niveles de seguridad en los servidores para la creación de reflejo de la base de datos "%.*ls". Se utilizará el nivel de seguridad FULL.|  
  
## <a name="explanation"></a>Explicación  
 Las conexiones de creación de reflejo se interrumpieron cuando el nivel de seguridad de la transacción se modificó porque la configuración de seguridad de la transacción era incoherente en las bases de datos principal y reflejada. Se usará la configuración de seguridad predeterminada de seguridad de transacciones completa. La sesión se ejecutará en modo de alta seguridad.  
  
## <a name="user-action"></a>Acción del usuario  
 Para desactivar la seguridad de transacciones, vuelva a ejecutar la instrucción ALTER DATABASE *nombreDeBaseDeDatos* SET PARTNER SAFETY OFF en la base de datos principal.  
  
  
