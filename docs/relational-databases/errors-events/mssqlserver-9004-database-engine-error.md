---
title: MSSQLSERVER_9004 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 9004 (Database Engine error)
ms.assetid: b528bb49-340c-4a81-9c8d-cefce6562f16
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: fe4aa3b74af774543c5125652d8f860c68fb04fd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68118333"
---
# <a name="mssqlserver9004"></a>MSSQLSERVER_9004
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|9004|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|LOG_CORRUPT|  
|Texto del mensaje|Se produjo un error mientras se procesaba el registro para la base de datos '%.*ls'.  If possible, restore from backup. Si no dispone de una copia de seguridad, puede ser necesario generar de nuevo el registro.|  
  
## <a name="explanation"></a>Explicación  
Se encontró un error al procesar el registro durante la operación de reversión, recuperación o replicación. Esto puede indicar un error detectado por el sistema operativo o un error de coherencia interno detectado por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="user-action"></a>Acción del usuario  
Este error se corregirá con una de las siguientes acciones:  
  
-   Restaure desde una copia de seguridad  
  
-   Vuelva a generar el registro  
  
Además, consulte los registros de eventos y errores del sistema para identificar posibles causas del problema en el sistema.  
  
