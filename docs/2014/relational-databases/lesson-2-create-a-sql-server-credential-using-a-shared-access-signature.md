---
title: 'Lección 3: Crear una credencial de SQL Server | Documentos de Microsoft'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 29e57ebd-828f-4dff-b473-c10ab0b1c597
caps.latest.revision: 7
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 201863a1df64cdc85ef41a55170948dbf4eba419
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36201366"
---
# <a name="lesson-3-create-a-sql-server-credential"></a>Lección 3: Crear una credencial de SQL Server
  En esta lección, creará una credencial para almacenar la información de seguridad usada para tener acceso a la cuenta de almacenamiento de Windows Azure.  
  
 Una credencial de SQL Server es un objeto que se usa para almacenar la información de autenticación necesaria para conectarse a un recurso fuera de SQL Server. La credencial almacena la ruta de acceso de URI de los valores clave de la signatura de acceso compartida y el contenedor de almacenamiento. Para cada contenedor de almacenamiento utilizado por un archivo de datos o de registro, debe crear una credencial de SQL Server cuyo nombre coincida con la ruta de acceso del contenedor.  
  
 Para obtener información general acerca de las credenciales, vea [credenciales &#40;motor de base de datos&#41;](security/authentication-access/credentials-database-engine.md).  
  
> [!IMPORTANT]  
>  Los requisitos para crear una credencial de SQL Server que se describe a continuación son específicos para la [archivos de datos de SQL Server en Windows Azure](databases/sql-server-data-files-in-microsoft-azure.md) característica. Para obtener información sobre cómo crear credenciales para los procesos de copia de seguridad en almacenamiento de Azure, consulte [lección 2: crear una credencial de SQL Server](../tutorials/lesson-2-create-a-sql-server-credential.md).  
  
 Para crear una credencial de SQL Server, siga estos pasos:  
  
1.  Conéctese a SQL Server Management Studio.  
  
2.  En el Explorador de objetos, conéctese a la instancia del Motor de base de datos instalado.  
  
3.  En la barra de herramientas Estándar, haga clic en Nueva consulta.  
  
4.  Copie y pegue el ejemplo siguiente en la ventana de consulta, y modifíquelo como sea necesario. La instrucción siguiente creará una credencial de SQL Server para almacenar el certificado de Acceso compartido del contenedor de almacenamiento.  
  
    ```tsql  
  
    USE master  
    CREATE CREDENTIAL credentialname – this name should match the container path and it must start with https.   
       WITH IDENTITY='SHARED ACCESS SIGNATURE', -- this is a mandatory string and do not change it.   
       SECRET = 'sharedaccesssignature' –- this is the shared access signature key that you obtained in Lesson 2.   
    GO  
  
    ```  
  
     Para obtener información detallada, vea [CREATE CREDENTIAL &#40;Transact-SQL&#41; ](/sql/t-sql/statements/create-credential-transact-sql) en libros en pantalla de SQL Server.  
  
5.  Para ver todas las credenciales disponibles, puede ejecutar la siguiente instrucción en la ventana de consulta:  
  
    ```tsql  
    SELECT * from sys.credentials  
    ```  
  
     Para obtener más información sobre sys.credentials, vea [sys.credentials &#40;Transact-SQL&#41; ](/sql/relational-databases/system-catalog-views/sys-credentials-transact-sql) en libros en pantalla de SQL Server.  
  
 **Lección siguiente:**  
  
 [Lección 4: Crear una base de datos en almacenamiento de Windows Azure](lesson-3-database-backup-to-url.md)  
  
  
