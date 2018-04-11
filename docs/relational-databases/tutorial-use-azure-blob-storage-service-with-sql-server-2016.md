---
title: 'Tutorial: Usar el servicio Azure Blob Storage con SQL Server 2016 | Microsoft Docs'
ms.custom: ''
ms.date: 01/07/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.component: tutorial
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: e69be67d-da1c-41ae-8c9a-6b12c8c2fb61
caps.latest.revision: 23
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 132e4242b7d9484fb0ce22e6628e07fc77adc8b3
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/06/2018
---
# <a name="tutorial-use-azure-blob-storage-service-with-sql-server-2016"></a>Tutorial: Usar el servicio Azure Blob Storage con SQL Server 2016
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Bienvenido al tutorial del servicio Trabajar con SQL Server 2016 en Microsoft Azure Blob Storage. Este tutorial le ayudará a saber cómo usar el servicio Microsoft Azure Blob Storage para archivos de datos de SQL Server y copias de seguridad de SQL Server.  
  
La compatibilidad de integración de SQL Server para el servicio Microsoft Azure Blob Storage comenzó como una mejora de SQL Server 2012 Service Pack 1 CU2 y se ha mejorado aún más con SQL Server 2014 y SQL Server 2016. Para obtener información general sobre la funcionalidad y las ventajas de usarla, consulte [Archivos de datos de SQL Server en Microsoft Azure](../relational-databases/databases/sql-server-data-files-in-microsoft-azure.md). Para obtener una demostración en vivo, consulte [Demo of Point in Time Restore](https://channel9.msdn.com/Blogs/Windows-Azure/File-Snapshot-Backups-Demo)(Demostración de restauración a un momento dado).  
  
  
**Descargar**<br /><br />**>>**  Para descargar [!INCLUDE[ssSQL15](../includes/sssql15-md.md)], vaya al  **[Centro de evaluación](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016)**.<br /><br />**>>**  ¿Tiene una cuenta de Azure?  Si es así, haga clic **[aquí](https://azure.microsoft.com/en-us/services/virtual-machines/sql-server/)** para poner en marcha una máquina virtual con [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] ya instalado.  
  
## <a name="what-you-will-learn"></a>Aprendizaje  
En este tutorial se incluyen varias lecciones en las que aprenderá a trabajar con archivos de datos de SQL Server en el servicio Microsoft Azure Blob Storage. Cada lección se centra en una tarea específica y se deben completar las lecciones por orden. En primer lugar, aprenderá a crear un nuevo contenedor en Blob Storage con una directiva de acceso almacenada y una firma de acceso compartido. Después, aprenderá a crear una credencial de SQL Server para integrar SQL Server con Azure Blob Storage. Luego, realizará una copia de seguridad de una base de datos en Blob Storage y la restaurará en una máquina virtual de Azure. Después usará la copia de seguridad del registro de transacciones de instantáneas de archivos de SQL Server 2016 para restaurar a un momento dado y a una nueva base de datos. Por último, en el tutorial se muestra el uso de funciones y procedimientos almacenados del sistema de metadatos para ayudarle a comprender y trabajar con copias de seguridad de instantáneas de archivos.  
  
En este artículo se asume que:  
  
-   Tiene una instancia local de SQL Server 2016 con una copia de AdventureWorks2014 instalada.  
  
-   Tiene una cuenta de almacenamiento de Azure.  
  
-   Tiene al menos una máquina virtual con SQL Server 2016 instalado y esta máquina virtual está aprovisionada según [Aprovisionamiento de una máquina virtual de SQL Server en el Portal de Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-provision-sql-server/). De forma opcional, se puede usar una segunda máquina virtual para el escenario de la [Lección 8: Restaurar como una base de datos nueva desde una copia de seguridad de registros](../relational-databases/lesson-8-restore-as-new-database-from-log-backup.md)).  
  
Este tutorial se divide en nueve lecciones, que debe completar en orden:  
  
**[Lección 1: Crear una directiva de acceso almacenada y una firma de acceso compartido en un contenedor de Azure](../relational-databases/lesson-1-create-stored-access-policy-and-shared-access-signature.md)**  
En esta lección, creará una directiva en un nuevo contenedor de blobs y también generará una firma de acceso compartido para usar al crear una credencial de SQL Server.  
  
**[Lección 2: Crear una credencial de SQL Server con una firma de acceso compartido](../relational-databases/lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md)**  
En esta lección, creará una credencial mediante una clave SAS para almacenar la información de seguridad usada para acceder a la cuenta de almacenamiento de Microsoft Azure.  
  
**[Lesson 3: Database backup to URL (Lección 3: Copia de seguridad de base de datos en la dirección URL)](../relational-databases/lesson-3-database-backup-to-url.md)**  
En esta lección, realizará una copia de seguridad de una base de datos local en Microsoft Azure Blob Storage.  
  
**[Lección 4: Restaurar la base de datos a la máquina virtual desde la dirección URL](../relational-databases/lesson-4-restore-database-to-virtual-machine-from-url.md)**  
En esta lección, restaurará una base de datos a una máquina virtual de Azure desde Microsoft Azure Blob Storage.  
  
**[Lesson 5: Backup database using file-snapshot backup (Lección 5: Realizar una copia de seguridad de la base de datos mediante la copia de seguridad de instantáneas de archivos)](../relational-databases/lesson-5-backup-database-using-file-snapshot-backup.md)**  
En esta lección, realizará una copia de seguridad de una base de datos mediante la copia de seguridad de instantáneas de archivos y los metadatos de instantáneas de archivos de vista.  
  
**[Lección 6: Generar el registro de actividades y copias de seguridad mediante la copia de seguridad de instantáneas de archivos](../relational-databases/lesson-6-generate-activity-and-backup-log-using-file-snapshot-backup.md)**  
En esta lección, generará actividad en la base de datos y realizará varias copias de seguridad de registros mediante la copia de seguridad de instantáneas de archivos y los metadatos de instantáneas de archivos de vista.  
  
**[Lección 7: Restaurar una base de datos a un momento dado](../relational-databases/lesson-7-restore-a-database-to-a-point-in-time.md)**  
En esta lección, restaurará una base de datos a un momento dado con dos copias de seguridad del registro de instantáneas de archivos.  
  
**[Lección 8: Restaurar como una base de datos nueva desde una copia de seguridad de registros](../relational-databases/lesson-8-restore-as-new-database-from-log-backup.md)**  
En esta lección, restaurará desde una copia de seguridad de registros de instantáneas de archivo a una base de datos en otra máquina virtual.  
  
**[Lección 9: Administrar conjuntos de copia de seguridad y copias de seguridad de instantáneas de archivos](../relational-databases/lesson-9-manage-backup-sets-and-file-snapshot-backups.md)**  
En esta lección, eliminará conjuntos de copia de seguridad innecesarios y aprenderá a eliminar copias de seguridad de instantáneas de archivos huérfanos (cuando sea necesario).  
  
## <a name="see-also"></a>Ver también  
[Archivos de datos de SQL Server en Microsoft Azure](../relational-databases/databases/sql-server-data-files-in-microsoft-azure.md)  
[Copias de seguridad de instantánea de archivos para archivos de base de datos de Azure](../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)  
[Copia de seguridad en URL de SQL Server](../relational-databases/backup-restore/sql-server-backup-to-url.md)  
  
  
  

