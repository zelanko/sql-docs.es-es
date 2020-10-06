---
description: 'Supresión de errores del modelo de recuperación: opción de configuración del servidor'
title: Supresión de errores del modelo de recuperación (opción de configuración del servidor) | Microsoft Docs
ms.custom: ''
ms.date: 07/20/2020
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 942dfc62bd55d1843babb78d89b95ad602f3d938
ms.sourcegitcommit: 2f868a77903c1f1c4cecf4ea1c181deee12d5b15
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2020
ms.locfileid: "91670748"
---
# <a name="suppress-recovery-model-errors-server-configuration-option"></a>Supresión de errores del modelo de recuperación (opción de configuración del servidor)

[!INCLUDE[tsql-appliesto-xxxxxx-asdbmi-xxxx-xxx-md.md](../../includes/tsql-appliesto-xxxxxx-asdbmi-xxxx-xxx-md.md)]

Los [modelos de recuperación](../../relational-databases/backup-restore/recovery-models-sql-server.md) de SQL Server controlan el mantenimiento del registro de transacciones. El modelo de recuperación completa garantiza que no se pierda trabajo por culpa de un archivo de datos extraviado o dañado, y admite la recuperación a un momento dado en el tiempo dentro de la directiva de retención de copias de seguridad. El modelo de recuperación completa es un valor predeterminado y el único modelo de recuperación compatible con SQL Managed Instance. Los intentos de cambiar el modelo de recuperación en SQL Managed Instance devolverán un mensaje de error.

Use la opción de configuración avanzada **suppress recovery model errors** para especificar si los comandos para cambiar el modelo de recuperación de base de datos, ejecutados en SQL Managed Instance, devolverán errores o solo advertencias. Cuando esta opción se establece en 1 (ON) en SQL Managed Instance, la ejecución del comando ALTER DATABASE SET RECOVERY no cambiará el modelo de recuperación de la base de datos, y no devolverá un mensaje de error, sino de advertencia. Cuando esta opción se establece en 0 (desactivada) en SQL Managed Instance, la ejecución del comando ALTER DATABASE SET RECOVERY devolverá un mensaje de error.

La opción **suppress recovery model errors** es útil en los casos en los que las aplicaciones heredadas o de terceros intentan cambiar el modelo de recuperación a registro simple o masivo, aunque no sea un requisito crítico ni obligatorio. Cuando el cambio del modelo de recuperación es lo único que nos impide usar SQL Managed Instance, activar la opción de configuración suppress recovery model errors elimina ese impedimento. Esta opción es especialmente útil cuando no es factible ni asequible cambiar el código de aplicación mediante una solución alternativa.

## <a name="examples"></a>Ejemplos

En el ejemplo siguiente se habilita la supresión de mensajes de error relacionados con el cambio del modelo de recuperación de base de datos y, después, se ejecuta el comando para cambiar el modelo de recuperación de base de datos y devolver solo la advertencia. El modelo de recuperación no se cambia realmente. Asegúrese de reemplazar *my_database* por el nombre real de la base de datos.

```sql
-- Turn advanced configuration options on:
sp_configure 'show advanced options', 1 ;  
GO
RECONFIGURE ;  
GO

-- Enable suppression of error messages for recovery model change:
sp_configure 'suppress recovery model errors', 1 ;  
GO
RECONFIGURE ;  
GO

-- Execute command for changing recovery model to Simple:
ALTER DATABASE my_database SET RECOVERY SIMPLE;
GO
```

## <a name="see-also"></a>Consulte también

[Opciones de configuración de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)

[sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)

[RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)