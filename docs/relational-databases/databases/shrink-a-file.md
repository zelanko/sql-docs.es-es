---
title: "Reducir un archivo | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.swb.shrinkfile.f1"
helpviewer_keywords: 
  - "reducir archivos"
  - "disminuir tamaño de archivo"
  - "bases de datos [SQL Server], reducir"
  - "reducir tamaño de archivo"
  - "tamaño [SQL Server], archivos"
  - "tamaño de archivo [SQL Server]"
ms.assetid: ce5c8798-c039-4ab2-81e7-90a8d688b893
caps.latest.revision: 25
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 25
---
# Reducir un archivo
  En este tema se describe cómo reducir un archivo de datos o de registro en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 La reducción de los archivos de datos permite recuperar espacio moviendo páginas de datos del final del archivo a espacio desocupado próximo al principio del archivo. Cuando se crea suficiente espacio disponible al final del archivo, las páginas de datos situadas al final del mismo se pueden desasignar y devolver al sistema de archivos.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Recomendaciones](#Recommendations)  
  
     [Seguridad](#Security)  
  
-   **Para reducir un archivo de datos o de registro, use:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   El archivo de datos principal no puede reducirse a un tamaño menor que el del archivo principal de la base de datos model.  
  
###  <a name="Recommendations"></a> Recomendaciones  
  
-   Los datos que se mueven para reducir un archivo se pueden dispersar en cualquier ubicación disponible en el archivo. Esto produce la fragmentación de índices y puede reducir el rendimiento de las consultas que buscan un intervalo del índice. Para eliminar la fragmentación, considere la posibilidad de volver a generar los índices en el archivo después de la reducción.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Debe pertenecer al rol fijo de servidor **sysadmin** o al rol fijo de base de datos **db_owner**.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### Para reducir un archivo de datos o de registro  
  
1.  En el Explorador de objetos, conéctese a una instancia del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] y expándala.  
  
2.  Expanda **Bases de datos** y, después, haga clic con el botón derecho en la base de datos que quiera reducir.  
  
3.  Seleccione **Tareas**y **Reducir**y haga clic en **Archivos**.  
  
     **Base de datos**  
     Muestra el nombre de la base de datos seleccionada.  
  
     **Tipo de archivo**  
     Seleccione el tipo de archivo. Las opciones disponibles son **Datos** y **Registro** . El valor predeterminado es **Datos**. Si se selecciona un tipo de grupo de archivos diferente, la selección de los demás campos también cambia.  
  
     **Grupo de archivos**  
     Seleccione un grupo de archivos en la lista de grupos de archivos asociados al **Tipo de archivo** seleccionado anteriormente. Si se selecciona un grupo de archivos diferente, la selección de los demás campos también cambia.  
  
     **Nombre de archivo**  
     Elija un archivo en la lista de archivos disponibles del grupo de archivos y del tipo de archivo seleccionados.  
  
     **Ubicación**  
     Muestra la ruta de acceso completa al archivo seleccionado. La ruta no se puede editar, pero se puede copiar al Portapapeles.  
  
     **Espacio asignado actualmente**  
     Para los archivos de datos, muestra el espacio asignado actualmente. En los archivos de registro, muestra el espacio asignado, calculado a partir del resultado de DBCC SQLPERF(LOGSPACE).  
  
     **Espacio disponible**  
     En los archivos de datos, muestra el espacio disponible, calculado a partir del resultado de DBCC SHOWFILESTATS(fileid). En los archivos de registro, muestra el espacio disponible, calculado a partir del resultado de DBCC SQLPERF(LOGSPACE).  
  
     **Liberar espacio no utilizado**  
     Hace que se libere el espacio no utilizado de los archivos para el sistema operativo y reduce el archivo a la última extensión asignada, lo que disminuye el tamaño del archivo sin mover los datos. No se realiza ningún intento de reubicación de las filas en páginas no asignadas.  
  
     **Reorganizar páginas antes de liberar espacio no utilizado**  
     Equivale a ejecutar DBCC SHRINKFILE con la especificación del tamaño del archivo de destino. Si se selecciona esta opción, el usuario debe especificar el tamaño del archivo de destino en el cuadro **Reducir el archivo a** .  
  
     **Reducir el archivo a**  
     Especifica el tamaño del archivo de destino para la operación de reducción. El tamaño no puede ser inferior al espacio asignado actual ni superior a la extensión total asignada al archivo. Si se introduce un valor inferior al mínimo o superior al máximo, se restablecerá el valor mínimo o máximo cuando cambie el foco o cuando se haga clic en los botones de la barra de herramientas.  
  
     **Vaciar el archivo migrando los datos a otros archivos del mismo grupo de archivos**  
     Migra todos los datos del archivo especificado. Esta opción permite que el archivo se pueda quitar mediante la instrucción ALTER DATABASE. Esta opción equivale a ejecutar DBCC SHRINKFILE con la opción EMPTYFILE.  
  
4.  Seleccione el tipo y el nombre del archivo.  
  
5.  También puede activar la casilla **Liberar espacio no utilizado** .  
  
     Si activa esta opción, el espacio no utilizado del archivo se libera al sistema operativo y el archivo se reduce a la última extensión asignada. De esta forma, se reduce el tamaño del archivo sin necesidad de mover datos.  
  
6.  También puede seleccionar la casilla **Reorganizar archivos antes de liberar espacio no utilizado** . Si activa esta opción, debe especificar el valor **Reducir el archivo a** . De forma predeterminada, esta opción no está activada.  
  
     Si activa esta opción, el espacio no utilizado del archivo se libera al sistema operativo y se intentan reubicar las filas en páginas no asignadas.  
  
7.  De manera opcional, especifique el porcentaje máximo de espacio disponible que desee dejar en el archivo de la base de datos después de reducirla. Los valores válidos están comprendidos entre 0 y 99. Esta opción solo está disponible cuando la opción **Reorganizar archivos antes de liberar espacio no utilizado** está habilitada.  
  
8.  De manera opcional, active la casilla **Vaciar el archivo migrando los datos a otros archivos del mismo grupo de archivos** .  
  
     Si activa esta opción, los datos se mueven del archivo especificado a otros archivos del grupo de archivos. A continuación, el archivo vacío puede eliminarse. Esta opción equivale a ejecutar DBCC SHRINKFILE con la opción EMPTYFILE.  
  
9. Haga clic en **Aceptar**.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### Para reducir un archivo de datos o de registro  
  
1.  Conéctese con el [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. Este ejemplo usa [DBCC SHRINKFILE](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md) para reducir a 7 MB el tamaño de un archivo de datos denominado `DataFile1` de la base de datos `UserDB` .  
  
 [!code-sql[DBCC#DBCC_SHRINKFILE1](../../relational-databases/databases/codesnippet/tsql/shrink-a-file_1.sql)]  
  
## Vea también  
 [DBCC SHRINKDATABASE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md)   
 [Reducir una base de datos](../../relational-databases/databases/shrink-a-database.md)   
 [Eliminar archivos de datos o de registro de una base de datos](../../relational-databases/databases/delete-data-or-log-files-from-a-database.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)  
  
  