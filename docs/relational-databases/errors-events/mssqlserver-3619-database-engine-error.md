---
title: MSSQLSERVER_3619 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 3619 (Database Engine error)
ms.assetid: 7d94f8d9-65ca-4fde-9c17-7b83e94a3779
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 86d99f8223cf969e5e28a6ae3eb6d453e3c07857
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "68043581"
---
# <a name="mssqlserver_3619"></a>MSSQLSERVER_3619
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|3619|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|SYS_NOLOG|  
|Texto del mensaje|No se pudo escribir un registro de punto de comprobación en la base de datos con id. %d. Espacio insuficiente para el registro. Póngase en contacto con el administrador de la base de datos para truncar el registro o asignar más espacio a los archivos de registro de base de datos.|  
  
## <a name="explanation"></a>Explicación  
El registro de transacciones se ha quedado sin espacio en disco.  
  
## <a name="user-action"></a>Acción del usuario  
Trunque el registro para liberar espacio o asigne más espacio al registro. Para obtener más información, vea "Solucionar problemas de un registro de transacciones lleno (Error 9002)" en los Libros en pantalla de SQL Server.  
  
