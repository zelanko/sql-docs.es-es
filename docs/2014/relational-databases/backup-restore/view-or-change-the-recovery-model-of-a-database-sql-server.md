---
title: Ver o cambiar el modelo de recuperación de una base de datos (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- database backups [SQL Server], recovery models
- recovery [SQL Server], recovery model
- backing up databases [SQL Server], recovery models
- recovery models [SQL Server], switching
- recovery models [SQL Server], viewing
- database restores [SQL Server], recovery models
- modifying database recovery models
ms.assetid: 94918d1d-7c10-4be7-bf9f-27e00b003a0f
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 4bc7254d8a3eafa3c7c7d152d323051a3c5bea94
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62875080"
---
# <a name="view-or-change-the-recovery-model-of-a-database-sql-server"></a>Ver o cambiar el modelo de recuperación de una base de datos (SQL Server)
  En este tema se describe cómo ver o cambiar el modelo de recuperación de una base de datos en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Un *modelo de recuperación* es una propiedad de base de datos que controla la forma en que se registran las transacciones, si el registro de transacciones requiere que se realice la copia de seguridad y si lo permite, y qué tipos de operaciones de restauración hay disponibles. Existen tres modelos de recuperación: simple, completa y por medio de registros de operaciones masivas. Normalmente, en las bases de datos se usa el modelo de recuperación completa o el modelo de recuperación simple. El modelo de recuperación de las bases de datos se puede cambiar en cualquier momento. La base de datos **modelo** establece el modelo de recuperación predeterminado de nuevas bases de datos.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Recomendaciones](#Recommendations)  
  
     [Seguridad](#Security)  
  
-   **Para ver o cambiar el modelo de recuperación de una base de datos, utilizando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Recomendaciones de seguimiento:**  [Después de cambiar el modelo de recuperación](#FollowUp)  
  
-   [Tareas relacionadas](#RelatedTasks)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Recommendations"></a> Recomendaciones  
  
-   Antes de cambiar del modelo de recuperación completa o del modelo de recuperación optimizado para cargas masivas de registros, haga copia de seguridad del registro de transacciones.  
  
-   La recuperación a un momento dado no es posible con el modelo optimizado para cargas masivas de registros. Por tanto, si ejecuta transacciones bajo el modelo de recuperación optimizado para cargas masivas de registros que requieran una restauración del registro de transacciones, estas transacciones podrían estar expuestas a la pérdida de datos. Para aumentar la capacidad de recuperación de datos en un escenario de recuperación ante desastres, se recomienda cambiar al modelo de recuperación optimizado para cargas masivas de registros solo en las siguientes condiciones:  
  
    -   Los usuarios no están permitidos en la base de datos.  
  
    -   Todas las modificaciones realizadas durante el proceso masivo son recuperables sin depender de una copia de seguridad de registros; por ejemplo, ejecutando de nuevo los procesos masivos.  
  
     Si satisface ambas condiciones, no se verá expuesto a ninguna pérdida de datos cuando restaure un registro de transacciones a partir de una copia de seguridad bajo el modelo de recuperación optimizado para cargas masivas de registros.  
  
> [!NOTE]  
>  Si cambia al modelo de recuperación completa durante una operación masiva, el registro de la operación masiva se modifica del registro mínimo al registro completo y viceversa.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Requiere el permiso ALTER en la base de datos.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-view-or-change-the-recovery-model"></a>Para ver o cambiar el modelo de recuperación  
  
1.  Después de conectarse a la instancia apropiada de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], en el Explorador de objetos, haga clic en el nombre del servidor para expandir el árbol de servidores.  
  
2.  Expanda **Bases de datos**y, en función de la base de datos, seleccione la base de datos de un usuario o expanda **Bases de datos del sistema** y seleccione una base de datos del sistema.  
  
3.  Haga clic con el botón derecho en la base de datos y haga clic en **Propiedades**, lo que abre el cuadro de diálogo **Propiedades de la base de datos** .  
  
4.  En el panel **Seleccionar una página** , haga clic en **Opciones**.  
  
5.  El modelo de recuperación actual se muestra en el cuadro de lista **Modelo de recuperación** .  
  
6.  Si lo desea, también puede seleccionar otra lista de modelos para cambiar el modelo de recuperación. Las opciones son **Completa**, **Registro masivo**o **Simple**.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-view-the-recovery-model"></a>Para ver el modelo de recuperación  
  
1.  Conéctese con el [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. Este ejemplo muestra cómo consultar la vista de catálogo [sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) para obtener información sobre el modelo de recuperación de la base de datos **modelo** .  
  
```sql  
SELECT name, recovery_model_desc  
   FROM sys.databases  
      WHERE name = 'model' ;  
GO  
  
```  
  
#### <a name="to-change-the-recovery-model"></a>Para cambiar el modelo de recuperación  
  
1.  Conéctese al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. En este ejemplo se muestra cómo cambiar el modelo de recuperación de la base de datos `model` a `FULL` utilizando la opción `SET RECOVERY` de la instrucción de [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql-set-options) .  
  
```sql  
USE master ;  
ALTER DATABASE model SET RECOVERY FULL ;  
```  
  
##  <a name="FollowUp"></a> Recomendaciones de seguimiento: Después de cambiar el modelo de recuperación  
  
-   **Después de cambiar entre el modelo de recuperación completa y el modelo de recuperación optimizado para cargas masivas de registros**  
  
    -   Después de haber completado las operaciones masivas, vuelva a cambiar inmediatamente al modelo de recuperación completa.  
  
    -   Después de cambiar del modelo de recuperación optimizado para cargas masivas de registros al modelo de recuperación completa, realice una copia de seguridad del registro.  
  
        > [!NOTE]  
        >  La estrategia de copia de seguridad sigue siendo la misma: siga realizando las copias de seguridad periódicas de la base de datos, del registro y diferenciales.  
  
-   **Después de cambiar desde el modelo de recuperación simple**  
  
    -   Inmediatamente después de cambiar al modelo de recuperación completa o al optimizado para cargas masivas de registros, realice una copia de seguridad de la base de datos completa o diferencial para iniciar la cadena de registros.  
  
        > [!NOTE]  
        >  El cambio al modelo de recuperación completa o al modelo de recuperación optimizado para cargas masivas de registros solo surte efecto después de la primera copia de seguridad de base de datos.  
  
    -   Programe periódicamente copias de seguridad de registros y actualice el plan de restauración en consecuencia.  
  
        > [!IMPORTANT]  
        >  Si no realiza la copia de seguridad con la frecuencia suficiente, el registro de transacciones se puede expandir hasta quedarse sin espacio en disco.  
  
-   **Tras cambiar al modelo de recuperación simple**  
  
    -   Interrumpa cualquier trabajo programado para realizar copia de seguridad del registro de transacciones.  
  
    -   Asegúrese de que estén programadas copias de seguridad periódicas de la base de datos. Es esencial hacer copia de seguridad de la base de datos para proteger los datos y para truncar la parte inactiva del registro de transacciones.  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
  
-   [Crear una copia de seguridad completa de base de datos &#40;SQL Server&#41;](create-a-full-database-backup-sql-server.md)  
  
-   [Realizar una copia de seguridad de un registro de transacciones &#40;SQL Server&#41;](back-up-a-transaction-log-sql-server.md)  
  
-   [Crear un trabajo](../../ssms/agent/create-a-job.md)  
  
-   [Deshabilitar o habilitar un trabajo](../../ssms/agent/disable-or-enable-a-job.md)  
  
##  <a name="RelatedContent"></a> Contenido relacionado  
  
-   [Planes de mantenimiento de bases de datos](../maintenance-plans/maintenance-plans.md) (en los Libros en pantalla de [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] )  
  
## <a name="see-also"></a>Vea también  
 [Modelos de recuperación &#40;SQL Server&#41;](recovery-models-sql-server.md)   
 [El registro de transacciones &#40;SQL Server&#41;](../logs/the-transaction-log-sql-server.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)   
 [Modelos de recuperación &#40;SQL Server&#41;](recovery-models-sql-server.md)  
  
  
