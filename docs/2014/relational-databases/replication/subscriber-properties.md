---
title: Propiedades del suscriptor | Microsoft Docs
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
- sql12.rep.configdistwizard.subscribers.f1
helpviewer_keywords:
- Subscriber Properties dialog box
ms.assetid: 32aa0347-64e4-4aa4-ac57-6bd3e5d52070
caps.latest.revision: 21
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 46c53e1f86bcdc21ff2e75d82de6343463f5c6ca
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37262361"
---
# <a name="subscriber-properties"></a>Propiedades del suscriptor
  El cuadro de diálogo **Propiedades del suscriptor** contiene información importante de los suscriptores que ejecutan versiones de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anteriores a [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
## <a name="options"></a>Opciones  
 **Conexión del agente al suscriptor**  
 Contexto bajo el que el Agente de distribución y el Agente de mezcla conectan desde el distribuidor al suscriptor. Se aplica solamente a versiones anteriores a [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
 Seleccione **Suplantar cuenta de proceso del agente** para establecer conexiones al suscriptor a través del contexto de la cuenta del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el distribuidor, o especifique **Autenticación de SQL Server**y escriba un valor para **Inicio de sesión** y **Contraseña**. [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomienda que se seleccione **Suplantar cuenta de proceso del agente**.  
  
 En [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y versiones posteriores la información de conexión se especifica para cada suscripción en el Asistente para nueva suscripción y puede cambiar en el cuadro de diálogo **Propiedades de suscripción** .  
  
 **Programaciones predeterminadas del agente**  
 Programación predeterminada utilizada en el Asistente para nueva suscripción para suscriptores que ejecutan versiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anteriores a [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)].  
  
 **Varios**  
 Incluye información sobre el suscriptor y el tipo de suscriptor.  
  
## <a name="see-also"></a>Vea también  
 [Ver y modificar las propiedades del distribuidor y del publicador](view-and-modify-distributor-and-publisher-properties.md)   
 [Referencia de propiedades &#40;replicación&#41;](properties-reference-replication.md)   
 [Suscribirse a publicaciones](subscribe-to-publications.md)  
  
  
