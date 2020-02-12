---
title: Seguridad del Agente de mezcla | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.security.MA.f1
helpviewer_keywords:
- Merge Agent Security dialog box
ms.assetid: 9b86171a-4381-4b39-869a-cdc161e7cd15
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: af3d3490957114d6ba7731b49435dc7e90122f90
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62932494"
---
# <a name="merge-agent-security"></a>Seguridad del Agente de mezcla
  El cuadro de diálogo **seguridad de agente de mezcla** permite especificar la [!INCLUDE[msCoName](../../includes/msconame-md.md)] cuenta de Windows con la que se ejecuta el agente de mezcla. El Agente de mezcla se ejecuta en el distribuidor para las suscripciones de inserción y en el suscriptor para las suscripciones de extracción. También se hace referencia a la cuenta de Windows como *cuenta de proceso*, ya que el proceso del agente se ejecuta en esta cuenta. Las opciones adicionales disponibles en el cuadro de diálogo dependen de cómo se tenga acceso al mismo:  
  
-   Si se tiene acceso al cuadro de diálogo desde el Asistente para nueva suscripción, también permite especificar el contexto para el que el Agente de mezcla realiza las conexiones con el suscriptor (para suscripciones de inserción) o con el publicador y el distribuidor (para las suscripciones de extracción). La conexión se puede realizar mediante la cuenta de Windows o en el contexto de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] una cuenta que especifique.  
  
-   Si se tiene acceso al cuadro de diálogo desde el cuadro de diálogo **Propiedades de suscripción** , se debe especificar el contexto en que el Agente de mezcla realiza las conexiones haciendo clic en el botón de propiedades (**...**) de la fila **Conexión de suscriptor** o **Conexión de publicador** de dicho cuadro de diálogo. Para más información sobre cómo acceder al cuadro de diálogo **Propiedades de suscripción**, vea [Ver y modificar las propiedades de una suscripción de inserción](view-and-modify-push-subscription-properties.md) y [Ver y modificar las propiedades de una suscripción de extracción](view-and-modify-pull-subscription-properties.md).  
  
 Todas las cuentas deben ser válidas y se debe especificar la contraseña correcta para cada cuenta. Las cuentas y las contraseñas se validan cuando se ejecuta el agente.  
  
## <a name="options"></a>Opciones  
 **Cuenta de proceso**  
 Escriba la cuenta de Windows con la que se ejecutará el Agente de mezcla.  
  
-   Para las suscripciones de inserción, la cuenta debe:  
  
    -   Ser, como mínimo, miembro del rol fijo de base de datos **db_owner** en la base de datos de distribución.  
  
    -   Ser miembro de la PAL.  
  
    -   Ser un inicio de sesión asociado a un usuario en la base de datos de publicaciones.  
  
    -   Tener permisos de lectura en el recurso compartido de instantáneas.  
  
-   Para las suscripciones de extracción, la cuenta debe ser como mínimo miembro del rol fijo de base de datos **db_owner** en la base de datos de suscripciones.  
  
 Si se suplanta la cuenta de proceso al realizar las conexiones serán necesarios permisos adicionales. Vea las secciones **Conectar al publicador y distribuidor** y **Conectar al suscriptor** a continuación.  
  
 No se puede especificar la **cuenta de proceso** para las suscripciones de extracción [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]en, porque el agente de mezcla no [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]se ejecuta en instancias de.  
  
 **Contraseña** y **Confirmar contraseña**  
 Escriba la contraseña de la cuenta de Windows.  
  
 **Conectar con el publicador y el distribuidor**  
 Para las suscripciones de inserción, las conexiones con el publicador y el distribuidor siempre se realizan suplantando la cuenta especificada en el cuadro de texto **Cuenta de proceso** .  
  
 Para las suscripciones de extracción, debe elegir si el Agente de mezcla debe realizar las conexiones con el publicador y el distribuidor mediante la suplantación de la cuenta especificada en el cuadro de texto **Cuenta de proceso** o bien usar una cuenta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Si selecciona utilizar una cuenta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , especifique una contraseña y un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomienda que se seleccione la opción de suplantar la cuenta de Windows en lugar de utilizar una cuenta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 La cuenta de Windows o la cuenta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usada para la conexión debe:  
  
-   Ser miembro de la PAL.  
  
-   Ser un inicio de sesión asociado a un usuario en la base de datos de publicaciones.  
  
-   Ser un inicio de sesión asociado a un usuario en la base de datos de distribución (el usuario puede ser el usuario Guest).  
  
-   Tener permisos de lectura en el recurso compartido de instantáneas.  
  
 **Conectarse al suscriptor**  
 Para las suscripciones de extracción, las conexiones con el suscriptor siempre se realizan suplantando la cuenta especificada en el cuadro de texto **Cuenta de proceso** .  
  
 Para las suscripciones de inserción, debe elegir si el Agente de mezcla debe realizar las conexiones con el publicador y el distribuidor mediante la suplantación de la cuenta especificada en el cuadro de texto **Cuenta de proceso** o mediante una cuenta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Si selecciona utilizar una cuenta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , especifique una contraseña y un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  Se recomienda usar la suplantación de la cuenta de Windows en lugar de usar una cuenta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 La cuenta de Windows o la cuenta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usada para la conexión con el suscriptor debe ser como mínimo miembro del rol fijo de base de datos **db_owner** en la base de datos de suscripciones.  
  
## <a name="see-also"></a>Consulte también  
 [Administrar inicios de sesión y contraseñas en la replicación](security/identity-and-access-control-replication.md#manage-logins-and-passwords-in-replication)   
 [Modelo de seguridad del Agente de replicación](security/replication-agent-security-model.md)   
 [Replication Agents Overview](agents/replication-agents-overview.md)  (Información general sobre los agentes de replicación)  
 [Replication Security Best Practices](security/replication-security-best-practices.md)   
 [Suscribirse a publicaciones](subscribe-to-publications.md)  
  
  
