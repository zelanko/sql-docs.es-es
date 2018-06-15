---
title: sp_monitor (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_monitor_TSQL
- sp_monitor
dev_langs:
- TSQL
helpviewer_keywords:
- sp_monitor
ms.assetid: cb628496-2f9b-40e4-b018-d0831c4cb018
caps.latest.revision: 18
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 277062160e01f0111eeade2dc4a05b3c6a3ab59d
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
ms.locfileid: "33259635"
---
# <a name="spmonitor-transact-sql"></a>sp_monitor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Muestra estadísticas sobre [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_monitor  
```  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Description|  
|-----------------|-----------------|  
|**last_run**|Tiempo **sp_monitor** se ejecutó por última vez.|  
|**current_run**|Tiempo **sp_monitor** se está ejecutando.|  
|**segundos**|Número de segundos transcurridos desde la **sp_monitor** se ejecutó.|  
|**cpu_busy**|Número de segundos durante los que la CPU del equipo servidor ha realizado trabajos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**io_busy**|Número de segundos que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ha invertido en realizar operaciones de E/S.|  
|**Inactivo**|Número de segundos durante los que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ha estado inactivo.|  
|**packets_received**|Número de paquetes de entrada que ha leído [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**packets_sent**|Número de paquetes de salida escritos por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**@packet_errors**|Número de errores que ha encontrado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al leer y escribir paquetes.|  
|**total_read**|Número de lecturas que ha realizado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**total_write**|Número de escrituras que ha realizado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**total_errors**|Número de errores que ha encontrado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al leer y escribir.|  
|**Conexiones**|Número de inicios de sesión o intentos de inicio de sesión en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
  
## <a name="remarks"></a>Comentarios  
 A través de una serie de funciones, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] realiza el seguimiento del trabajo que ha realizado. Ejecutar **sp_monitor** muestra los valores devueltos por estas funciones y muestra la cantidad han cambiado desde la última vez que se ejecutó el procedimiento.  
  
 Para cada columna, la estadística se imprime en el formulario *número*(*número*)-*número*% o *número*(*número*). La primera *número* hace referencia al número de segundos (para **@cpu_busy**, **io_busy**, y **inactivo**) o el número total (para los demás variables) puesto que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se reinició. El *número* entre paréntesis hace referencia al número de segundos o al número total desde la última vez **sp_monitor** se ejecutó. El porcentaje es el porcentaje de tiempo transcurrido desde **sp_monitor** se ejecutó por última vez. Por ejemplo, si el informe muestra **cpu_busy** como 4250 (215)-68%, la CPU ha estado ocupada 4250 segundos desde [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se inició por última vez hacia arriba, 215 segundos desde **sp_monitor** fue la última ejecución y un 68 por ciento de la total de tiempo transcurrido desde **sp_monitor** se ejecutó por última vez.  
  
## <a name="permissions"></a>Permissions  
 Requiere la pertenencia al rol fijo de servidor **sysadmin** .  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se informa acerca la ocupación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```  
USE master  
EXEC sp_monitor  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
||||  
|-|-|-|  
|**last_run**|**current_run**|**segundos**|  
|29 mar 1998 11:55 a. m.|4 abr 1998 2:22 p. m.|561|  
  
||||  
|-|-|-|  
|**cpu_busy**|**io_busy**|**Inactivo**|  
|190(0)-0%|187(0)-0%|148(556)-99%|  
  
||||  
|-|-|-|  
|**packets_received**|**packets_sent**|**@packet_errors**|  
|16(1)|20(2)|0(0)|  
  
|||||  
|-|-|-|-|  
|**total_read**|**total_write**|**total_errors**|**Conexiones**|  
|141(0)|54920(127)|0(0)|4(0)|  
  
## <a name="see-also"></a>Vea también  
 [sp_who &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
