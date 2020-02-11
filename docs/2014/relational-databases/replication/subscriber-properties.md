---
title: Propiedades del suscriptor | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.configdistwizard.subscribers.f1
helpviewer_keywords:
- Subscriber Properties dialog box
ms.assetid: 32aa0347-64e4-4aa4-ac57-6bd3e5d52070
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3142a78fcf3a2413e43b1a7598b5d3b282aba1c7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62629447"
---
# <a name="subscriber-properties"></a>Propiedades del suscriptor
  El cuadro de diálogo **propiedades del suscriptor** contiene información relevante para los suscriptores [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]ejecutan versiones de anteriores a.  
  
## <a name="options"></a>Opciones  
 **Conexión del agente al suscriptor**  
 Contexto bajo el que el Agente de distribución y el Agente de mezcla conectan desde el distribuidor al suscriptor. Se aplica solamente a versiones anteriores a [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
 Seleccione **Suplantar cuenta de proceso del agente** para establecer conexiones al suscriptor a través del contexto de la cuenta del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el distribuidor, o especifique **Autenticación de SQL Server**y escriba un valor para **Inicio de sesión** y **Contraseña**. [!INCLUDE[msCoName](../../includes/msconame-md.md)]recomienda seleccionar **Suplantar cuenta de proceso del agente**.  
  
 En [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y versiones posteriores la información de conexión se especifica para cada suscripción en el Asistente para nueva suscripción y puede cambiar en el cuadro de diálogo **Propiedades de suscripción** .  
  
 **Programaciones predeterminadas del agente**  
 Programación predeterminada utilizada en el Asistente para nueva suscripción para suscriptores que ejecutan versiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anteriores a [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)].  
  
 **Varios**  
 Incluye información sobre el suscriptor y el tipo de suscriptor.  
  
## <a name="see-also"></a>Consulte también  
 [Ver y modificar las propiedades del distribuidor y del publicador](view-and-modify-distributor-and-publisher-properties.md)   

 [Suscribirse a publicaciones](subscribe-to-publications.md)  
  
  
