---
title: 'Lección 2: Crear una directiva en el contenedor y generar una clave de firma de acceso compartido (SAS) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 41674d9d-8132-4bff-be4d-85a861419f3d
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c9efb23d15b4f72375077f4bbf1450d8c47fddf4
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2019
ms.locfileid: "70153845"
---
# <a name="lesson-2-create-a-policy-on-container-and-generate-a-shared-access-signature-sas-key"></a>Lección 2: Crear una directiva en el contenedor y generar una clave de firma de acceso compartido (SAS)
  En esta lección, aprenderá a crear una directiva en el contenedor de blobs y también a generar una clave SAS.  
  
 Una directiva de acceso almacenada proporciona un nivel de control adicional sobre las firmas de acceso compartidas en el servidor. Una firma de acceso compartido es un URI que concede derechos de acceso restringidos a los contenedores, los blobs, las colas y las tablas. Al utilizar esta nueva mejora, debe crear una directiva en un contenedor con derechos de lectura, escritura y enumeración.  
  
 Puede crear una directiva y una firma de acceso compartido mediante uno de los métodos siguientes:  
  
-   Operaciones de la API de REST de Azure: [Crear contenedor](https://msdn.microsoft.com/library/azure/dd179468.aspx), [establecer la ACL del contenedor](https://msdn.microsoft.com/library/azure/dd179391.aspx)y [obtener la ACL del contenedor](https://msdn.microsoft.com/library/azure/dd179469.aspx).  
  
-   [Método CloudBlobContainer. GetSharedAccessSignature](https://docs.microsoft.com/dotnet/api/microsoft.azure.storage.blob.cloudblobcontainer.getsharedaccesssignature) en el SDK de Azure.  
  
    ```  
  
       string signature = blob.GetSharedAccessSignature(new SharedAccessPolicy()   
        {   
            // Specify the expiration time for the signature.   
            SharedAccessExpiryTime = DateTime.Now.Years(1),   
            // Specify the permissions granted by the signature.    
            Permissions = SharedAccessPermissions.Write | SharedAccessPermissions.Read   
        });  
  
    ```  
  
-   Una herramienta de Azure Explorer de terceros, como [Explorador de Azure Storage](http://azurestorageexplorer.codeplex.com/).  
  
 **Lección siguiente:**  
  
 [Lección 3: Crear una credencial de SQL Server](../relational-databases/lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md)  
  
  
