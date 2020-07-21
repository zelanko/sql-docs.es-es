---
title: Permisos necesarios para ejecutar SQL Server Profiler | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- Profiler [SQL Server Profiler], permissions
- traces [SQL Server], replaying
- replaying traces
- SQL Server Profiler, permissions
- security [SQL Server], SQL Server Profiler
ms.assetid: 5c580a87-88ae-4314-8fe1-54ade83f227f
author: stevestein
ms.author: sstein
ms.openlocfilehash: e73ffe2e127299db9a9e37e48f089aab2cccca52
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85054356"
---
# <a name="permissions-required-to-run-sql-server-profiler"></a>Permisos necesarios para ejecutar SQL Server Profiler
  De forma predeterminada, la ejecución del [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] requiere los mismos permisos de usuario que los procedimientos almacenados de Transact-SQL que se utilizan para crear seguimientos. Para ejecutar [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)], debe concederse a los usuarios el permiso ALTER TRACE. Para obtener más información, vea [GRANT &#40;permisos de servidor de Transact-SQL&#41;](/sql/t-sql/statements/grant-server-permissions-transact-sql).

> [!IMPORTANT]
>  Los usuarios que tienen el permiso SHOWPLAN, ALTER TRACE o VIEW SERVER STATE pueden ver consultas capturadas en la salida del plan de presentación. Estas consultas pueden contener información confidencial, como contraseñas. Por consiguiente, se recomienda conceder estos permisos solo a los usuarios que tengan autorización para ver información confidencial, como los miembros del rol fijo de base de datos db_owner o los miembros del rol fijo de servidor sysadmin. Además, se recomienda guardar solo los archivos del plan de presentación o los archivos de seguimiento que contengan eventos relacionados con el plan de presentación en una ubicación que utilice el sistema de archivos NTFS, así como restringir el acceso a los usuarios que tengan autorización para ver información confidencial.

## <a name="permissions-used-to-replay-traces"></a>Permisos utilizados para reproducir seguimientos
 La reproducción de seguimientos también requiere que el usuario que reproduce el seguimiento disponga del permiso ALTER TRACE.

 Sin embargo, durante la reproducción, [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] utiliza el comando EXECUTE AS si se encuentra un evento Audit Login en el seguimiento que se está reproduciendo. [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] utiliza el comando EXECUTE AS para suplantar al usuario asociado al evento de inicio de sesión.

 Si el [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] encuentra un evento de inicio de sesión en un seguimiento que se está reproduciendo, se realizan las siguientes comprobaciones de permisos:

1.  El usuario 1, que tiene el permiso ALTER TRACE, comienza a reproducir una seguimiento.

2.  Se encuentra un evento de inicio de sesión para el usuario 2 en la seguimiento reproducida.

3.  [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] utiliza el comando EXECUTE AS para suplantar al usuario 2.

4.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] intenta autenticar al usuario 2 y, en función del resultado, tiene lugar una de las siguientes acciones:

    1.  Si el usuario 2 no se puede autenticar, el [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] devuelve un error y continúa reproduciendo la seguimiento como usuario 1.

    2.  Si el usuario 2 se autentica correctamente, la reproducción de la seguimiento como usuario 2 continúa.

5.  Los permisos del usuario 2 se comprueban en la base de datos de destino y, en función del resultado, tiene lugar una de las siguientes acciones:

    1.  Si el usuario 2 tiene permisos en la base de datos de destino, la suplantación ha tenido éxito y la seguimiento se reproduce como usuario 2.

    2.  Si el usuario 2 no tiene permisos en la base de datos de destino, el servidor busca un usuario Invitado en esa base de datos.

6.  Se comprueba la existencia de un usuario Invitado en la base de datos de destino y, en función del resultado, tiene lugar una de las siguientes acciones:

    1.  Si existe una cuenta Invitado, la seguimiento se reproduce como la cuenta Invitado.

    2.  Si no existe una cuenta Invitado en la base de datos de destino, se devuelve un error y la seguimiento se reproduce como el usuario 1.

 En el siguiente diagrama se muestra el proceso de comprobación de permisos al reproducir seguimientos:

 ![Permisos de seguimiento de reproducción de SQL Server Profiler](../../database-engine/media/replaytracedecisiontree.gif "Permisos de seguimiento de reproducción de SQL Server Profiler")

## <a name="see-also"></a>Consulte también
 [SQL Server Profiler procedimientos almacenados &#40;los seguimientos de la reproducción de&#41;de Transact-SQL](/sql/relational-databases/system-stored-procedures/sql-server-profiler-stored-procedures-transact-sql) [Replay Traces](replay-traces.md) [crean un seguimiento &#40;SQL Server Profiler](create-a-trace-sql-server-profiler.md)&#41;[reproducir una tabla de seguimiento](replay-a-trace-table-sql-server-profiler.md) &#40;SQL Server Profiler&#41;[reproducir un archivo de seguimiento &#40;](replay-a-trace-file-sql-server-profiler.md) SQL Server Profiler&#41;


