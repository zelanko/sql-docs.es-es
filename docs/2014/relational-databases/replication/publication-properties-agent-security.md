---
title: Propiedades de la publicación, Seguridad del agente | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.rep.newpubwizard.pubproperties.agentsecurity.f1
ms.assetid: 03945aac-66f2-4370-b5d1-c1de694bc4c1
caps.latest.revision: 20
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 2b72ec15e139ee164e74589ce70db4e193972ee0
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36200094"
---
# <a name="publication-properties-agent-security"></a>Propiedades de la publicación, Seguridad del agente
  La página **Seguridad del agente** del cuadro de diálogo **Propiedades de la publicación** permite obtener acceso a la configuración de las cuentas en las que se ejecutan los siguientes agentes y realizar conexiones con los equipos de una topología de replicación:  
  
-   Agente de instantáneas para todas las publicaciones.  
  
-   Agente de registro del LOG para todas las publicaciones transaccionales. Existe un Agente de registro del LOG para cada base de datos publicada para la replicación transaccional. Si se cambia la configuración del Agente de registro del LOG, esto afectará a todas las publicaciones transaccionales de una base de datos.  
  
-   Agente de lectura de cola para publicaciones transaccionales que permiten suscripciones de actualización en cola Existe un Agente de lectura de cola para cada base de datos de distribución. Si se cambia la configuración del Agente de lectura de cola, esto afecta a todas las publicaciones transaccionales con suscripciones de actualización en cola que utilizan la misma base de datos de distribución. Para obtener más información sobre la configuración de seguridad del Agente de lectura de cola de replicación, vea [Ver y modificar la configuración de seguridad de la replicación](security/view-and-modify-replication-security-settings.md).  
  
 Para obtener más información sobre la configuración de seguridad y los permisos necesarios para cada agente, vea [Replication Agent Security Model](security/replication-agent-security-model.md).  
  
## <a name="options"></a>Opciones  
 **Configuración de seguridad** o **Crear agente**  
 Si se ha creado un trabajo de agente, haga clic en **Configuración de seguridad** para obtener acceso al cuadro de diálogo que permite cambiar la configuración de seguridad de un agente. Si no se ha creado el trabajo de agente, haga clic en **Crear agente** para crear uno y especifique la configuración de seguridad correspondiente.  
  
## <a name="see-also"></a>Vea también  
 [Create a Publication](publish/create-a-publication.md)   
 [Ver y modificar propiedades de publicación](publish/view-and-modify-publication-properties.md)   
 [Publicar datos y objetos de base de datos](publish/publish-data-and-database-objects.md)   
 [Replication Security Best Practices](security/replication-security-best-practices.md)   
 [Seguridad y protección &#40;Replicación&#41;](security/security-and-protection-replication.md)  
  
  