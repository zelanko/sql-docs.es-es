---
title: Configurar alertas para notificar los errores de directiva a los administradores de directivas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, configure alerts
ms.assetid: e8e60159-d5b0-49d5-91f3-af8e9cb994c1
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 57eb4f021a25fa2fa559fa7ff21d12bb621cc53a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "63126910"
---
# <a name="configure-alerts-to-notify-policy-administrators-of-policy-failures"></a>Configurar alertas para notificar los errores de directiva a los administradores de directivas
  Cuando las directivas de administración basada en directivas se ejecutan en uno de los tres modos de evaluación automatizados, si se produce la infracción de una directiva, se escribe un mensaje en el registro de eventos. Para que se le notifique cuando este mensaje se escribe en el registro de eventos, puede crear una alerta que se active al detectar el mensaje y permita realizar una acción. La alerta debería detectar los mensajes que se muestran en la tabla siguiente.  
  
|Modo de ejecución|Número de mensaje|  
|--------------------|--------------------|  
|Al cambiar: impedir<br /><br /> (si es Automático)|34050|  
|Al cambiar: impedir<br /><br /> (si es A petición)|34051|  
|Al programar|34052|  
|Al cambiar|34053|  
  
 Si desea configurar una alerta para responder a los mensajes de error de administración basada en directivas, vea los temas siguientes:  
  
-   [Crear un operador](../../ssms/agent/create-an-operator.md)  
  
-   [Crear una alerta con un número de error](../../ssms/agent/create-an-alert-using-an-error-number.md)  
  
-   [Asignar alertas a un operador](../../ssms/agent/assign-alerts-to-an-operator.md)  
  
## <a name="permissions"></a>Permisos  
 Cuando las directivas se evalúan a petición, se ejecutan en el contexto de seguridad del usuario. Para escribir en el registro de errores, el usuario debe tener los permisos ALTER TRACE o ser miembro del rol fijo de servidor sysadmin. Las directivas que evalúe un usuario que tenga menos privilegios no escribirán en el registro de eventos y no desencadenarán una alerta.  
  
 Los modos de ejecución automatizados se ejecutan como un miembro del rol sysadmin. Esto permite que la directiva se escriba en el registro de errores y se genere una alerta.  
  
## <a name="additional-considerations-about-alerts"></a>Consideraciones adicionales sobre las alertas  
 Tenga en cuenta las consideraciones adicionales siguientes acerca de las alertas:  
  
-   Las alertas solo se generan para las directivas que están habilitadas. Dado que las directivas **A petición** no pueden estar habilitadas, no se generan alertas para las directivas que se ejecutan a petición.  
  
-   Si la acción que desea tomar incluye enviar un mensaje de correo electrónico, debe configurar una cuenta de correo. Recomendamos usar Correo electrónico de base de datos. Para obtener más información sobre cómo configurar Correo electrónico de base de datos, vea [Crear una nueva cuenta de Correo electrónico de base de datos](../database-mail/create-a-database-mail-account.md).  
  
  
