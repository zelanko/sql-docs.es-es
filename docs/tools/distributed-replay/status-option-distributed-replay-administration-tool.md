---
title: Opción Status (herramienta de administración de Distributed Replay) | Microsoft Docs
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: ea89386e-1598-4412-8b37-680d14b2a5b6
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: c8b3ec71769f38036e6af46e1738676a242fd607
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/10/2019
ms.locfileid: "67732570"
---
# <a name="status-option-distributed-replay-administration-tool"></a>Opción Status (herramienta de administración de Distributed Replay)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  La herramienta de administración de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay, **DReplay.exe**, es una herramienta de línea de comandos que puede usar para comunicarse con el controlador de reproducción distribuida. En este tema se describe la opción del símbolo del sistema **status** y la sintaxis correspondiente.  
  
 La opción **status** consulta el controlador y muestra el estado actual.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") Para obtener más información sobre las convenciones de sintaxis que se usan con la sintaxis de la herramienta de administración, vea [Convenciones de sintaxis de Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
dreplay status [-m controller] [-f status_interval]  
```  
  
#### <a name="parameters"></a>Parámetros  
 **-m** _controller_  
 Especifica el nombre del equipo que se va a controlar. Puede utilizar "`localhost`" o "`.`" para hacer referencia al equipo local.  
  
 Si no se especifica el parámetro **-m** , se usará el equipo local.  
  
 **-f** _status_interval_  
 Especifica la frecuencia (en segundos) con la que se muestra el estado.  
  
 Si no se especifica el parámetro **-f** , el intervalo predeterminado es de 30 segundos.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente, se muestra el estado actual cada 60 segundos. El valor `localhost` indica que el servicio del controlador se está ejecutando en el mismo equipo que la herramienta de administración.  
  
```  
dreplay status -m localhost -f 60  
```  
  
## <a name="permissions"></a>Permisos  
 Debe ejecutar la herramienta de administración como un usuario interactivo, como un usuario local o una cuenta de usuario de dominio. Para utilizar una cuenta de usuario local, la herramienta de administración y el controlador se deben estar ejecutando en el mismo equipo.  
  
 Para más información, consulte [Distributed Replay Security](../../tools/distributed-replay/distributed-replay-security.md).  
  
## <a name="see-also"></a>Consulte también  
 [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)   
 [Depurador de Transact-SQL](../../relational-databases/scripting/transact-sql-debugger.md)  
  
  
