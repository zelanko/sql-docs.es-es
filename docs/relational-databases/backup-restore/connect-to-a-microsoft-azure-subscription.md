---
title: "Conexión a una suscripción de Microsoft Azure | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: backup-restore
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: cca5a270-643f-4677-8802-98464f19f82a
caps.latest.revision: 
author: dagiro
ms.author: v-dagir
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a4bcc3df84094ff17bf2239e278f559458a7a568
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/18/2018
---
# <a name="connect-to-a-microsoft-azure-subscription"></a>Connect to a Microsoft Azure Subscription (Conectarse a una suscripción de Microsoft Azure)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Use **Connect to a Microsoft Azure Subscription** (Conectarse a una suscripción de Microsoft) para registrar un contenedor de blobs de Azure existente con la instancia de SQL Server.  El cuadro de diálogo creará una firma de acceso compartido y una directiva de acceso almacenada en un contenedor de blobs de Azure y, seguidamente, creará una credencial de SQL Server.  Este cuadro de diálogo aparece cuando se usa la tarea de copia de seguridad y restauración de SQL Server Management Studio y en dicha operación participa un dispositivo URL.

## <a name="limitation"></a>Limitación
La opción**Connect to a Microsoft Azure Subscription (Conectarse a una suscripción de Microsoft)** funciona únicamente con una cuenta de almacenamiento de Azure creada a través del modelo de implementación de administración de servicios (Clásico).  Para obtener más información sobre los modelos de implementación de Azure, vea [La implementación de Azure Resource Manager frente a la implementación clásica: los modelos de implementación y el estado de los recursos](https://azure.microsoft.com/en-us/documentation/articles/resource-manager-deployment-model/).

## <a name="options"></a>.
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
