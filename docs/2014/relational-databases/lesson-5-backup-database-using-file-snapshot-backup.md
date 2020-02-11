---
title: 'Lección 6: migrar una base de datos de una máquina de origen local a un equipo de destino en Azure | Microsoft Docs'
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
ms.openlocfilehash: 689c3a734a5b4eb424511da52032dc348b5757ea
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "75231797"
---
# <a name="lesson-6-migrate-a-database-from-a-source-machine-on-premises-to-a-destination-machine-in-azure"></a>Lección 6: Migración de una base de datos de un equipo de origen local a un equipo de destino en Azure
  En esta lección se supone que ya tiene otro SQL Server, que puede residir en otro equipo local o en una máquina virtual de Azure. Para obtener información sobre cómo crear una máquina virtual SQL Server en Azure, consulte [aprovisionamiento de una máquina virtual SQL Server en Azure](https://www.windowsazure.com/manage/windows/common-tasks/install-sql-server/). Después de aprovisionar una máquina virtual SQL Server en Azure, asegúrese de que puede conectarse a una instancia de SQL Server en esta máquina virtual a través de SQL Server Management Studio en otro equipo.  
  
 En esta lección también se supone que ya completó los pasos siguientes:  
  
-   Tiene una cuenta de Azure Storage.  
  
-   Ha creado un contenedor en su cuenta de Azure Storage.  
  
-   Ha creado una directiva en un contenedor con derechos de lectura, escritura y enumeración. También generó una clave SAS.  
  
-   Ha creado una credencial de SQL Server en el equipo de origen.  
  
-   Ya ha creado una máquina virtual de destino SQL Server en Azure. Para crearla, se recomienda que seleccione una imagen de plataforma que incluya SQL Server 2014.  
  
 Para migrar una base de datos de SQL Server local a otra máquina virtual de Azure, puede seguir estos pasos:  
  
1.  En la máquina de origen (que es un equipo local en este tutorial), abra una ventana de consulta en SQL Server Management Studio. Separe la base de datos para moverla a otra máquina ejecutando estas instrucciones:  
  
    ```  
    -- Detach the database in the source machine   
    USE master  
    EXEC sp_detach_db 'TestDB1', 'true';  
    ```  
  
2.  Si necesita transferir una base de datos a un equipo de destino, primero debe prepararlo. Para preparar el equipo de destino, primero debe crear una credencial de SQL Server en dicho equipo. Si es una base de datos cifrada, también debe importar el certificado de la máquina de origen a la de destino.  
  
    1.  Para crear una credencial de SQL Server en el equipo de destino, siga estos pasos:  
  
        1.  Conéctese al equipo de destino mediante SQL Server Management Studio en el equipo de origen.  O bien, inicie SQL Server Management Studio en el equipo de destino directamente.  
  
        2.  En la barra de herramientas Estándar , haga clic en **Nueva consulta**.  
  
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
  
    2.  A continuación, cree una base de datos con los archivos de datos y de registro que apuntan a los archivos existentes en Azure Storage mediante la opción FOR ATTACH. En la ventana de consulta, ejecute la instrucción siguiente:  
  
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
  
 Para crear una base de datos con archivos de datos y de registro que señalen a los archivos existentes en Azure Storage mediante SQL Server Management Studio interfaz de usuario, siga estos pasos:  
  
1.  En **Explorador de objetos**, conéctese a una instancia del Motor de base de datos de SQL Server y, a continuación, expándala.  
  
2.  Haga clic con el botón derecho en **Bases de datos**y, después, haga clic en **Nueva base de datos**. A continuación, haga clic con el botón secundario en TestDB1. Haga clic en Tareas y, a continuación, haga clic en Separar. En la ventana del cuadro de diálogo Separar, active Quitar conexiones. Haga clic en **OK**.  
  
3.  Conéctese a la máquina de destino, que tiene SQL Server 2014 CTP2 o posterior. Para preparar la máquina de destino, debe crear una credencial de SQL Server en ella para señalar al mismo contenedor en el que colocó TestDB1. Si va a volver a adjuntar la base de datos en el mismo equipo, no es necesario crear otra credencial.  
  
4.  En **Explorador de objetos**, haga clic con el botón derecho en **bases** de datos y haga clic en **asociar**.  
  
5.  En el cuadro de diálogo **adjuntar bases de datos** , para especificar la base de datos que se va a adjuntar, haga clic en **Agregar**. En la ventana de diálogo **buscar archivos de base de datos** :  
  
     En ubicación del archivo de datos de la `https://teststorageaccnt.blob.core.windows.net/testcontainer/`base de datos, escriba:.  
  
     En nombre de archivo, escriba `TestDB1Data.mdf`:.  
  
6.  Haga clic en **OK**.  
  
     ![SQL 14 CTP2](../tutorials/media/ss-was-tutlesson-6-7.gif "SQL 14 CTP2")  
  
 **Lección siguiente:**  
  
 [Lección 7: Traslado de archivos de datos a Azure Storage](../relational-databases/lesson-6-generate-activity-and-backup-log-using-file-snapshot-backup.md)  
  
