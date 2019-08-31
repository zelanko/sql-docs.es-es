---
title: 'Tutorial: SQL Server archivos de datos en Azure Storage servicio | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: e69be67d-da1c-41ae-8c9a-6b12c8c2fb61
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a15f6735ef0ef79b7eb953445c926f60f6bfb12e
ms.sourcegitcommit: 3b1f873f02af8f4e89facc7b25f8993f535061c9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/30/2019
ms.locfileid: "70176086"
---
# <a name="tutorial-sql-server-data-files-in-azure-storage-service"></a>Tutorial: SQL Server archivos de datos en Azure Storage servicio
  Este es el tutorial SQL Server los archivos de datos en Azure Storage Service. Este tutorial le ayudará a comprender cómo almacenar los archivos de datos de SQL Server en el servicio de almacenamiento de blobs de Azure directamente.  
  
 SQL Server compatibilidad con la integración del servicio de almacenamiento de blobs de Azure es una mejora del SQL Server 2014. Para obtener información general sobre la funcionalidad y las ventajas de usar esta funcionalidad, vea [SQL Server archivos de datos en Azure](databases/sql-server-data-files-in-microsoft-azure.md).  
  
## <a name="what-you-will-learn"></a>Aprendizaje  
 En este tutorial se muestra cómo almacenar archivos de datos de SQL Server en Azure Storage Service en varias lecciones. Cada una de las lecciones se centra en una tarea determinada. En primer lugar, aprenderá a crear una cuenta de almacenamiento y un contenedor en Azure. A continuación, aprenderá a crear una credencial SQL Server para poder integrar SQL Server con Azure Storage. A continuación, creará una base de datos en Azure Storage directamente. Por otra parte, el tutorial presentará escenarios de cifrado, migración y de copia de seguridad y restauración.  
  
 El tutorial se divide en nueve lecciones:  
  
 **[Lección 1: Crear Azure Storage cuenta y un contenedor](../tutorials/lesson-1-create-windows-azure-storage-account-and-container.md)**  
 En esta lección, creará una cuenta de Azure Storage y un contenedor.  
  
 **[Lección 2. Creación de una directiva en el contenedor y generación de una &#40;clave&#41; SAS de firma de acceso compartido](lesson-1-create-stored-access-policy-and-shared-access-signature.md)**  
 En esta lección, creará una directiva en el contenedor de blobs y también generará una firma de acceso compartido.  
  
 **[Lección 3: Crear una credencial de SQL Server](lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md)**  
 En esta lección, creará una credencial para almacenar la información de seguridad usada para acceder a la cuenta de Azure Storage.  
  
 **[Lección 4: Crear una base de datos en Azure Storage](../relational-databases/lesson-3-database-backup-to-url.md)**  
 En esta lección, creará una base de datos en Azure Storage mediante la opción CREATE DATABASE FILENAME.  
  
 **Lección 5. &#40;Opcional&#41; cifrar la base de datos mediante TDE**  
 En esta lección, cifrará la base de datos mediante un cifrado de datos transparente (TDE) y un certificado de servidor.  
  
 **[Lección 6: Migración de una base de datos de una máquina de origen local a un equipo de destino en Azure](lesson-5-backup-database-using-file-snapshot-backup.md)**  
 En esta lección, va a migrar una base de datos de local a una máquina virtual de Azure mediante la opción crear base de datos para adjuntar.  
  
 **[Lección 7: Mueva los archivos de datos a Azure Storage](../relational-databases/lesson-6-generate-activity-and-backup-log-using-file-snapshot-backup.md)**  
 En esta lección, moverá los archivos de datos a Azure Storage mediante la instrucción ALTER DATABASE.  
  
 **[Lección 8: Restaurar una base de datos a Azure Storage](../relational-databases/lesson-7-restore-a-database-to-a-point-in-time.md)**  
 En esta lección, restaurará una base de datos de a Azure Storage mediante la opción RESTOre Database MOVE.  
  
 **[Lección 9. Restaurar una base de datos desde Azure Storage](lesson-8-restore-as-new-database-from-log-backup.md)**  
 En esta lección, restaurará una base de datos de Azure Storage mediante la opción RESTOre Database MOVE.  
  
## <a name="see-also"></a>Vea también  
 [SQL Server de los archivos de datos en Azure](databases/sql-server-data-files-in-microsoft-azure.md)  
  
  
