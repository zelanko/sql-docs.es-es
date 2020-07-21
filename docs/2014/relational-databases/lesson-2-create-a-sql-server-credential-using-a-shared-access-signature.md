---
title: 'Lección 3: crear una credencial de SQL Server | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 29e57ebd-828f-4dff-b473-c10ab0b1c597
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 808438e544e3beb18b2e2afa9c399b5666277483
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85025064"
---
# <a name="lesson-3-create-a-sql-server-credential"></a>Lección 3: Crear una credencial de SQL Server
  En esta lección, creará una credencial para almacenar la información de seguridad que se usa para acceder a la cuenta de almacenamiento de Azure.  
  
 Una credencial de SQL Server es un objeto que se usa para almacenar la información de autenticación necesaria para conectarse a un recurso fuera de SQL Server. La credencial almacena la ruta de acceso de URI de los valores clave de la signatura de acceso compartida y el contenedor de almacenamiento. Para cada contenedor de almacenamiento utilizado por un archivo de datos o de registro, debe crear una credencial de SQL Server cuyo nombre coincida con la ruta de acceso del contenedor.  
  
 Para obtener información general sobre las credenciales, vea [credenciales &#40;Motor de base de datos&#41;](security/authentication-access/credentials-database-engine.md).  
  
> [!IMPORTANT]  
>  Los requisitos para crear una credencial SQL Server que se describe a continuación son específicos de la característica [archivos de datos de SQL Server en Azure](databases/sql-server-data-files-in-microsoft-azure.md) . Para información sobre cómo crear credenciales para los procesos de copias de seguridad en el almacenamiento de Azure, vea [Lesson 2: Create a SQL Server Credential](../tutorials/lesson-2-create-a-sql-server-credential.md).  
  
 Para crear una credencial de SQL Server, siga estos pasos:  
  
1.  Conéctese a SQL Server Management Studio.  
  
2.  En el Explorador de objetos, conéctese a la instancia del Motor de base de datos instalado.  
  
3.  En la barra de herramientas Estándar, haga clic en Nueva consulta.  
  
4.  Copie y pegue el ejemplo siguiente en la ventana de consulta, y modifíquelo como sea necesario. La siguiente instrucción creará una credencial SQL Server para almacenar el certificado de acceso compartido del contenedor de almacenamiento.  
  
    ```sql  
  
    USE master  
    CREATE CREDENTIAL credentialname - this name should match the container path and it must start with https.   
       WITH IDENTITY='SHARED ACCESS SIGNATURE', -- this is a mandatory string and do not change it.   
       SECRET = 'sharedaccesssignature' -- this is the shared access signature key that you obtained in Lesson 2.   
    GO  
  
    ```  
  
     Para obtener información detallada, consulte [Create CREDENTIAL &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-credential-transact-sql) en libros en pantalla de SQL Server.  
  
5.  Para ver todas las credenciales disponibles, puede ejecutar la siguiente instrucción en la ventana de consulta:  
  
    ```sql  
    SELECT * from sys.credentials  
    ```  
  
     Para obtener más información sobre sys. Credentials, vea [Sys. credentials &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-credentials-transact-sql) en libros en pantalla de SQL Server.  
  
 **Lección siguiente:**  
  
 [Lección 4: Crear una base de datos en Azure Storage](lesson-3-database-backup-to-url.md)  
  
  
