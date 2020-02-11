---
title: Administración de la tabla suspect_pages (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- 824 (Database Engine error)
- restoring pages [SQL Server]
- pages [SQL Server], suspect
- pages [SQL Server], restoring
- suspect_pages system table
- suspect pages [SQL Server]
- restoring [SQL Server], pages
ms.assetid: f394d4bc-1518-4e61-97fc-bf184d972e2b
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 0f6c6afc1822e2f56189aace2836a15486d1b73b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62922023"
---
# <a name="manage-the-suspect_pages-table-sql-server"></a>Administrar la tabla suspect_pages (SQL Server)
  En este tema se describe cómo administrar la tabla **suspect_pages** en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] por medio de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. La tabla **suspect_pages** sirve para conservar información sobre las páginas sospechosas y es de gran utilidad para decidir si es necesaria una restauración. La tabla [suspect_pages](/sql/relational-databases/system-tables/suspect-pages-transact-sql) reside en la [base de datos msdb](../databases/msdb-database.md).  
  
 Una página se considera "sospechosa" cuando [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)] encuentra uno de los errores siguientes al intentar leer una página de datos:  
  
-   Un [error 823](../errors-events/mssqlserver-823-database-engine-error.md) producido por una comprobación de redundancia cíclica (CRC) emitido por el sistema operativo, como un error de disco (ciertos errores de hardware)  
  
-   Un [error 824](../errors-events/mssqlserver-824-database-engine-error.md), como una página rasgada (cualquier error lógico)  
  
 El identificador de página de cada página sospechosa se registra en la tabla **suspect_pages** . [!INCLUDE[ssDE](../../includes/ssde-md.md)] registra todas las páginas sospechosas que encuentra durante el procesamiento normal, como en estos casos:  
  
-   Una consulta tiene que leer una página.  
  
-   Durante una operación DBCC CHECKDB.  
  
-   Durante una operación de copia de seguridad.  
  
 La tabla **suspect_pages** también se actualiza cuando es necesario durante una operación de restauración, una operación de reparación de DBCC o una operación de quitar la base de datos.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Recomendaciones](#Recommendations)  
  
     [Seguridad](#Security)  
  
-   **Para administrar la tabla suspect_pages, utilizando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Recommendations"></a> Recomendaciones  
  
-   **Errores registrados en la tabla suspect_pages**  
  
     La tabla **suspect_pages** contiene una fila por cada página que causó un error 824, hasta un límite de 1000 filas. En la siguiente tabla se muestran los errores registrados en la columna **event_type** de la tabla **suspect_pages** .  
  
    |Descripción del error|Valor**event_type**|  
    |-----------------------|---------------------------|  
    |Error 823 producido por un error de CRC del sistema operativo, o error 824 que no sea una suma de comprobación no válida o una página rasgada (por ejemplo, un Id. de página no válido)|1|  
    |Suma de comprobación errónea|2|  
    |Página rasgada|3|  
    |Restaurada (la página se restauró después de marcarse como errónea)|4|  
    |Reparada (DBCC, AlwaysOn o la creación de reflejos han reparado la página).|5|  
    |Desasignada por DBCC|7|  
  
     En la tabla **suspect_pages** también se registran errores transitorios. El origen de los errores transitorios puede ser un error de E/S (por ejemplo, un cable desconectado) o una página que genera un error temporal en una prueba de suma de comprobación repetida.  
  
-   **Cómo actualiza el motor de base de datos la tabla suspect_pages**  
  
     El [!INCLUDE[ssDE](../../includes/ssde-md.md)] realiza las siguientes acciones en la tabla **suspect_pages** :  
  
    -   Si la tabla no está llena, se actualiza para cada error 824, para indicar que se ha producido un error, y el contador de errores se incrementa. Si una página tiene un error después de ser corregida mediante reparación, restauración o desasignación, su contador **number_of_errors** se incrementa y la columna **last_update** se actualiza.  
  
    -   Después de corregir una página de la lista con una operación de restauración o de reparación, la operación actualiza la fila **suspect_pages** para indicar que la página está reparada (**event_type** = 5) o restaurada (**event_type** = 4).  
  
    -   Si se ejecuta una comprobación DBCC, esta marca las páginas sin errores como reparadas (**event_type** = 5) o desasignadas (**event_type** = 7).  
  
-   **Actualizaciones automáticas de la tabla suspect_pages**  
  
     Un asociado de creación de reflejo de la base de datos o réplica de disponibilidad AlwaysOn actualiza la tabla **suspect_pages** después de un error en un intento de leer una página de un archivo de datos por una de las razones siguientes.  
  
    -   Error 823 error producido por un error de CRC del sistema operativo  
  
    -   Error 824, (error lógico, como una página rasgada)  
  
     Las siguientes acciones también actualizan automáticamente las filas de la tabla **suspect_pages** .  
  
    -   DBCC CHECKDB REPAIR_ALLOW_DATA_LOSS actualiza la tabla **suspect_pages** para indicar cada página que se ha reparado o desasignado.  
  
    -   Una operación de restauración RESTORE completa, de archivos o de páginas marca las entradas de página como restauradas.  
  
     Las siguientes acciones eliminan automáticamente filas de la tabla **suspect_pages** .  
  
    -   ALTER DATABASE REMOVE FILE  
  
    -   DROP DATABASE  
  
-   **Rol de mantenimiento del administrador de la base de datos**  
  
     Los administradores de bases de datos son responsables de la administración de la tabla, sobre todo de eliminar las filas antiguas. La tabla **suspect_pages** tiene un tamaño limitado; si se llena, los errores nuevos no se registrarán. Para evitar que esta tabla se llene, el administrador de la base de datos o el administrador del sistema debe borrar manualmente las entradas antiguas de la tabla eliminando filas. Por tanto, recomendamos que elimine o archive periódicamente las filas cuyo **event_type** se ha restaurado o reparado o las filas que tengan un valor **last_update** antiguo.  
  
     Para supervisar la actividad en la tabla suspect_pages, puede usar la clase de eventos [Database Suspect Data Page](../event-classes/database-suspect-data-page-event-class.md). A veces, se agregan filas a la tabla **suspect_pages** debido a errores transitorios. Si se agregan muchas filas a la tabla, sin embargo, es probable que haya un problema con el subsistema de E/S. Si observa un aumento repentino en el número de filas que se agregan a la tabla, recomendamos que investigue los posibles problemas en el subsistema de E/S.  
  
     Un administrador de la base de datos también puede insertar o actualizar registros. Por ejemplo, actualizar una fila puede resultar útil cuando el administrador de la base de datos sabe que una determinada página sospechosa está intacta realmente, pero desea preservar el registro durante un tiempo.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Cualquier persona con acceso a **msdb** puede leer los datos de la tabla **suspect_pages** . Cualquier persona con el permiso UPDATE en la tabla suspect_pages puede actualizar sus registros. Los miembros del rol fijo de base de datos **db_owner** de **msdb** o el rol fijo de servidor **sysadmin** pueden insertar, actualizar y eliminar registros.  
  
##  <a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
  
#### <a name="to-manage-the-suspect_pages-table"></a>Para administrar la tabla suspect_pages  
  
1.  En el **Explorador de objetos**, conéctese a una instancia de [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)], expándala y, a continuación, expanda **Bases de datos**.  
  
2.  Expanda **Bases de datos del sistema**, expanda **msdb**, expanda **Tablas**y, por último, expanda **Tablas del sistema**.  
  
3.  Expanda **dbo.suspect_pages** y haga clic con el botón derecho en **Editar las 200 primeras filas**.  
  
4.  En la ventana de consulta, edite, actualice o elimine las filas que desee.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-manage-the-suspect_pages-table"></a>Para administrar la tabla suspect_pages  
  
1.  Conéctese con el [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue los ejemplos siguientes en la ventana de consulta y haga clic en **Ejecutar**. En este ejemplo se eliminan algunas filas de la tabla `suspect_pages` .  
  
```  
-- Delete restored, repaired, or deallocated pages.  
DELETE FROM msdb..suspect_pages  
   WHERE (event_type = 4 OR event_type = 5 OR event_type = 7);  
GO  
  
```  
  
 E este ejemplo se devuelve las páginas no válidas de la tabla `suspect_pages` .  
  
```  
-- Select nonspecific 824, bad checksum, and torn page errors.  
SELECT * FROM msdb..suspect_pages  
   WHERE (event_type = 1 OR event_type = 2 OR event_type = 3);  
GO  
  
```  
  
## <a name="see-also"></a>Consulte también  
 [DROP DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-database-audit-specification-transact-sql)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [DBCC &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-transact-sql)   
 [Restaurar páginas &#40;SQL Server&#41;](restore-pages-sql-server.md)   
 [suspect_pages &#40;&#41;de Transact-SQL](/sql/relational-databases/system-tables/suspect-pages-transact-sql)   
 [MSSQLSERVER_823](../errors-events/mssqlserver-823-database-engine-error.md)   
 [MSSQLSERVER_824](../errors-events/mssqlserver-824-database-engine-error.md)  
  
  
