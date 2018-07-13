---
title: 'Propiedades del publicador: Distribuidor | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.rep.configdistwizard.distpubproperties.f1
helpviewer_keywords:
- Publisher Properties dialog box
ms.assetid: ab6ada76-0f99-43fe-b524-baac7b1bc483
caps.latest.revision: 18
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 721b2030285f50ca2f7a1212b8589ebcb05957cd
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37164126"
---
# <a name="publisher-properties---distributor"></a>Propiedades del publicador: Distribuidor
  El cuadro de diálogo **Propiedades del publicador** le permitirá ver y modificar las propiedades asociadas a la relación entre el publicador y el distribuidor.  
  
## <a name="options"></a>Opciones  
 **Conexión del agente al publicador**  
 Especifique el contexto en el que los siguientes agentes establecerán conexiones del distribuidor al publicador:  
  
-   Agente de lectura de cola para publicaciones transaccionales que permiten suscripciones de actualización en cola  
  
-   Agente de instantáneas y Agente de registro del LOG para publicaciones de Oracle  
  
 Seleccione **Suplantar cuenta de proceso del agente** para establecer conexiones al publicador a través del contexto de la cuenta de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows con la que se ejecutan los agentes o especifique **Autenticación de SQL Server**y escriba un valor para **Inicio de sesión** y **Contraseña**. Se recomienda seleccionar **Suplantar cuenta de proceso del agente**. Para obtener más información, vea [Modelo de seguridad del agente de replicación](security/replication-agent-security-model.md).  
  
 Las cuentas de Windows con las que se ejecutan los agentes se especifican en el Asistente para nueva publicación. Podrá cambiar las cuentas:  
  
-   En el cuadro de diálogo **Propiedades del distribuidor** del Agente de lectura de cola.  
  
-   En el cuadro de diálogo **Propiedades de la publicación** del Agente de instantáneas y del Agente de registro del LOG.  
  
 **Varios**  
 Las propiedades **Tipo de publicador** y **Nombre de base de datos de distribución** son de solo lectura. Es posible cambiar la propiedad **Carpeta de instantáneas predeterminada** . Para obtener más información sobre la carpeta de instantáneas, vea [Proteger la carpeta de instantáneas](security/secure-the-snapshot-folder.md).  
  
## <a name="see-also"></a>Vea también  
 [Create a Publication](publish/create-a-publication.md)   
 [Ver y modificar las propiedades del distribuidor y del publicador](view-and-modify-distributor-and-publisher-properties.md)   
 [Referencia de propiedades &#40;replicación&#41;](properties-reference-replication.md)  
  
  
