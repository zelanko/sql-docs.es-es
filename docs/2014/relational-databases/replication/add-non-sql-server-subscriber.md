---
title: Agregar suscriptor que no sea de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.newsubwizard.addnonsqlsubscriber.f1
ms.assetid: 21beeaa0-4b9e-48da-be63-1b9ff14e03d2
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: cc291a9677efe2acf875f5b5a37d9153fcb3eee3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62676928"
---
# <a name="add-non-sql-server-subscriber"></a>Agregar suscriptor que no sea de SQL Server
  La replicación admite la creación de publicaciones de inserción a publicaciones de instantáneas y transaccionales para suscriptores de Oracle e IBM DB2.  
  
## <a name="options"></a>Opciones  
 **Tipo de suscriptor que se agregará**  
 Seleccione un suscriptor de Oracle o IBM DB2. Para obtener más información sobre cómo admitir estos suscriptores, vea [Non-SQL Server Subscribers](non-sql/non-sql-server-subscribers.md) (Suscriptores que no son de SQL Server).  
  
 **Nombre del origen de datos**  
 Nombre utilizado para localizar la base de datos en una red. La replicación produce una cadena de conexión a la base de datos utilizando el nombre del origen de datos, combinado con el inicio de sesión, la contraseña y las opciones de conexión especificadas en la página **Seguridad del Agente de distribución** de este asistente.  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no valida el nombre del origen de datos y la cadena de conexión hasta que el Agente de distribución intenta inicializar la suscripción.  
  
## <a name="see-also"></a>Vea también  
 [Crear una suscripción para un suscriptor que no sea de SQL Server](create-a-subscription-for-a-non-sql-server-subscriber.md)   
 [Non-SQL Server Subscribers](non-sql/non-sql-server-subscribers.md)  (Suscriptores que no son de SQL Server)  
 [Suscribirse a publicaciones](subscribe-to-publications.md)  
  
  
