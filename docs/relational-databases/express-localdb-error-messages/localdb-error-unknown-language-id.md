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
ms.openlocfilehash: 053fb88279d0aa2ad664e50d4b9c6bbb454f2adb
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/28/2020
ms.locfileid: "87245938"
---
# <a name="localdb_error_unknown_language_id"></a>LOCALDB_ERROR_UNKNOWN_LANGUAGE_ID
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
## <a name="details"></a>Detalles  
  
| Atributo | Value |
| --------- | ----- |
|Nombre de producto|SQL Server|  
|Id. de evento|270|  
|Origen de eventos|SQL Server Local Database Runtime 12.0|  
|Componente|API de Local Database Runtime|  
|Texto del mensaje|Error al obtener el mensaje de error localizado. El idioma especificado por el parámetro “Id. de idioma” es desconocido.|  
  
## <a name="explanation"></a>Explicación  
 El idioma solicitado para el mensaje de Local Database Runtime es desconocido o no es compatible.  
  
## <a name="user-action"></a>Acción del usuario  
 Intente solicitar uno de los idiomas compatibles para los mensajes de error de Local Database Runtime o un idioma predeterminado.  
  
  
