---
title: MSSQLSERVER_1461 | Microsoft Docs
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
- 1461 (Database Engine error)
ms.assetid: fce10907-4753-441b-b624-f28e00ed7520
caps.latest.revision: 15
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 663aeec8ff61ce1717392c32d4f97e71403d1b5c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36108971"
---
# <a name="mssqlserver1461"></a>MSSQLSERVER_1461
    
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
  
  