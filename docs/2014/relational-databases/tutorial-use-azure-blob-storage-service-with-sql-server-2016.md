---
title: 'Tutorial: De archivos de datos SQL Server en el servicio de almacenamiento de Windows Azure | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: e69be67d-da1c-41ae-8c9a-6b12c8c2fb61
caps.latest.revision: 7
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: f805d7a9b0997d9f5a7cecbf61b5120bdf09f3cd
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37323865"
---
# <a name="tutorial-sql-server-data-files-in-windows-azure-storage-service"></a>Tutorial: Archivos de datos de SQL Server en el servicio Azure Storage
  Este es el tutorial de Archivos de datos de SQL Server en el servicio Azure Storage. Este tutorial le ayudará a saber cómo almacenar archivos de datos de SQL Server en el servicio de almacenamiento Blob de Windows Azure directamente.  
  
 La compatibilidad con la integración de SQL Server para el servicio de almacenamiento Blob de Windows Azure es una mejora de SQL Server 2014. Para información general sobre la funcionalidad y las ventajas de usar esta funcionalidad, consulte [archivos de datos de SQL Server en Windows Azure](databases/sql-server-data-files-in-microsoft-azure.md).  
  
## <a name="what-you-will-learn"></a>Aprendizaje  
 Este tutorial contiene varias lecciones en las que se muestra cómo almacenar archivos de datos de SQL Server en el servicio Azure Storage. Cada una de las lecciones se centra en una tarea determinada. Primero, aprenderá a crear una cuenta de almacenamiento y un contenedor en Windows Azure. A continuación, aprenderá a crear una credencial de SQL Server para poder integrar SQL Server con Azure Storage. Después, creará una nueva base de datos en Azure Storage directamente. Por otra parte, el tutorial presentará escenarios de cifrado, migración y de copia de seguridad y restauración.  
  
 El tutorial se divide en nueve lecciones:  
  
 **[Lección 1: Crear el contenedor y cuenta de Microsoft Azure Storage](../tutorials/lesson-1-create-windows-azure-storage-account-and-container.md)**  
 En esta lección, creará una cuenta de Azure Storage y un contenedor.  
  
 **[Lección 2. Crear una directiva en el contenedor y generar una firma de acceso compartido &#40;SAS&#41; clave](lesson-1-create-stored-access-policy-and-shared-access-signature.md)**  
 En esta lección, creará una directiva en el contenedor de blobs y también generará una firma de acceso compartido.  
  
 **[Lección 3: Crear una credencial de SQL Server](lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md)**  
 En esta lección, creará una credencial para almacenar la información de seguridad usada para tener acceso a la cuenta de almacenamiento de Windows Azure.  
  
 **[Lección 4: Creación de una base de datos en almacenamiento de Windows Azure](../relational-databases/lesson-3-database-backup-to-url.md)**  
 En esta lección, creará una base de datos de Azure Storage con la opción FILENAME de la instrucción CREATE DATABASE.  
  
 **[Lección 5. &#40;Opcional&#41; cifrar la base de datos mediante TDE](../relational-databases/lesson-4-restore-database-to-virtual-machine-from-url.md)**  
 En esta lección, cifrará la base de datos mediante un cifrado de datos transparente (TDE) y un certificado de servidor.  
  
 **[Lección 6: Migrar una base de datos desde un origen de máquina local a un equipo de destino de Windows Azure](lesson-5-backup-database-using-file-snapshot-backup.md)**  
 En esta lección, migrará una base de datos desde el entorno local a una máquina virtual de Windows Azure mediante la opción CREATE DATABASE FOR ATTACH.  
  
 **[Lección 7: Mover los archivos de datos a almacenamiento de Windows Azure](../relational-databases/lesson-6-generate-activity-and-backup-log-using-file-snapshot-backup.md)**  
 En esta lección, moverá los archivos de datos a Azure Storage mediante la instrucción ALTER DATABASE.  
  
 **[Lección 8: Restaurar una base de datos en Azure Storage](../relational-databases/lesson-7-restore-a-database-to-a-point-in-time.md)**  
 En esta lección, restaurará una base de datos en Azure Storage con la opción MOVE de la instrucción RESTORE DATABASE.  
  
 **[Lección 9. Restaurar una base de datos de almacenamiento de Windows Azure](lesson-8-restore-as-new-database-from-log-backup.md)**  
 En esta lección, restaurará una base de datos desde Azure Storage con la opción MOVE de la instrucción RESTORE DATABASE.  
  
## <a name="see-also"></a>Vea también  
 [Archivos de datos de SQL Server en Windows Azure](databases/sql-server-data-files-in-microsoft-azure.md)  
  
  
