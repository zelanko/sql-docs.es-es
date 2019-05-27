---
title: 'Lección 6: Migrar una base de datos desde un origen de máquina local a un equipo de destino de Windows Azure | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: d9134ade-7b03-4c5c-8ed3-3bc369a61691
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 1a5787a3f5aecd746ac9aafd5850e6109ebcd999
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66090695"
---
# <a name="lesson-6-migrate-a-database-from-a-source-machine-on-premises-to-a-destination-machine-in-windows-azure"></a>Lección 6: Migración de una base de datos desde un equipo de origen local a un equipo de destino en Windows Azure
  En esta lección se supone que ya tiene otro servidor SQL Server, que puede residir en otro equipo local o en una máquina virtual de Windows Azure. Para obtener información sobre cómo crear una máquina virtual de SQL Server en Windows Azure, consulte [aprovisionamiento de una máquina Virtual de SQL Server en Windows Azure](http://www.windowsazure.com/manage/windows/common-tasks/install-sql-server/). Después de aprovisionar una máquina virtual de SQL Server en Windows Azure, asegúrese de que puede conectarse a una instancia de SQL Server en esta máquina virtual a través de SQL Server Management Studio en otro equipo.  
  
 En esta lección también se supone que ya completó los pasos siguientes:  
  
-   Tiene una cuenta de Almacenamiento de Windows Azure.  
  
-   Ha creado un contenedor con su cuenta de Almacenamiento de Windows Azure.  
  
-   Ha creado una directiva en un contenedor con derechos de lectura, escritura y enumeración. También generó una clave SAS.  
  
-   Ha creado una credencial de SQL Server en el equipo de origen.  
  
-   Ha creado una máquina virtual de SQL Server de destino en Windows Azure. Para crearla, se recomienda que seleccione una imagen de plataforma que incluya SQL Server 2014.  
  
 Para migrar una base de datos local de SQL Server a otra máquina virtual de Windows Azure, puede seguir estos pasos:  
  
1.  En la máquina de origen (que es un equipo local en este tutorial), abra una ventana de consulta en SQL Server Management Studio. Separe la base de datos para moverla a otra máquina ejecutando estas instrucciones:  
  
    ```  
    -- Detach the database in the source machine   
    USE master  
    EXEC sp_detach_db 'TestDB1', 'true';  
    ```  
  
2.  Si necesita transferir una base de datos a un equipo de destino, primero debe prepararlo. Para preparar el equipo de destino, primero debe crear una credencial de SQL Server en dicho equipo. Si es una base de datos cifrada, también debe importar el certificado de la máquina de origen a la de destino.  
  
    1.  Para crear una credencial de SQL Server en el equipo de destino, siga estos pasos:  
  
        1.  Conéctese al equipo de destino mediante SQL Server Management Studio en el equipo de origen.  O bien, inicie SQL Server Management Studio en el equipo de destino directamente.  
  
        2.  En la barra de herramientas estándar, haga clic en **nueva consulta**.  
  
        3.  Copie y pegue el ejemplo siguiente en la ventana de consulta, y modifíquelo como sea necesario. La siguiente instrucción crea una credencial de SQL Server para almacenar el certificado de acceso compartido del contenedor de almacenamiento.  
  
            ```sql  
  
            USE master   
            GO   
            CREATE CREDENTIAL [http://teststorageaccnt.blob.core.windows.net/testcontainer]   
            WITH IDENTITY='SHARED ACCESS SIGNATURE',   
            SECRET = 'your SAS key'   
            GO  
  
            ```  
  
        4.  Para ver todas las credenciales disponibles, puede ejecutar la siguiente instrucción en la ventana de consulta:  
  
            ```sql  
            SELECT * from sys.credentials   
            ```  
  
        5.  Cuando se conecte al servidor de destino, abra la ventana de consulta y ejecute:  
  
            ```sql  
  
            -- Create a master key and a server certificate   
            USE master   
            GO   
            CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'MySQLKey01'; -- You may use a different password.   
            GO   
            CREATE CERTIFICATE MySQLCert   
            FROM FILE = 'C:\certs\MySQLCert.CER'   
            WITH PRIVATE KEY   
            (   
            FILE = 'C:\certs\MySQLPrivateKeyFile.PVK',   
            DECRYPTION BY PASSWORD = 'MySQLKey01'   
            );   
            GO  
  
            ```  
  
             Al final de este paso, la máquina de destino ha importado el certificado de cifrado cuya copia de seguridad se realizó desde la máquina de origen. A continuación, puede adjuntar los archivos de datos en el equipo de destino.  
  
    2.  A continuación, cree una base de datos con los archivos de registro y de datos que señalan a los archivos existentes en Azure Storage con la opción FOR ATTACH. En la ventana de consulta, ejecute la instrucción siguiente:  
  
        ```sql  
  
        --Create a database on the destination server   
        CREATE DATABASE TestDB1onDest   
        ON   
        (NAME = TestDB1_data,   
            FILENAME = 'https://teststorageaccnt.blob.core.windows.net/testcontainer/TestDB1Data.mdf' )   
        LOG ON   
         (NAME = TestDB1_log,   
            FILENAME = 'https://teststorageaccnt.blob.core.windows.net/testcontainer/TestDB1Log.ldf')   
        FOR ATTACH   
        GO  
  
        ```  
  
    3.  En el Explorador de objetos, haga clic en Bases de datos y, a continuación, haga clic con el botón secundario en Actualizar. Debe poder ver la base de datos creada recientemente TestDB1onDest.  
  
    4.  Después, en la ventana de consulta, ejecute la instrucción siguiente:  
  
        ```sql  
  
        USE TestDB1onDest   
        SELECT * FROM Table1;   
        GO  
  
        ```  
  
         Debería enumerar todos los datos que especificó en la lección 4.  
  
 Tenga en cuenta que la base de datos cifrada se transfirió a otra instancia de cálculo sin mover los datos.  
  
 Para crear una base de datos con los archivos de registros y datos para los archivos existentes de Azure Storage mediante la interfaz de usuario de SQL Server Management Studio, siga estos pasos:  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del Motor de base de datos de SQL Server y expándala.  
  
2.  Haga clic con el botón derecho en **Bases de datos**y, después, haga clic en **Nueva base de datos**. A continuación, haga clic con el botón secundario en TestDB1. Haga clic en Tareas y, a continuación, haga clic en Separar. En la ventana del cuadro de diálogo Separar, active Quitar conexiones. Haga clic en **Aceptar**.  
  
3.  Conéctese a la máquina de destino, que tiene SQL Server 2014 CTP2 o posterior. Para preparar la máquina de destino, debe crear una credencial de SQL Server en ella para señalar al mismo contenedor en el que colocó TestDB1. Si va a volver a adjuntar la base de datos en el mismo equipo, no es necesario crear otra credencial.  
  
4.  En **Explorador de objetos**, haga clic en **bases de datos** y haga clic en **adjuntar**.  
  
5.  En el **adjuntar bases de datos** cuadro de diálogo, para especificar la base de datos que se adjuntará, haga clic en **agregar**. En el **buscar archivos de base de datos** ventana de cuadro de diálogo:  
  
     Ubicación del archivo de datos de base de datos, escriba: `https://teststorageaccnt.blob.core.windows.net/testcontainer/`.  
  
     Nombre de archivo, escriba: `TestDB1Data.mdf`.  
  
6.  Haga clic en **Aceptar**.  
  
     ![SQL 14 CTP2](../tutorials/media/ss-was-tutlesson-6-7.gif "SQL 14 CTP2")  
  
 **Lección siguiente:**  
  
 [Lección 7: Mover los archivos de datos a almacenamiento de Windows Azure](../relational-databases/lesson-6-generate-activity-and-backup-log-using-file-snapshot-backup.md)  
  
  
