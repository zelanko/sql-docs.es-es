---
title: MSSQLSERVER_18452 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 18456 (Database Engine error)
- 18452 (Database Engine error)
ms.assetid: 21da332c-e81d-4dee-a9d2-95598911b3be
caps.latest.revision: 9
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cf867e4a9b70f2b8ab165c6daa2516492b399b06
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver18452"></a>MSSQLSERVER_18452
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|18452|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|LOGON_INVALID_CONNECT|  
|Texto del mensaje|Error de inicio de sesión del usuario '%.*ls'. El inicio de sesión es un inicio de sesión de SQL Server y no se puede usar con la autenticación de Windows.%.\*ls|  
  
## <a name="explanation"></a>Explicación  
El usuario intentó iniciar sesión con credenciales que no se pueden validar. Las posibles causas son:  
  
-   El inicio de sesión puede ser un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pero el servidor solo acepta la autenticación de Windows.  
  
-   Intenta conectar utilizando la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pero el inicio de sesión utilizado no existe en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   El inicio de sesión puede utilizar la autenticación de Windows pero el inicio de sesión es una entidad de seguridad de Windows no reconocida. Una entidad de seguridad de Windows no reconocida significa que Windows no puede comprobar el inicio de sesión. Esto podría deberse a que el inicio de sesión de Windows procede de un dominio que no es de confianza.  
  
Problemas similares pueden producir el error menos específico 18456.  
  
## <a name="user-action"></a>Acción del usuario  
Si intenta establecer conexión usando la Autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], compruebe que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está configurado en modo de autenticación mixto.  
  
Si intenta establecer conexión usando la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], compruebe que el inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] existe.  
  
Si intenta establecer conexión usando la Autenticación de Windows, compruebe que está registrado correctamente en el dominio correcto.  
  
