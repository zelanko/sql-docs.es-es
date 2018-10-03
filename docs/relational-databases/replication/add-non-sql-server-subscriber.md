---
title: Agregar suscriptor que no sea de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.newsubwizard.addnonsqlsubscriber.f1
ms.assetid: 21beeaa0-4b9e-48da-be63-1b9ff14e03d2
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 423a744d7d7a16d17ae1574b108ce651cbcc03bf
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47603063"
---
# <a name="add-non-sql-server-subscriber"></a>Agregar suscriptor que no sea de SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  La replicación admite la creación de publicaciones de inserción a publicaciones de instantáneas y transaccionales para suscriptores de Oracle e IBM DB2.  
  
## <a name="options"></a>Opciones  
 **Tipo de suscriptor que se agregará**  
 Seleccione un suscriptor de Oracle o IBM DB2. Para obtener más información sobre cómo admitir estos suscriptores, vea [Non-SQL Server Subscribers](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md) (Suscriptores que no son de SQL Server).  
  
 **Nombre del origen de datos**  
 Nombre utilizado para localizar la base de datos en una red. La replicación produce una cadena de conexión a la base de datos utilizando el nombre del origen de datos, combinado con el inicio de sesión, la contraseña y las opciones de conexión especificadas en la página **Seguridad del Agente de distribución** de este asistente.  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no valida el nombre del origen de datos y la cadena de conexión hasta que el Agente de distribución intenta inicializar la suscripción.  
  
## <a name="see-also"></a>Ver también  
 [Crear una suscripción para un suscriptor que no sea de SQL Server](../../relational-databases/replication/create-a-subscription-for-a-non-sql-server-subscriber.md)   
 [Non-SQL Server Subscribers](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)  (Suscriptores que no son de SQL Server)  
 [Suscribirse a publicaciones](../../relational-databases/replication/subscribe-to-publications.md)  
  
  
