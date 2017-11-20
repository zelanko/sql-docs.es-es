---
title: Cambiar la cuenta para el registro de SSIS horizontalmente | Documentos de Microsoft
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: scale-out
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: 1
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: ec785459e5f9585776d83cde3f460c1e79367e46
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="change-the-account-for-scale-out-logging"></a>Cambiar la cuenta para el registro horizontalmente
Al ejecutar paquetes en horizontalmente, los mensajes de eventos se registran en SSISDB con un usuario creado automáticamente **MS_SSISLogDBWorkerAgentLogin ##**. El inicio de sesión de este usuario utiliza autenticación de SQL Server. Para cambiar la cuenta, sigue los pasos siguientes:

## <a name="1-create-a-user-of-ssisdb"></a>1. Crear un usuario de SSISDB
Para obtener instrucciones de creación de un usuario de base de datos, vea [crear un usuario de base de datos](../../relational-databases/security/authentication-access/create-a-database-user.md).

## <a name="2-add-the-user-to-database-role-ssisclusterworker"></a>2. Agregue el usuario ssis_cluster_worker de rol de base de datos

Para obtener instrucciones de unirse a un rol de base de datos, vea [combinar un rol](../../relational-databases/security/authentication-access/join-a-role.md).

## <a name="3-update-logging-information-in-ssisdb"></a>3. Información de registro de actualización de SSISDB
Llame al procedimiento almacenado [catalog]. [update_logdb_info] con la cadena de conexión y nombre de Sql Server como parámetros.

#### <a name="example"></a>Ejemplo
```sql
SET @serverName = CONVERT(sysname, SERVERPROPERTY('servername'))
SET @connectionString = 'Data Source=' + @serverName + ';Initial Catalog=SSISDB;Integrated Security=SSPI;'
EXEC [internal].[update_logdb_info] @serverName, @connectionString
GO
```

## <a name="4-restart-scale-out-worker-service"></a>4. Reiniciar servicio escala Out Worker

> [!NOTE]
> Si usa una cuenta de usuario de Windows para el registro, debe ser la misma cuenta que ejecuta el servicio de escala Out trabajo. En caso contrario, se producirá un error en el inicio de sesión de SQL Server.

