---
title: RECONFIGURE (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 05/20/2016
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- RECONFIGURE
- RECONFIGURE_TSQL
dev_langs: TSQL
helpviewer_keywords:
- reconfiguring configuration options
- configuration options [SQL Server], reconfiguring
- updating configuration options
- RECONFIGURE, RECONFIGURE statement
- RECONFIGURE
- RECONFIGURE, WITH OVERRIDE statement
ms.assetid: 2e6e4eeb-b70b-4f45-a253-28ac4e595d75
caps.latest.revision: "50"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 432e5157969a10f36273db3bbd8990fa9e332b68
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="reconfigure-transact-sql"></a>RECONFIGURE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Actualiza el valor configurado actualmente (la **config_value** columna en el **sp_configure** conjunto de resultados) de una opción de configuración se modifica con el **sp_configure** sistema procedimiento almacenado. Dado que algunas opciones de configuración es necesario server detener y reiniciar para actualizar el valor que se está ejecutando, RECONFIGURE no siempre actualiza el valor que se está ejecutando (la **run_value** columna en el **sp_configure**  conjunto de resultados) para un valor de configuración modificado.    
    
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)    
    
## <a name="syntax"></a>Sintaxis    
    
```    
    
RECONFIGURE [ WITH OVERRIDE ]    
```    
    
## <a name="arguments"></a>Argumentos    
 RECONFIGURE    
 Especifica que, si para el valor de la configuración no es necesario que se detenga y reinicie el servidor, se debe actualizar el valor actual en ejecución. RECONFIGURE también comprueba los nuevos valores de configuración para crear los valores que no son válidos (por ejemplo, un valor de orden de ordenación no existe en **syscharsets**) o valores no recomendados. En el caso de las opciones de configuración que no requieren que se detenga y reinicie el servidor, el valor en ejecución y los valores configurados actualmente para la opción de configuración deben tener el mismo valor después de especificar RECONFIGURE.    
    
 WITH OVERRIDE    
 Deshabilita el valor de configuración comprobación (para los valores que no son válidos o recomiendan) para la **intervalo de recuperación** opción de configuración avanzada.    
    
 Puede volver a configurar casi cualquier opción de configuración mediante la opción WITH OVERRIDE, errores irrecuperables sin embargo algunas todavía pueden evitarse. Por ejemplo, el **memoria de servidor mínima** no se puede configurar la opción de configuración con un valor mayor que el valor especificado en el **memoria de servidor máxima** opción de configuración.
      
## <a name="remarks"></a>Comentarios    
 **sp_configure** no acepta nuevos valores de opción de configuración fuera de los intervalos válidos documentados para cada opción de configuración.    
    
 RECONFIGURE no se permite en una transacción implícita o explícita. Al reconfigurar varias opciones al mismo tiempo, si una de las operaciones de reconfiguración genera un error, ninguna de estas operaciones surtirá efecto.    
    
 Al volver a configurar el regulador de recursos, vea la opción de volver a configurar de [ALTER RESOURCE GOVERNOR &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-resource-governor-transact-sql.md).    
    
## <a name="permissions"></a>Permissions    
 De manera predeterminada, los permisos de RECONFIGURE corresponden a los beneficiarios del permiso ALTER SETTINGS. El **sysadmin** y **serveradmin** roles fijos de servidor tienen este permiso de forma implícita.    
    
## <a name="examples"></a>Ejemplos    
 En el ejemplo siguiente se establece el límite superior de la opción de configuración `recovery interval` en `75` minutos y se utiliza `RECONFIGURE WITH OVERRIDE` para instalarlo. No se recomiendan intervalos de recuperación superiores a 60 minutos y, por ello, no se admiten de manera predeterminada. No obstante, al especificar la opción `WITH OVERRIDE`, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no comprueba si el valor especificado (`90`) es un valor válido para la opción de configuración `recovery interval`.    
    
```    
EXEC sp_configure 'recovery interval', 75'    
RECONFIGURE WITH OVERRIDE;    
GO    
```    
    
## <a name="see-also"></a>Vea también    
 [Opciones de configuración de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)     
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)    
    
  
