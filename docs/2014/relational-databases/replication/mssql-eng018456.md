---
title: MSSQL_ENG018456 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG018456 error
ms.assetid: 3daa8144-d81f-445a-b6c3-4bb3e9fd1526
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 2f83f3b3eeb4375fc71db8ac8988980ab86208d1
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85005568"
---
# <a name="mssql_eng018456"></a>MSSQL_ENG018456
    
## <a name="message-details"></a>Detalles del mensaje  
  
|||  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|18456|  
|Origen de eventos|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nombre simbólico||  
|Texto del mensaje|Error de inicio de sesión del usuario '%.*ls'.%.\*ls|  
  
## <a name="explanation"></a>Explicación  
 El error MSSQL_ENG018456 se produce cuando no se puede iniciar sesión. Si el mensaje de error incluye la cuenta **distributor_admin** (Error de inicio de sesión del usuario 'distributor_admin'.), el problema reside en la cuenta utilizada en la replicación. La replicación crea un servidor remoto, **repl_distributor**, que permite la comunicación entre el distribuidor y el publicador. El inicio de sesión **distributor_admin** se asocia con este servidor remoto y debe tener una contraseña válida.  
  
## <a name="user-action"></a>Acción del usuario  
 Asegúrese de que ha especificado una contraseña para esta cuenta. Para más información, vea [Proteger el distribuidor](security/secure-the-distributor.md).  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de errores y eventos &#40;replicación&#41;](errors-and-events-reference-replication.md)  
  
  
