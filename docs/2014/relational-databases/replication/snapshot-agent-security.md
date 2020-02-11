---
title: Seguridad del Agente de instantáneas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.security.SSA.f1
helpviewer_keywords:
- Snapshot Agent Security dialog box
ms.assetid: 64e84c67-acc6-4906-98d4-3451767363fe
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1e63cee642738036933b0a1e2a9da6b48192fba9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62676640"
---
# <a name="snapshot-agent-security"></a>Seguridad del Agente de instantáneas
  El cuadro de diálogo **seguridad de agente de instantáneas** permite especificar:  
  
-   La cuenta de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows bajo la cual el Agente de instantáneas se ejecuta en el Distribuidor. También se hace referencia a la cuenta de Windows como *cuenta de proceso*, ya que el proceso del agente se ejecuta en esta cuenta.  
  
-   Contexto en el que el agente de instantáneas realiza conexiones al [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicador. La conexión se puede realizar suplantando la cuenta de Windows o en el contexto de la cuenta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se especifique.  
  
    > [!NOTE]  
    >  El Agente de instantáneas establece conexiones con el publicador aun cuando el publicador y el distribuidor se encuentren en el mismo equipo. El Agente de instantáneas también establece conexiones con el distribuidor; estas conexiones siempre se establecen suplantando la cuenta de Windows bajo la cual se ejecuta el agente.  
  
     Para publicadores de Oracle, especifique el contexto bajo el cual el Agente de instantáneas se conecta con el publicador en el cuadro de diálogo **Propiedades del publicador** (disponible desde el cuadro de diálogo **Propiedades del distribuidor** ). Para obtener más información, vea [ver y modificar la configuración de seguridad](security/view-and-modify-replication-security-settings.md)de la replicación.  
  
 Todas las cuentas deben ser válidas y se debe especificar la contraseña correcta para cada cuenta. Las cuentas y las contraseñas se validan cuando se ejecuta el agente.  
  
## <a name="options"></a>Opciones  
 **Cuenta de proceso**  
 Especifique una cuenta de Windows bajo la cual el Agente de instantáneas se ejecuta en el Distribuidor. La cuenta de Windows que especifique debe cumplir lo siguiente:  
  
-   Ser, como mínimo, miembro del rol fijo de base de datos **db_owner** en la base de datos de distribución.  
  
-   Tener permisos de escritura en el recurso compartido de instantáneas.  
  
 **Contraseña** y **Confirmar contraseña**  
 Escriba la contraseña de la cuenta de Windows.  
  
 **Conectar al publicador**  
 Seleccione si el Agente de instantáneas debe establecer conexiones con el publicador mediante la suplantación de la cuenta especificada en el cuadro de texto **Cuenta de proceso** o utilizando una cuenta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Si selecciona utilizar una cuenta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , especifique una contraseña y un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  Se recomienda usar la suplantación de la cuenta de Windows en lugar de usar una cuenta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 La cuenta de Windows o la cuenta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizada para conectarse debe ser miembro, como mínimo, del rol fijo de base de datos **db_owner** de la base de datos de publicación.  
  
## <a name="see-also"></a>Consulte también  
 [Administrar inicios de sesión y contraseñas en la replicación](security/identity-and-access-control-replication.md#manage-logins-and-passwords-in-replication)   
 [Modelo de seguridad del Agente de replicación](security/replication-agent-security-model.md)   
 [Replication Agents Overview](agents/replication-agents-overview.md)  (Información general sobre los agentes de replicación)  
 [Procedimientos recomendados de seguridad de replicación](security/replication-security-best-practices.md)  
  
  
