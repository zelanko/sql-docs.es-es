---
title: LOCALDB_ERROR_UNKNOWN_LANGUAGE_ID | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: reference
ms.assetid: fa082dca-bf88-46e7-b61e-7ac8835a3493
author: stevestein
ms.author: sstein
ms.openlocfilehash: 488199547cd5b96190b30ab415b08f9be2b4bd66
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85641266"
---
# <a name="localdb_error_unknown_language_id"></a>LOCALDB_ERROR_UNKNOWN_LANGUAGE_ID
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|270|  
|Origen de eventos|SQL Server Local Database Runtime 12.0|  
|Componente|API de Local Database Runtime|  
|Texto del mensaje|Error al obtener el mensaje de error localizado. El idioma especificado por el parámetro “Id. de idioma” es desconocido.|  
  
## <a name="explanation"></a>Explicación  
 El idioma solicitado para el mensaje de Local Database Runtime es desconocido o no es compatible.  
  
## <a name="user-action"></a>Acción del usuario  
 Intente solicitar uno de los idiomas compatibles para los mensajes de error de Local Database Runtime o un idioma predeterminado.  
  
  
