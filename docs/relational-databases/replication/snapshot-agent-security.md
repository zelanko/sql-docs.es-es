---
title: Seguridad del Agente de instantáneas | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.security.SSA.f1
helpviewer_keywords:
- Snapshot Agent Security dialog box
ms.assetid: 64e84c67-acc6-4906-98d4-3451767363fe
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 321639282201761e48d34c43411b74c15d77e72e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47742113"
---
# <a name="snapshot-agent-security"></a>Seguridad del Agente de instantáneas
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  El cuadro de diálogo **Seguridad del Agente de instantáneas** le permite especificar lo siguiente:  
  
-   La cuenta de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows bajo la cual el Agente de instantáneas se ejecuta en el Distribuidor. La cuenta de Windows se denomina también *cuenta de proceso*porque el proceso del agente se ejecuta con dicha cuenta.  
  
-   El contexto bajo el cual el Agente de instantáneas establece conexiones con el publicador de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . La conexión se puede realizar suplantando la cuenta de Windows o en el contexto de la cuenta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se especifique.  
  
    > [!NOTE]  
    >  El Agente de instantáneas establece conexiones con el publicador aun cuando el publicador y el distribuidor se encuentren en el mismo equipo. El Agente de instantáneas también establece conexiones con el distribuidor; estas conexiones siempre se establecen suplantando la cuenta de Windows bajo la cual se ejecuta el agente.  
  
     Para publicadores de Oracle, especifique el contexto bajo el cual el Agente de instantáneas se conecta con el publicador en el cuadro de diálogo **Propiedades del publicador** (disponible desde el cuadro de diálogo **Propiedades del distribuidor** ). Para más información, consulte [View and Modify Replication Security Settings](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md).  
  
 Todas las cuentas deben ser válidas y se debe especificar la contraseña correcta para cada cuenta. Las cuentas y las contraseñas se validan cuando se ejecuta el agente.  
  
## <a name="options"></a>Opciones  
 **Process account**  
 Especifique una cuenta de Windows bajo la cual el Agente de instantáneas se ejecuta en el Distribuidor. La cuenta de Windows que especifique debe cumplir lo siguiente:  
  
-   Ser como mínimo miembro del rol fijo de base de datos **db_owner** en la base de datos de distribución.  
  
-   Tener permisos de escritura en el recurso compartido de instantáneas.  
  
 **Contraseña** y **Confirmar contraseña**  
 Escriba la contraseña de la cuenta de Windows.  
  
 **Conectar al publicador**  
 Seleccione si el Agente de instantáneas debe establecer conexiones con el publicador mediante la suplantación de la cuenta especificada en el cuadro de texto **Cuenta de proceso** o utilizando una cuenta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Si selecciona utilizar una cuenta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , especifique una contraseña y un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  Se recomienda usar la suplantación de la cuenta de Windows en lugar de usar una cuenta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 La cuenta de Windows o la cuenta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizada para conectarse debe ser miembro, como mínimo, del rol fijo de base de datos **db_owner** de la base de datos de publicación.  
  
## <a name="see-also"></a>Ver también  
 [Administrar inicios de sesión y contraseñas en la replicación](../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md)   
 [Modelo de seguridad del Agente de replicación](../../relational-databases/replication/security/replication-agent-security-model.md)   
 [Replication Agents Overview](../../relational-databases/replication/agents/replication-agents-overview.md)  (Información general sobre los agentes de replicación)  
 [Prácticas recomendadas de seguridad de replicación](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  
