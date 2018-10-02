---
title: 'Lección 2: Creación de una credencial de SQL Server con una firma de acceso compartido | Microsoft Docs'
ms.custom: ''
ms.date: 02/25/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 29e57ebd-828f-4dff-b473-c10ab0b1c597
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: cee571e8076628f1868c5ccf8d6940471363dc5d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47830013"
---
# <a name="lesson-2-create-a-sql-server-credential-using-a-shared-access-signature"></a>Lección 2: Crear una credencial de SQL Server con una firma de acceso compartido
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
En esta lección, creará una credencial para almacenar la información de seguridad que SQL Server usará para escribir y leer desde el contenedor de Azure que ha creado en la [Lección 1: Crear una directiva de acceso almacenada y una firma de acceso compartido en un contenedor de Azure](../relational-databases/lesson-1-create-stored-access-policy-and-shared-access-signature.md).  
  
Una credencial de SQL Server es un objeto que se usa para almacenar la información de autenticación necesaria para conectarse a un recurso fuera de SQL Server. La credencial almacena la ruta de acceso URI de la firma de acceso compartido y del contenedor de almacenamiento de este contenedor.  
  
> [!NOTE]  
> Si quiere realizar una copia de seguridad de una base de datos SQL Server 2012 SP1 CU2 o posterior o de una base de datos de SQL Server 2014 a este contenedor de Azure, puede usar la [sintaxis desusada](https://technet.microsoft.com/library/dn435916(v=sql.120).aspx) que aparece aquí para crear una credencial de SQL Server basada en la clave de la cuenta de almacenamiento.  
  
## <a name="create-sql-server-credential"></a>Crear una credencial de SQL Server  
Para crear una credencial de SQL Server, siga estos pasos:  
  
1.  Conéctese a SQL Server Management Studio.  
  
2.  Abra una nueva ventana de consulta y conéctese a la instancia de SQL Server 2016 del motor de base de datos en su entorno local.  
  
3.  En la nueva ventana de consulta, pegue la instrucción CREATE CREDENTIAL con la firma de acceso compartido de la lección 1 y ejecute el script.  
  
    El script tendrá un aspecto similar al código siguiente.  
  
    ```Transact-SQL  
  
    USE master  
    CREATE CREDENTIAL [https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>] -- this name must match the container path, start with https and must not contain a forward slash.  
       WITH IDENTITY='SHARED ACCESS SIGNATURE' -- this is a mandatory string and do not change it.   
       , SECRET = 'sharedaccesssignature' -- this is the shared access signature key that you obtained in Lesson 1.   
    GO  
  
    ```  
  
4.  Para ver todas las credenciales disponibles, puede ejecutar la siguiente instrucción en una ventana de consulta conectada a su instancia:  
  
    ```Transact-SQL  
    SELECT * from sys.credentials  
    ```  
  
5.  Abra una nueva ventana de consulta y conéctese a la instancia de SQL Server 2016 del motor de base de datos de la máquina virtual de Azure.  
  
6.  En la nueva ventana de consulta, pegue la instrucción CREATE CREDENTIAL con la firma de acceso compartido de la lección 1 y ejecute el script.  
  
7.  Repita los pasos 5 y 6 para cualquier instancia de SQL Server 2016 adicional que quiere que tenga acceso al contenedor de Azure.  
  
**Lección siguiente:**  
  
[Lección 3: Copia de seguridad de base de datos en la dirección URL](../relational-databases/lesson-3-database-backup-to-url.md)  
  
## <a name="see-also"></a>Ver también  
[Credenciales &#40;motor de base de datos&#41;](../relational-databases/security/authentication-access/credentials-database-engine.md)  
[CREATE CREDENTIAL &#40;Transact-SQL&#41;](../t-sql/statements/create-credential-transact-sql.md)  
[sys.credentials &#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)  
  

