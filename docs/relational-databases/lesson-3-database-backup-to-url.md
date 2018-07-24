---
title: 'Lección 3: Copia de seguridad de base de datos en la dirección URL | Microsoft Docs'
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: tutorial
ms.reviewer: ''
ms.suite: sql
ms.technology: backup-restore
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- SQL Server 2016
ms.assetid: a9ae1501-b614-49d3-b975-6569da8350b2
caps.latest.revision: 16
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: aa6da6086cd5c1a0ebfd56394e5c79b2078ef82e
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/12/2018
ms.locfileid: "38978937"
---
# <a name="lesson-3-database-backup-to-url"></a>Lesson 3: Database backup to URL (Lección 3: Copia de seguridad de base de datos en la dirección URL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
En esta lección, realizará una copia de seguridad de la base de datos AdventureWorks2014 en la instancia local de SQL Server 2016 en el contenedor de Azure que ha creado en la [Lección 1: Crear una directiva de acceso almacenada y una firma de acceso compartido en un contenedor de Azure](../relational-databases/lesson-1-create-stored-access-policy-and-shared-access-signature.md).  
  
> [!NOTE]  
> Si quiere realizar una copia de seguridad de una base de datos de SQL Server 2012 SP1 CU2 o posterior o de una base de datos de SQL Server 2014 a este contenedor de Azure, puede usar la sintaxis en desuso que aparece [aquí](https://technet.microsoft.com/library/dn435916(v=sql.120).aspx) para realizar una copia de seguridad en la dirección URL mediante la sintaxis WITH CREDENTIAL.  
  
Para realizar una copia de seguridad de una base de datos en Blob Storage, siga estos pasos:  
  
1.  Conéctese a SQL Server Management Studio.  
  
2.  Abra una nueva ventana de consulta y conéctese a la instancia de SQL Server 2016 del motor de base de datos de la máquina virtual de Azure.  
  
3.  Copie y pegue el siguiente script de Transact-SQL en la ventana de consulta. Modifique la dirección URL correctamente para su nombre de cuenta de almacenamiento y el contenedor que ha especificado en la lección 1 y, después, ejecute este script.  
  
    ```  
  
    -- To permit log backups, before the full database backup, modify the database to use the full recovery model.  
    USE master;  
    ALTER DATABASE AdventureWorks2014  
       SET RECOVERY FULL;  
  
    -- Back up the full AdventureWorks2014 database to the container that you created in Lesson 1  
    BACKUP DATABASE AdventureWorks2014   
       TO URL = 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/AdventureWorks2014_onprem.bak'  
  
    ```  
  
4.  Abra el Explorador de objetos y conéctese a Azure Storage con su cuenta de almacenamiento y la clave de la cuenta.  
  
5.  Expanda Contenedores, expanda el contenedor creado en la lección 1 y compruebe que la copia de seguridad del paso 3 aparece en este contenedor.  
  
    ![El archivo de copia de seguridad local aparece en forma de blob en el contenedor de Azure](../relational-databases/media/0d060e51-012f-4c61-ab8d-16d461d0ffad.JPG "El archivo de copia de seguridad local aparece en forma de blob en el contenedor de Azure")  
  
**Lección siguiente:**  
  
[Lección 4: Restaurar la base de datos a la máquina virtual desde la dirección URL](../relational-databases/lesson-4-restore-database-to-virtual-machine-from-url.md)  
  
