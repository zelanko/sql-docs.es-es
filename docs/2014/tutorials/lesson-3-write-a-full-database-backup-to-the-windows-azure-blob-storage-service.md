---
title: 'Lección 3: Escribir una copia de seguridad de base de datos completa en el servicio de Windows Azure Blob Storage | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 454c8296-64e9-46ed-b141-5ebfbc8a4fe2
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: f0de77c43dc2a18bbbb4496f6c1d1c3aab21de96
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48172275"
---
# <a name="lesson-3-write-a-full-database-backup-to-the-windows-azure-blob-storage-service"></a>Lección 3: Escribir una copia de seguridad completa de la base de datos en el servicio Azure Blob Storage
  En esta lección se muestra el uso de una instrucción tsql para realizar una copia de seguridad completa de la base de datos en el servicio de almacenamiento Blob de Windows Azure.  
  
## <a name="perform-a-full-database-backup-to-the-windows-azure-blob-storage-service"></a>Realizar una copia de seguridad completa de la base de datos en el servicio de almacenamiento Blob de Windows Azure  
 Para realizar una copia de seguridad completa de la base de datos, siga estos pasos:  
  
1.  Conectarse a [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
2.  En el **Explorador de objetos**, conéctese a la instancia de [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].  
  
3.  En el menú Estándar, haga clic en **Nueva consulta**.  
  
4.  Copie y pegue el siguiente ejemplo en la ventana de consulta, realice las modificaciones necesarias y haga clic en **Ejecutar**.  
  
    ```  
    BACKUP DATABASE[AdventureWorks2012]   
    TO URL = 'https://mystorageaccount.blob.core.windows.net/privatecontainertest/AdventureWorks2012.bak'   
    /* URL includes the endpoint for the BLOB service, followed by the container name, and the name of the backup file*/   
    WITH CREDENTIAL = 'mycredential';  
    /* name of the credential you created in the previous step */   
    GO  
  
    ```  
  
5.  En el Explorador de objetos, conéctese a Almacenamiento de Windows Azure. Busque el contenedor y los archivos de copia de seguridad recién creados.  
  
## <a name="next-lesson"></a>Lección siguiente  
 [Lección 4: Realizar una restauración desde una copia de seguridad de base de datos completa](../../2014/tutorials/lesson-4-perform-a-restore-from-a-full-database-backup.md).  
  
  
