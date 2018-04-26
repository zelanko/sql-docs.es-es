---
title: 'Lección 8: Restauración como una base de datos nueva desde una copia de seguridad de registros | Microsoft Docs'
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: tutorial
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: ebba12c7-3d13-4c9d-8540-ad410a08356d
caps.latest.revision: 12
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 632c6dbc496da650418ef4bc7239605b0e9e8149
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="lesson-8-restore-as-new-database-from-log-backup"></a>Lección 8: Restaurar como una base de datos nueva desde una copia de seguridad de registros
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
En esta lección, restaurará la base de datos AdventureWorks2014 como una base de datos nueva desde una copia de seguridad del registro de transacciones de instantáneas de archivos.  
  
En este escenario, realizará una restauración a una instancia de SQL Server en una máquina virtual diferente a efectos de análisis de negocio e informes. Al restaurar en una instancia diferente en una máquina virtual diferente, se descarga la carga de trabajo en una máquina virtual dedicada y con un tamaño para este propósito, quitando los requisitos del recurso del sistema transaccional.  
  
La restauración desde una copia de seguridad del registro de transacciones con una copia de seguridad de instantáneas de archivos es muy rápida, considerablemente más rápido que con las copias de seguridad de streaming tradicionales. Con las copias de seguridad de streaming tradicionales, usaba la copia de seguridad completa de la base de datos, quizás una copia de seguridad diferencial y algunas o todas las copias de seguridad del registro de transacciones (o una copia de seguridad completa de la base de datos nueva). En cambio, con las copias de seguridad de registros de instantáneas de archivos, solo necesita la copia de seguridad de registros más reciente (o cualquier otra copia de seguridad de registros o dos copias de seguridad de registros adyacentes para la restauración a un momento dado entre dos copias de seguridad de registros). Para que quede claro, solo necesita un conjunto de copia de seguridad de registros de instantáneas de archivos, porque cada copia de seguridad de registros de instantáneas de archivos crea una instantánea de archivo de cada archivo de base de datos (cada archivo de datos y el archivo de registro).  
  
Para restaurar una base de datos a una base de datos nueva desde una copia de seguridad del registro de transacciones mediante la copia de seguridad de instantánea de archivo, siga estos pasos:  
  
1.  Conéctese a SQL Server Management Studio.  
  
2.  Abra una nueva ventana de consulta y conéctese a la instancia de SQL Server 2016 del motor de base de datos de una máquina virtual de Azure.  
  
    > [!NOTE]  
    > Si se trata de una máquina virtual de Azure diferente de la que ha usado para las lecciones anteriores, asegúrese de que ha seguido los pasos descritos en [Lección 2: Crear una credencial de SQL Server con una firma de acceso compartido](../relational-databases/lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md). Si quiere restaurar a un contenedor diferente, siga los pasos de [Lección 1: Crear una directiva de acceso almacenada y una firma de acceso compartido en un contenedor de Azure](../relational-databases/lesson-1-create-stored-access-policy-and-shared-access-signature.md) y [Lección 2: Crear una credencial de SQL Server con una firma de acceso compartido](../relational-databases/lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md) para el nuevo contenedor.  
  
3.  Copie y pegue el siguiente script de Transact-SQL en la ventana de consulta. Seleccione el archivo de copia de seguridad de registros que quiera usar. Modifique la dirección URL correctamente para su nombre de cuenta de almacenamiento y el contenedor que ha especificado en la lección 1, proporcione el nombre de archivo de la copia de seguridad de registros y ejecute este script.  
  
    ```  
  
    -- restore as a new database from a transaction log backup file  
    RESTORE DATABASE AdventureWorks2014_EOM   
        FROM URL = 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/<logbackupfile.bak'    
        WITH MOVE 'AdventureWorks2014_data' to 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/AdventureWorks2014_EOM_Data.mdf'  
       , MOVE 'AdventureWorks2014_log' to 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/AdventureWorks2014_EOM_Log.ldf'  
       , RECOVERY  
    --, REPLACE  
  
    ```  
  
4.  Revise el resultado para comprobar que la restauración se ha realizado correctamente.  
  
5.  En el Explorador de objetos, conéctese a Azure Storage.  
  
6.  Expanda los contenedores, expanda el contenedor que ha creado en la lección 1 (actualícelo si es necesario) y compruebe que aparecen los nuevos archivos de datos y de registro en el contenedor, junto con los blobs de las lecciones anteriores.  
  
    ![Contenedor de Azure que muestra los datos y los archivos de registro para la nueva base de datos](../relational-databases/media/e9705083-86bc-4309-a0bf-92c15f174c0a.JPG "Contenedor de Azure que muestra los datos y los archivos de registro para la nueva base de datos")  
  
[Lección 9: Administrar conjuntos de copia de seguridad y copias de seguridad de instantáneas de archivos](../relational-databases/lesson-9-manage-backup-sets-and-file-snapshot-backups.md)  
  
  
  
