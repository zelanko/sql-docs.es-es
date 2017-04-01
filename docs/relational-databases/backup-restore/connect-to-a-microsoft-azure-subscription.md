---
title: "Connect to a Microsoft Azure Subscription (Conectarse a una suscripci&#243;n de Microsoft Azure) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-backup-restore"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: cca5a270-643f-4677-8802-98464f19f82a
caps.latest.revision: 4
author: "dagiro"
ms.author: "v-dagir"
manager: "jhubbard"
caps.handback.revision: 4
---
# Connect to a Microsoft Azure Subscription (Conectarse a una suscripci&#243;n de Microsoft Azure)
Use **Connect to a Microsoft Azure Subscription (Conectarse a una suscripción de Microsoft)** para registrar un contenedor de blobs de Azure existente con la instancia de SQL Server.  El cuadro de diálogo creará una firma de acceso compartido y una directiva de acceso almacenada en un contenedor de blobs de Azure y, seguidamente, creará una credencial de SQL Server.  Este cuadro de diálogo aparece cuando se usa la tarea de copia de seguridad y restauración de SQL Server Management Studio y en dicha operación participa un dispositivo URL.

## Limitación
La opción **Connect to a Microsoft Azure Subscription (Conectarse a una suscripción de Microsoft)** funciona únicamente con una cuenta de almacenamiento de Azure creada a través del modelo de implementación de administración de servicios (Clásico).  Para obtener más información sobre los modelos de implementación de Azure, vea [La implementación de Azure Resource Manager frente a la implementación clásica: los modelos de implementación y el estado de los recursos](https://azure.microsoft.com/en-us/documentation/articles/resource-manager-deployment-model/).

## Opciones
**Iniciar sesión**     
Permite iniciar sesión con la cuenta de Azure apropiada.

**Seleccionar una suscripción que usar**      
Permite elegir la suscripción que se prefiera de la lista desplegable.

**Seleccionar una cuenta de almacenamiento**  
Permite elegir la cuenta de almacenamiento que se prefiera de la lista desplegable.

**Seleccionar contenedor de blobs**   
Permite elegir el contenedor de blobs que se prefiera de la lista desplegable.

**Expiración de la directiva de acceso compartido**   
La directiva de acceso compartido expirará en la fecha que se indique.  La fecha de expiración predeterminada es de un año desde el momento de la creación.  Modifíquela como considere oportuno.

**Firma de acceso compartido generada**   
Este cuadro de texto enriquecido mostrará la firma de acceso compartido generada.

**Crear credencial**   
Este botón generará una directiva de acceso almacenada y una firma de acceso compartido y, luego, creará una credencial de SQL Server.
