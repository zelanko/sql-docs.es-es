---
description: Información del servidor web
title: Información del servidor web | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.newsubwizard.webserverinformation.f1
ms.assetid: 86d72275-45c7-459f-98cf-f5a366ed279c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 7ba110489a2ec2623018563257953d764ef371c2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88325952"
---
# <a name="web-server-information"></a>Información del servidor web
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Para usar la opción de sincronización web en la replicación de mezcla se necesita la información del servidor web. Para más información sobre cómo configurar la sincronización web, vea [Configurar la sincronización web](../../relational-databases/replication/configure-web-synchronization.md).  
  
## <a name="options"></a>Opciones  
 **Dirección del servidor web**  
 Si se especifica una dirección de servidor web en la página **Instantánea FTP e Internet** del cuadro de diálogo **Propiedades de la publicación**, aparecerá en este cuadro de texto de forma predeterminada. Puede aceptar la dirección predeterminada o escribir una dirección completa de servidor web para el servidor de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Information Services (IIS) que sincroniza la suscripción.  
  
 **¿Cómo se conectarán los suscriptores al servidor web?**  
 Especifique el tipo de autenticación usado para conectar con el servidor web. Se recomienda usar la autenticación básica para las conexiones con el servidor IIS junto con la Seguridad de la capa de transporte (TLS), anteriormente conocida como Capa de sockets seguros (SSL). Si selecciona Autenticación básica, escriba el nombre de inicio de sesión y la contraseña para conectar desde el suscriptor con el servidor IIS.  
  
## <a name="see-also"></a>Consulte también  
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [View and Modify Pull Subscription Properties](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)  (Ver y modificar las propiedades de una suscripción de extracción)  
 [Non-SQL Server Subscribers](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)   
 [Subscribe to Publications](../../relational-databases/replication/subscribe-to-publications.md)   
 [Sincronización web para la replicación de mezcla](../../relational-databases/replication/web-synchronization-for-merge-replication.md)  
  
  
