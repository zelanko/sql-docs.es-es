---
title: 'Lección 8: Restaurar una base de datos en Azure Storage | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: a9f99670-e1de-441e-972c-69faffcac17a
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: f7da373509d875057f4d1ff50884ec446feb6cd2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66090710"
---
# <a name="lesson-8-restore-a-database-to-windows-azure-storage"></a>Lección 8: Restaurar una base de datos en Azure Storage
  En esta lección, aprenderá a crear un archivo de copia de seguridad local y a restaurarlo en Azure Storage. Tenga en cuenta que puede tener la base de datos en local o en una máquina virtual de Windows Azure. Para seguir esta lección, no es necesario completar las lecciones 4, 5, 6 y 7.  
  
 En esta lección se supone que ya completó los pasos siguientes:  
  
-   Tiene una cuenta de Almacenamiento de Windows Azure.  
  
-   Ha creado un contenedor con su cuenta de Almacenamiento de Windows Azure.  
  
-   Ha creado una directiva en un contenedor con derechos de lectura, escritura y enumeración. También generó una clave SAS.  
  
-   Ha creado una credencial de SQL Server en el equipo de origen basada en la Firma de acceso compartido.  
  
-   Ha creado una base de datos en el equipo de origen.  
  
 Para restaurar una base de datos en Azure Storage, puede seguir estos pasos:  
  
1.  En el equipo de origen, inicie SQL Server Management Studio.  
  
2.  Cuando se conecte a la base de datos recién creada, abra la ventana de consulta. Ejecute la siguiente instrucción:  
  
    ```sql  
  
    USE TestDB3Restore;   
    GO   
    BACKUP DATABASE TestDB3Restore   
    TO DISK = 'C:\BACKUP\TestDB3Restore.Bak'   
       WITH FORMAT,   
       NAME = 'Full Backup of TestDB3Restore'   
    GO  
  
    ```  
  
3.  Después, copie y ejecute las instrucciones siguientes en la ventana de consulta.  
  
    ```sql  
  
    USE master;   
    GO   
    RESTORE DATABASE TestDB3Restore    
    FROM DISK = 'C:\BACKUP\TestDB3Restore.bak'    
    WITH REPLACE,   
    MOVE 'TestDB3Restore' TO 'https://teststorageaccnt.blob.core.windows.net/testcontainrestore/TestDB3Restore.mdf',     
    MOVE 'TestDB3Restore_log' TO 'https://teststorageaccnt.blob.core.windows.net/testcontainrestore/TestDB3Restore_log.ldf';   
    GO  
  
    ```  
  
     Al final de este paso, el contenedor debe enumerar los archivos (.ldf) y datos (.mdf) en el Portal de administración.  
  
 Para restaurar una base de datos con los archivos de registros y datos de Azure Storage mediante la interfaz de usuario de SQL Server Management Studio, siga estos pasos:  
  
1.  En **Explorador de objetos**, haga clic en el nombre del servidor para expandir el árbol de servidores.  
  
2.  Expanda **bases de datos**y seleccione la base de datos.  
  
3.  Haga clic con el botón derecho en la base de datos, seleccione **Tareas**y, después, haga clic en **Restaurar**.  
  
4.  En el **General** página, en el **restaurar** sección de código fuente, haga clic en **origen** dispositivo.  
  
5.  Haga clic en el botón Examinar para el **origen** cuadro de texto de dispositivo, que abre el **seleccionar dispositivos de copia de seguridad** cuadro de diálogo.  
  
6.  En el cuadro de texto medios de copia de seguridad, seleccione **archivo**y haga clic en el **agregar** botón para buscar el archivo de copia de seguridad (.bak). Haga clic en **Aceptar**.  
  
7.  Haga clic en **archivos** en la primera página.  
  
8.  En el **restaurar archivos de base de datos** como sección en **restaurar como** , escriba lo siguiente:  
  
     Para el archivo de datos, escriba: `https://teststorageaccnt.blob.core.windows.net/testrestoressms/TestRESSMS.mdf`. Archivo de registro, escriba: `https://teststorageaccnt.blob.core.windows.net/testrestoressms/TestRESSMS_log.ldf`.  
  
     ![SQL 14 CTP2](../tutorials/media/ss-was-tutlesson-8-8.gif "SQL 14 CTP2")  
  
9. Haga clic en **Aceptar**.  
  
 Cuando se realice la restauración, inicie sesión en el Portal de administración. Debe poder ver los archivos .mdf y .ldf en el contenedor como sigue:  
  
 ![SQL 14 CTP2](../tutorials/media/ss-was-tutlesson-8-9.gif "SQL 14 CTP2")  
  
 **Lección siguiente:**  
  
 [Lección 9: Restaurar una base de datos desde Azure Storage](../relational-databases/lesson-8-restore-as-new-database-from-log-backup.md)  
  
  
