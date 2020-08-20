---
description: Seguridad del Agente de mezcla
title: Seguridad del Agente de mezcla | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.security.MA.f1
helpviewer_keywords:
- Merge Agent Security dialog box
ms.assetid: 9b86171a-4381-4b39-869a-cdc161e7cd15
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6d571e5b41937947e0c6d03e5d1a84fe0dc88e8b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465277"
---
# <a name="merge-agent-security"></a>Seguridad del Agente de mezcla
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
   El cuadro de diálogo **Seguridad del Agente de mezcla** permite especificar la cuenta de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows en la que se ejecuta el Agente de mezcla. El Agente de mezcla se ejecuta en el distribuidor para las suscripciones de inserción y en el suscriptor para las suscripciones de extracción. La cuenta de Windows se denomina también *cuenta de proceso*porque el proceso del agente se ejecuta con dicha cuenta. Las opciones adicionales disponibles en el cuadro de diálogo dependen de cómo se tenga acceso al mismo:  
  
-   Si se tiene acceso al cuadro de diálogo desde el Asistente para nueva suscripción, también permite especificar el contexto para el que el Agente de mezcla realiza las conexiones con el suscriptor (para suscripciones de inserción) o con el publicador y el distribuidor (para las suscripciones de extracción). La conexión puede realizarse con la cuenta Windows o en el contexto de una cuenta de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que especifique.  
  
-   Si se tiene acceso al cuadro de diálogo desde el cuadro de diálogo **Propiedades de suscripción** , se debe especificar el contexto en que el Agente de mezcla realiza las conexiones haciendo clic en el botón de propiedades (**...**) de la fila **Conexión de suscriptor** o **Conexión de publicador** de dicho cuadro de diálogo. Para más información sobre cómo acceder al cuadro de diálogo **Propiedades de suscripción**, vea [Ver y modificar las propiedades de una suscripción de inserción](../../relational-databases/replication/view-and-modify-push-subscription-properties.md) y [Ver y modificar las propiedades de una suscripción de extracción](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md).  
  
 Todas las cuentas deben ser válidas y se debe especificar la contraseña correcta para cada cuenta. Las cuentas y las contraseñas se validan cuando se ejecuta el agente.  
  
## <a name="options"></a>Opciones  
 **Process Account**  
 Escriba la cuenta de Windows con la que se ejecutará el Agente de mezcla.  
  
-   Para las suscripciones de inserción, la cuenta debe:  
  
    -   Ser como mínimo miembro del rol fijo de base de datos **db_owner** en la base de datos de distribución.  
  
    -   Ser miembro de la PAL.  
  
    -   Ser un inicio de sesión asociado a un usuario en la base de datos de publicaciones.  
  
    -   Tener permisos de lectura en el recurso compartido de instantáneas.  
  
-   Para las suscripciones de extracción, la cuenta debe ser como mínimo miembro del rol fijo de base de datos **db_owner** en la base de datos de suscripciones.  
  
 Si se suplanta la cuenta de proceso al realizar las conexiones serán necesarios permisos adicionales. Vea las secciones **Conectar al publicador y distribuidor** y **Conectar al suscriptor** a continuación.  
  
 No se puede especificar **Cuenta de proceso** para las suscripciones de extracción a [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], ya que el Agente de mezcla no se ejecuta en instancias de [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)].  
  
 **Contraseña** y **Confirmar contraseña**  
 Escriba la contraseña de la cuenta de Windows.  
  
 **Conectar al publicador y distribuidor**  
 Para las suscripciones de inserción, las conexiones con el publicador y el distribuidor siempre se realizan suplantando la cuenta especificada en el cuadro de texto **Cuenta de proceso** .  
  
 Para las suscripciones de extracción, debe elegir si el Agente de mezcla debe realizar las conexiones con el publicador y el distribuidor mediante la suplantación de la cuenta especificada en el cuadro de texto **Cuenta de proceso** o bien usar una cuenta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Si selecciona utilizar una cuenta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , especifique una contraseña y un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomienda que se seleccione la opción de suplantar la cuenta de Windows en lugar de utilizar una cuenta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 La cuenta de Windows o la cuenta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usada para la conexión debe:  
  
-   Ser miembro de la PAL.  
  
-   Ser un inicio de sesión asociado a un usuario en la base de datos de publicaciones.  
  
-   Ser un inicio de sesión asociado a un usuario en la base de datos de distribución (el usuario puede ser el usuario Guest).  
  
-   Tener permisos de lectura en el recurso compartido de instantáneas.  
  
 **Conectar al suscriptor**  
 Para las suscripciones de extracción, las conexiones con el suscriptor siempre se realizan suplantando la cuenta especificada en el cuadro de texto **Cuenta de proceso** .  
  
 Para las suscripciones de inserción, debe elegir si el Agente de mezcla debe realizar las conexiones con el publicador y el distribuidor mediante la suplantación de la cuenta especificada en el cuadro de texto **Cuenta de proceso** o mediante una cuenta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Si selecciona utilizar una cuenta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , especifique una contraseña y un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  Se recomienda usar la suplantación de la cuenta de Windows en lugar de usar una cuenta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 La cuenta de Windows o la cuenta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usada para la conexión con el suscriptor debe ser como mínimo miembro del rol fijo de base de datos **db_owner** en la base de datos de suscripciones.  
  
## <a name="see-also"></a>Vea también  
 [Administrar inicios de sesión y contraseñas en la replicación](../../relational-databases/replication/security/identity-and-access-control-replication.md)   
 [Modelo de seguridad del Agente de replicación](../../relational-databases/replication/security/replication-agent-security-model.md)   
 [Replication Agents Overview](../../relational-databases/replication/agents/replication-agents-overview.md)  (Información general sobre los agentes de replicación)  
 [Replication Security Best Practices](../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Suscribirse a publicaciones](../../relational-databases/replication/subscribe-to-publications.md)  
  
  
