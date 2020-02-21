---
title: Delete an Operator
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, operators
- canceling operators
- removing operators
- deleting operators
- dropping operators
- jobs [SQL Server Agent], operators
- operators (users) [Database Engine], deleting with Management Studio
ms.assetid: 2b7b8627-082d-4189-8584-abd3a9b604cf
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 8b7f2b056e4fa634f338d3165391af8a3d958c3a
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "75242491"
---
# <a name="delete-an-operator"></a>Delete an Operator
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> En [Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), la mayoría de las características de agente SQL Server son compatibles actualmente, aunque no todas. Vea [Diferencias de T-SQL en Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para obtener más información.

En este tema se describe cómo quitar un operador para que deje de recibir notificaciones de alerta del Agente [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
## <a name="BeforeYouBegin"></a>Antes de empezar  
  
### <a name="Restrictions"></a>Limitaciones y restricciones 
Cuando se quita un operador, se quitan también todas las notificaciones asociadas con él.  
  
### <a name="Security"></a>Seguridad  
  
#### <a name="Permissions"></a>Permisos  
Los miembros del rol fijo de servidor **sysadmin** pueden eliminar operadores.  
  
## <a name="SSMSProcedure"></a>Usar SQL Server Management Studio  
  
#### <a name="to-delete-an-operator"></a>Para eliminar un operador  
  
1.  En el **Explorador de objetos**, haga clic en el signo más para expandir el servidor que contiene el operador que desea eliminar.  
  
2.  Haga clic en el signo más para expandir **Agente SQL Server**.  
  
3.  Haga clic en el signo más para expandir la carpeta **Operadores** .  
  
4.  Haga clic con el botón derecho en el operador que desea eliminar y seleccione **Eliminar**.  
  
5.  En el cuadro de diálogo **Eliminar objeto** , asegúrese de que está seleccionado el operador correcto y haga clic en **Aceptar**. Para que otro operador reciba las alertas y trabajos enviados al operador eliminado, active **Volver a asignar a** y seleccione un operador de la lista.  
  
## <a name="TsqlProcedure"></a>Usar Transact-SQL  
  
#### <a name="to-delete-an-operator"></a>Para eliminar un operador  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    -- deletes operator 'Test Operator' and reassigns all alerts and jobs
    --  sent to that operator to 'François Ajenstat'  
    USE msdb ;  
    GO  
  
    EXEC sp_delete_operator @name = 'Test Operator',  
        @reassign_to_operator = 'François Ajenstat';  
    GO  
    ```  
  
Para más información, consulte [sp_delete_operator (Transact-SQL)](https://msdn.microsoft.com/ff6c2c4b-e9fe-4d0c-bbc2-a2ddcc1acb95).  
  
