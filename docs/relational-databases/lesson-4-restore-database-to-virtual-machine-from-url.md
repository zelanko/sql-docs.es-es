---
title: "Lección 4: Restauración de la base de datos a la máquina virtual desde la dirección URL | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: tutorial
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
ms.assetid: ba793c8f-665a-4c46-b68d-f558a37906b2
caps.latest.revision: "23"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ad780f4f49f99c0537e5ff560d1addab59627d9c
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="lesson-4-restore-database-to-virtual-machine-from-url"></a>Lección 4: Restaurar la base de datos a la máquina virtual desde la dirección URL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] En esta lección, restaurará la base de datos AdventureWorks2014 en la instancia de SQL Server 2016 de la máquina virtual de Azure.  
  
> [!NOTE]  
> Para simplificar este tutorial, usamos el mismo contenedor para los archivos de datos y de registros que se usan para la copia de seguridad de la base de datos. En un entorno de producción, usaría varios contenedores y, con frecuencia, varios archivos de datos. Con SQL Server 2016, también puede considerar la posibilidad de crear bandas de la copia de seguridad en varios blobs para aumentar el rendimiento de la copia de seguridad al realizar la copia de seguridad de una base de datos de gran tamaño.  
  
Para restaurar la base de datos de SQL Server 2014 desde Azure Blob Storage en la instancia de SQL Server 2016 en la máquina virtual de Azure, siga estos pasos:  
  
1.  Conéctese a SQL Server Management Studio.  
  
2.  Abra una nueva ventana de consulta y conéctese a la instancia de SQL Server 2016 del motor de base de datos de la máquina virtual de Azure.  
  
3.  Copie y pegue el siguiente script de Transact-SQL en la ventana de consulta. Modifique la dirección URL correctamente para su nombre de cuenta de almacenamiento y el contenedor que ha especificado en la lección 1 y, después, ejecute este script.  
  
    ```  
  
    -- Restore AdventureWorks2014 from URL to SQL Server instance using Azure blob storage for database files  
    RESTORE DATABASE AdventureWorks2014   
       FROM URL = 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/AdventureWorks2014_onprem.bak'   
       WITH  
          MOVE 'AdventureWorks2014_data' to 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/AdventureWorks2014_Data.mdf'  
         ,MOVE 'AdventureWorks2014_log' to 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/AdventureWorks2014_Log.ldf'  
    --, REPLACE  
  
    ```  
  
4.  Abra el Explorador de objetos y conéctese a la instancia de SQL Server 2016 de Azure.  
  
5.  En el Explorador de objetos, expanda el nodo Bases de datos y compruebe que se ha restaurado la base de datos AdventureWorks2014 (actualice el nodo según sea necesario).  
  
    ![Base de datos de Adventure Works 2014 restaurada a SQL Server 2016 en máquina virtual](../relational-databases/media/311f69a6-8443-4df5-8f30-3103c2472300.JPG "Base de datos de Adventure Works 2014 restaurada a SQL Server 2016 en máquina virtual")  
  
6.  En el Explorador de objetos, haga clic en AdventureWorks2014 y haga clic en Propiedades (haga clic en Cancelar cuando haya terminado).  
  
7.  Haga clic en Archivos y compruebe que la ruta de acceso a los dos archivos de base de datos son direcciones URL que apuntan a los blobs del contenedor de blobs de Azure.  
  
    ![Propiedades de base de datos en los que se muestra la ruta de acceso de los archivos de datos lógicos en forma de URL](../relational-databases/media/cfeee576-6319-460e-9fa2-f0922e02ee23.JPG "Propiedades de base de datos en los que se muestra la ruta de acceso de los archivos de datos lógicos en forma de URL")  
  
8.  En el Explorador de objetos, conéctese a Azure Storage.  
  
9. Expanda Contenedores, expanda el contenedor que ha creado en la Lección 1 y compruebe que AdventureWorks2014_Data.mdf y AdventureWorks2014_Log.ldf del paso 3 anterior aparecen en este contenedor, junto con el archivo de copia de seguridad de la Lección 3 (actualice el nodo según sea necesario).  
  
    ![Los archivos de datos y de registro de Adventure Works 2014 aparecen en forma de blobs en el contenedor de Azure](../relational-databases/media/156c7d73-44be-4754-9653-04cccb6c3066.JPG "Los archivos de datos y de registro de Adventure Works 2014 aparecen en forma de blobs en el contenedor de Azure")  
  
**Lección siguiente:**  
  
[Lesson 5: Backup database using file-snapshot backup (Lección 5: Realizar una copia de seguridad de la base de datos mediante la copia de seguridad de instantáneas de archivos)](../relational-databases/lesson-5-backup-database-using-file-snapshot-backup.md)  
  
  
  
