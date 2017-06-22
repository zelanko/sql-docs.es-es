---
title: "Información del servidor web | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rep.newsubwizard.webserverinformation.f1
ms.assetid: 86d72275-45c7-459f-98cf-f5a366ed279c
caps.latest.revision: 19
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 9c3db680206fb7c752fe27f968961d751c78aae0
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="web-server-information"></a>Información del servidor web
  Para usar la opción de sincronización web en la replicación de mezcla se necesita la información del servidor web. Para más información sobre cómo configurar la sincronización web, vea [Configurar la sincronización web](../../relational-databases/replication/configure-web-synchronization.md).  
  
## <a name="options"></a>Opciones  
 **Dirección del servidor web**  
 Si se especifica una dirección de servidor web en la página **Instantánea FTP e Internet** del cuadro de diálogo **Propiedades de la publicación**, aparecerá en este cuadro de texto de forma predeterminada. Puede aceptar la dirección predeterminada o escribir una dirección completa de servidor web para el servidor de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Information Services (IIS) que sincroniza la suscripción.  
  
 **¿Cómo se conectarán los suscriptores al servidor web?**  
 Especifique el tipo de autenticación usado para conectar con el servidor web. Se recomienda usar Autenticación básica para las conexiones con el servidor IIS junto con SSL (Capa de sockets seguros). Si selecciona Autenticación básica, escriba el nombre de inicio de sesión y la contraseña para conectar desde el suscriptor con el servidor IIS.  
  
## <a name="see-also"></a>Vea también  
 [Crear una suscripción de extracción](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Ver y modificar las propiedades de una suscripción de extracción](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [Suscriptores que no son de SQL Server](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)   
 [Suscribirse a publicaciones](../../relational-databases/replication/subscribe-to-publications.md)   
 [Web Synchronization for Merge Replication](../../relational-databases/replication/web-synchronization-for-merge-replication.md)  
  
  
