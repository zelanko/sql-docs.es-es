---
title: 'Propiedades del publicador: Distribuidor | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.rep.configdistwizard.distpubproperties.f1
helpviewer_keywords:
- Publisher Properties dialog box
ms.assetid: ab6ada76-0f99-43fe-b524-baac7b1bc483
caps.latest.revision: 19
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d6ed39a7bcfd48cbcaddbc0bfb90effd3b36d212
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="publisher-properties---distributor"></a>Propiedades del publicador: Distribuidor
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  El cuadro de diálogo **Propiedades del publicador** le permitirá ver y modificar las propiedades asociadas a la relación entre el publicador y el distribuidor.  
  
## <a name="options"></a>Opciones  
 **Conexión del agente al publicador**  
 Especifique el contexto en el que los siguientes agentes establecerán conexiones del distribuidor al publicador:  
  
-   Agente de lectura de cola para publicaciones transaccionales que permiten suscripciones de actualización en cola  
  
-   Agente de instantáneas y Agente de registro del LOG para publicaciones de Oracle  
  
 Seleccione **Suplantar cuenta de proceso del agente** para establecer conexiones al publicador a través del contexto de la cuenta de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows con la que se ejecutan los agentes o especifique **Autenticación de SQL Server**y escriba un valor para **Inicio de sesión** y **Contraseña**. Se recomienda seleccionar **Suplantar cuenta de proceso del agente**. Para obtener más información, vea [Modelo de seguridad del agente de replicación](../../relational-databases/replication/security/replication-agent-security-model.md).  
  
 Las cuentas de Windows con las que se ejecutan los agentes se especifican en el Asistente para nueva publicación. Podrá cambiar las cuentas:  
  
-   En el cuadro de diálogo **Propiedades del distribuidor** del Agente de lectura de cola.  
  
-   En el cuadro de diálogo **Propiedades de la publicación** del Agente de instantáneas y del Agente de registro del LOG.  
  
 **Varios**  
 Las propiedades **Tipo de publicador** y **Nombre de base de datos de distribución** son de solo lectura. Es posible cambiar la propiedad **Carpeta de instantáneas predeterminada** . Para obtener más información sobre la carpeta de instantáneas, vea [Proteger la carpeta de instantáneas](../../relational-databases/replication/security/secure-the-snapshot-folder.md).  
  
## <a name="see-also"></a>Ver también  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Ver y modificar las propiedades del distribuidor y del publicador](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [Referencia de propiedades &#40;replicación&#41;](../../relational-databases/replication/properties-reference-replication.md)  
  
  
