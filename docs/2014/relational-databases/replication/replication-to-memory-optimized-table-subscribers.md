---
title: Replicación en suscriptores de tablas con optimización para memoria | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
ms.assetid: 1a8e6bc7-433e-471d-b646-092dc80a2d1a
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b9f58e472b0b6e6d164e45c2d1136c81bc4a46d6
ms.sourcegitcommit: 495913aff230b504acd7477a1a07488338e779c6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2019
ms.locfileid: "68811228"
---
# <a name="replication-to-memory-optimized-table-subscribers"></a>Replicación en suscriptores de tablas con optimización para memoria
  Las tablas que actúan como suscriptores de replicación transaccional, excluida la replicación transaccional punto a punto, pueden configurarse como tablas optimizadas para memoria. Otras configuraciones de replicación no son compatibles con las tablas optimizadas para memoria.  
  
## <a name="configuring-a-memory-optimized-table-as-a-subscriber"></a>Configurar una tabla optimizada para memoria como suscriptor  
 Para configurar una tabla optimizada para memoria como suscriptor, realice los pasos siguientes.  
  
 **Crear y habilitar publicación**  
  
1.  Crear una publicación.  
  
2.  Agregue artículos a la publicación. Para el parámetro `@upd_cmd`, use la convención SCALL o SQL.  
  
    ```  
    EXEC sp_addarticle  
        @publication = N'Publication1',  
        @article = N'Mem_Table',  
        @source_owner = N'dbo',  
        @source_object = N'Mem_Table',  
        @type = N'logbased',  
        @description = null,  
        @creation_script = null,  
        @pre_creation_cmd = N'none',  
        @schema_option = 0x00000000080050DF,  
        @identityrangemanagementoption = N'manual',  
        @destination_table = N'Mem_Table',  
        @destination_owner = N'dbo',  
        @vertical_partition = N'false',  
        @ins_cmd = N'CALL sp_MSins_Mem_Table',  
        @del_cmd = N'CALL sp_MSdel_Mem_Table',  
        @upd_cmd = N'SCALL sp_MSupd_Mem_Table';  
    GO  
    ```  
  
 **Generar una instantánea y ajustar el esquema**  
  
1.  Cree un trabajo de instantánea y genere una instantánea.  
  
    ```  
    EXEC sp_addpublication_snapshot @publication = N'Publication1', @frequency_type = 1;  
    EXEC sp_startpublication_snapshot @publication = N'Publication1';  
    ```  
  
2.  Navegue hasta la carpeta de la instantánea. La ubicación predeterminada es "C:\Archivos de Programa\microsoft SQL Server\MSSQL12. Instancia > \MSSQL\repldata\unc\XXX\YYYYMMDDHHMMSS\\". \<  
  
3.  Busque el **. SCH** en la tabla y ábralo en Management Studio. Cambie el esquema de tabla y actualice el procedimiento almacenado como se describe a continuación.  
  
     Evalúe los índices definidos en el archivo IDX. Modifique `CREATE TABLE` para especificar los índices, las restricciones, la clave principal y la sintaxis optimizada para memoria necesarios. Para las tablas optimizadas para memoria, las columnas de índice deben ser NOT NULL y las columnas de índice de tipos de caracteres deben ser Unicode y usar la intercalación BIN2. Vea el ejemplo siguiente:  
  
    ```  
    SET ANSI_PADDING ON;  
    GO  
  
    SET ANSI_NULLS ON;  
    GO  
  
    SET QUOTED_IDENTIFIER ON;  
    GO  
  
    CREATE TABLE [dbo].[Mem_Table]([c1] [int] NOT NULL,  
        [c2] [float] NOT NULL,  
        [c3] [decimal](10, 2) NOT NULL,  
        [c4] [nvarchar](5) COLLATE SQL_Latin1_General_CP850_BIN2 NOT NULL,  
        INDEX [hash_index_sample_memoryoptimizedtable_c2] HASH (c2) WITH (BUCKET_COUNT = 1024),  
        INDEX [index_sample_memoryoptimizedtable_c3] NONCLUSTERED ([c3]),  
        INDEX [nvarchar_index_sample_memoryoptimizedtable_c4] ([c4]),  
        CONSTRAINT [PK_sample_memoryoptimizedtable] PRIMARY KEY NONCLUSTERED ([c1])) WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA);  
    GO  
    ```  
  
4.  Cuando use la convención SCALL para el parámetro `@upd_cmd`, vaya al archivo de esquema (.SCH) y cambie la instrucción de actualización de tabla en `create procedure [sp_MSupd_<SCHEMA><TABLE_NAME>]` para quitar las columnas de clave principal.  
  
     Para admitir actualizaciones de la clave principal, use un procedimiento almacenado de actualización personalizado para reemplazar la instrucción de actualización de la clave principal de la manera siguiente:  
  
    1.  Seleccione los valores de columna ausentes (SCALL solo proporciona la columna implicada en la operación de actualización).  
  
    2.  Elimine el registro existente.  
  
    3.  Inserte un nuevo registro con los nuevos valores suministrados, incluida la nueva clave principal.  
  
     El procedimiento de actualización original es similar al siguiente:  
  
    ```  
    create procedure [sp_MSupd_Mem_Table]  
                   @c1 int = NULL,  
                   @c2 float = NULL,  
                   @c3 decimal(10,2) = NULL,  
                   @c4 nvarchar(5) = NULL,  
                   @pkc1 int = NULL,  
                   @bitmap binary(1)  
    as  
    begin    
    if (substring(@bitmap,1,1) & 1 = 1)  
    begin   
    update [dbo].[Mem_Table] set  
                   [c1] = case substring(@bitmap,1,1) & 1 when 1 then @c1 else [c1] end,  
                   [c2] = case substring(@bitmap,1,1) & 2 when 2 then @c2 else [c2] end,  
                   [c3] = case substring(@bitmap,1,1) & 4 when 4 then @c3 else [c3] end,  
                   [c4] = case substring(@bitmap,1,1) & 8 when 8 then @c4 else [c4] end  
    where [c1] = @pkc1  
    if @@rowcount = 0  
        if @@microsoftversion>0x07320000  
            exec sp_MSreplraiserror 20598  
    end    
    else  
    begin   
    update [dbo].[Mem_Table] set  
                   [c2] = case substring(@bitmap,1,1) & 2 when 2 then @c2 else [c2] end,  
                   [c3] = case substring(@bitmap,1,1) & 4 when 4 then @c3 else [c3] end,  
                   [c4] = case substring(@bitmap,1,1) & 8 when 8 then @c4 else [c4] end  
    where [c1] = @pkc1  
    if @@rowcount = 0  
        if @@microsoftversion>0x07320000  
            exec sp_MSreplraiserror 20598  
    end   
    end   
    go  
    ```  
  
     Si la clave principal nunca se debe actualizar en un publicador. Marque con comentarios la actualización de esas columnas en el procedimiento de actualización de la manera siguiente:  
  
    ```  
    create procedure [sp_MSupd_Mem_Table]  
                   @c1 int = NULL,  
                   @c2 float = NULL,  
                   @c3 decimal(10,2) = NULL,  
                   @c4 nvarchar(5) = NULL,  
                   @pkc1 int = NULL,  
                   @bitmap binary(1)  
    as  
    begin    
    if (substring(@bitmap,1,1) & 1 = 1)  
    begin   
    update [dbo].[Mem_Table] set  
    --             [c1] = case substring(@bitmap,1,1) & 1 when 1 then @c1 else [c1] end,  
                   [c2] = case substring(@bitmap,1,1) & 2 when 2 then @c2 else [c2] end,  
                   [c3] = case substring(@bitmap,1,1) & 4 when 4 then @c3 else [c3] end,  
                   [c4] = case substring(@bitmap,1,1) & 8 when 8 then @c4 else [c4] end  
    where [c1] = @pkc1  
    if @@rowcount = 0  
        if @@microsoftversion>0x07320000  
            exec sp_MSreplraiserror 20598  
    end    
    else  
    begin   
    update [dbo].[Mem_Table] set  
                   [c2] = case substring(@bitmap,1,1) & 2 when 2 then @c2 else [c2] end,  
                   [c3] = case substring(@bitmap,1,1) & 4 when 4 then @c3 else [c3] end,  
                   [c4] = case substring(@bitmap,1,1) & 8 when 8 then @c4 else [c4] end  
    where [c1] = @pkc1  
    if @@rowcount = 0  
        if @@microsoftversion>0x07320000  
            exec sp_MSreplraiserror 20598  
    end   
    end   
    go  
    ```  
  
     Para permitir actualizaciones a la clave principal, modifique el procedimiento de actualización de la manera siguiente:  
  
    ```  
    create procedure [sp_MSupd_Mem_Table]  
                   @c1 int = NULL,  
                   @c2 float = NULL,  
                   @c3 decimal(10,2) = NULL,  
                   @c4 nvarchar(5) = NULL,  
                    @pkc1 int = NULL,  
                   @bitmap binary(1)  
    as  
    begin    
    if (substring(@bitmap,1,1) & 1 = 1)  
    begin   
    select  
                   @c1 = case substring(@bitmap,1,1) & 1 when 1 then @c1 else [c1] end,  
                   @c2 = case substring(@bitmap,1,1) & 2 when 2 then @c2 else [c2] end,  
                   @c3 = case substring(@bitmap,1,1) & 4 when 4 then @c3 else [c3] end,  
                   @c4 = case substring(@bitmap,1,1) & 8 when 8 then @c4 else [c4] end  
    from [dbo].[Mem_Table] where [c1] = @pkc1  
    if @@rowcount <> 0 begin  
            delete [dbo].[Mem_Table] where [c1] = @pkc1  
            if @@rowcount <> 0  
                   insert into [dbo].[Mem_Table]([c1],  
                           [c2],  
                           [c3],  
                           [c4]) values (  
                           @c1,  
                           @c2,  
                           @c3,  
                           @c4  
                   )   
    end  
    if @@rowcount = 0  
        if @@microsoftversion>0x07320000  
            exec sp_MSreplraiserror 20598  
    end    
    else  
    begin   
    update [dbo].[Mem_Table] set  
                   [c2] = case substring(@bitmap,1,1) & 2 when 2 then @c2 else [c2] end,  
                   [c3] = case substring(@bitmap,1,1) & 4 when 4 then @c3 else [c3] end,  
                   [c4] = case substring(@bitmap,1,1) & 8 when 8 then @c4 else [c4] end  
    where [c1] = @pkc1  
    if @@rowcount = 0  
        if @@microsoftversion>0x07320000  
            exec sp_MSreplraiserror 20598  
    end   
    end   
    go  
    ```  
  
5.  Cree una base de datos de suscriptor con la opción de **aislamiento elevar a Snapshot** y establezca la intercalación predeterminada en Latin1_General_CS_AS_KS_WS en caso de que se utilicen tipos de datos de caracteres no Unicode.  
  
    ```  
    CREATE DATABASE [Sub]   
    CONTAINMENT = NONE   
    ON PRIMARY ( NAME = [Sub], FILENAME = [C:\Program Files\Microsoft SQL Server\MSSQL12\MSSQL\DATA\Sub.mdf]),   
    FILEGROUP [mem] CONTAINS MEMORY_OPTIMIZED_DATA ( NAME = [mem],   
    FILENAME = [C:\Program Files\Microsoft SQL Server\MSSQL12\MSSQL\DATA\Sub])  
    LOG ON ( NAME = [Sub_log], FILENAME = [C:\Program Files\Microsoft SQL Server\MSSQL12\MSSQL\DATA\Sub.ldf])  
    COLLATE Latin1_General_CS_AS_KS_WS;  
  
    ALTER DATABASE [Sub] SET MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT = ON;  
    GO  
    ```  
  
6.  Aplique el esquema a la base de datos de un suscriptor y guarde el esquema para su uso futuro.  
  
7.  Cargue los datos del publicador (origen) en el suscriptor. Los datos no deben cambiarse en el publicador hasta que no agregue una suscripción.  Puede usar BCP como se muestra a continuación:  
  
    ```  
    bcp Pub.dbo.Mem_Table out Mem_Table.bcp -S. -T -C1252 -n  
    bcp Sub.dbo.Mem_Table in Mem_Table.bcp -S. -T -C1252 -n  
    ```  
  
8.  Reconfigure el artículo para deshabilitar los cambios de esquema en el suscriptor:  
  
    ```  
    EXEC sp_changearticle  
        @publication = N'Publication1',  
        @article = N'Mem_Table',  
        @property = N'schema_option',  
        @value = 0,  
        @force_invalidate_snapshot = 1,  
        @force_reinit_subscription = 1;  
    GO  
    ```  
  
 **No agregar suscripción de sincronización**  
  
 Agregue una suscripción nosync.  
  
```  
EXEC sp_addsubscription  
    @publication = N' Publication1',  
    @subscriber = @@ServerName,  
    @destination_db = N'Sub',  
    @subscription_type = N'Push',  
    @sync_type = N'replication support only',  
    @article = N'all',  
    @update_mode = N'read only',  
    @subscriber_type = 0;  
GO  
```  
  
 Las tablas con optimización para memoria deben empezar ahora a recibir actualizaciones del publicador.  
  
## <a name="restrictions"></a>Restricciones  
 Solo se admite la replicación transaccional unidireccional. No se admite la replicación transaccional punto a punto.  
  
 Las tablas con optimización para memoria no se pueden publicar.  
  
 Las tablas de replicación del distribuidor no se pueden configurar como tablas optimizadas para memoria.  
  
 La replicación de mezcla no puede incluir tablas optimizadas para memoria.  
  
 En el suscriptor, las tablas implicadas en la replicación transaccional se pueden configurar como tablas optimizadas para memoria, pero las tablas del suscriptor deben cumplir los requisitos de las tablas optimizadas para memoria. Esto requiere las restricciones siguientes.  
  
-   Para crear una tabla optimizada para memoria en un suscriptor de replicación transaccional, los archivos de esquema de instantáneas usados para crear las tablas optimizadas para memoria se deben modificar manualmente. Para obtener más información, vea [modificar un archivo de esquema](#Schema).  
  
-   Las tablas replicadas en tablas optimizadas para memoria de un suscriptor tienen el límite de 8060 bytes por fila de las tablas optimizadas para memoria.  
  
-   Las tablas replicadas en tablas optimizadas para memoria de un suscriptor están limitadas a los tipos de datos permitidos en las tablas optimizadas para memoria. Para obtener más información, vea [tipos de datos admitidos](../in-memory-oltp/supported-data-types-for-in-memory-oltp.md).  
  
-   Hay ciertas restricciones para la actualización de la clave principal de tablas que se replican en una tabla optimizada para memoria en un suscriptor. Para obtener más información, vea [replicar cambios en una clave principal](#PrimaryKey).  
  
-   En las tablas optimizadas para memoria no se admiten claves externas, restricciones UNIQUE, desencadenadores, modificaciones de esquema, ROWGUIDCOL, columnas calculadas, compresión de datos, tipos de datos de alias, control de versiones ni bloqueos. Vea [Construcciones T-SQL no admitidas por OLTP en memoria](../in-memory-oltp/transact-sql-constructs-not-supported-by-in-memory-oltp.md) para obtener información.  
  
##  <a name="Schema"></a> Modificar un archivo de esquema  
  
-   No se admiten índices clúster. Cambie los índices clúster a los índices no clúster.  
  
-   Todas las columnas de la clave de un índice se deben especificar como `NOT NULL`.  
  
-   Si se usa la opción `DURABILITY = SCHEMA_AND_DATA` de tabla optimizada para memoria, la tabla debe tener un índice de clave principal no clúster.  
  
-   ANSI_PADDING debe ser ON.  
  
##  <a name="PrimaryKey"></a>Replicación de cambios en una clave principal  
 La clave principal de una tabla optimizada para memoria no se puede actualizar. Para replicar la actualización de una clave principal en un suscriptor, modifique el procedimiento almacenado de actualización para entregar la actualización como un par de eliminación e inserción.  
  
## <a name="see-also"></a>Vea también  
 [Replicación de SQL Server](sql-server-replication.md)  
  
  
