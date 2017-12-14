---
title: Cambiar la cuenta para el registro de escalabilidad horizontal de SSIS | Microsoft Docs
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: scale-out
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: "1"
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: dcedbe0d2c2ef2c2089af1e2a8b31fbeb75ce2fc
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="change-the-account-for-scale-out-logging"></a>Cambiar la cuenta para el registro del escalabilidad horizontal
Al ejecutar paquetes en Escalabilidad horizontal, los mensajes de eventos se registran en SSISDB con un usuario creado automáticamente **##MS_SSISLogDBWorkerAgentLogin##**. El inicio de sesión de este usuario utiliza la autenticación de SQL Server. Para cambiar la cuenta, siga los pasos a continuación:

## <a name="1-create-a-user-of-ssisdb"></a>1. Crear un usuario de SSISDB
Para obtener instrucciones de creación de un usuario de base de datos, vea [Crear un usuario de base de datos](../../relational-databases/security/authentication-access/create-a-database-user.md).

## <a name="2-add-the-user-to-database-role-ssisclusterworker"></a>2. Agregar el usuario al rol de base de datos ssis_cluster_worker

Para obtener instrucciones acerca de cómo unirse a un rol de base de datos, vea [Combinar un rol](../../relational-databases/security/authentication-access/join-a-role.md).

## <a name="3-update-logging-information-in-ssisdb"></a>3. Actualizar información de registro en SSISDB
Llame al procedimiento almacenado [catalog]. [update_logdb_info] con la cadena de conexión y el nombre de SQL Server como parámetros.

#### <a name="example"></a>Ejemplo
```sql
SET @serverName = CONVERT(sysname, SERVERPROPERTY('servername'))
SET @connectionString = 'Data Source=' + @serverName + ';Initial Catalog=SSISDB;Integrated Security=SSPI;'
EXEC [internal].[update_logdb_info] @serverName, @connectionString
GO
```

## <a name="4-restart-scale-out-worker-service"></a>4. Reiniciar el servicio de trabajo de escalabilidad horizontal

> [!NOTE]
> Si usa una cuenta de usuario de Windows para el registro, debe ser la misma cuenta que ejecuta el servicio de trabajo de escalabilidad horizontal. En caso contrario, se producirá un error en el inicio de sesión de SQL Server.
