---
title: Prácticas recomendadas de seguridad de replicación | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- security [SQL Server replication], best practices
- security [SQL Server replication], between domains
- authentication [SQL Server replication]
- Internet [SQL Server replication], security
ms.assetid: 1ab2635d-0992-4c99-b17d-041d02ec9a7c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7db85ce6d63cd6c3eb458434357fa5a2d8127dec
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "63268671"
---
# <a name="replication-security-best-practices"></a>Prácticas recomendadas de seguridad de replicación
  La replicación mueve datos en entornos distribuidos que incluyen desde intranets con un solo dominio hasta aplicaciones que tienen acceso a datos entre dominios sin confianza y por Internet. Es importante comprender el mejor método que se debe utilizar para proteger las conexiones de replicación en diferentes circunstancias.  
  
 La siguiente información es importante para la replicación en todos los entornos:  
  
-   Cifre las conexiones entre equipos en una topología de replicación mediante un método estándar, como Red privada virtual (VPN), Capa de sockets seguros (SSL) o Seguridad IP (IPSEC). Para obtener más información, vea [Habilitar conexiones cifradas en el motor de base de datos &#40;Administrador de configuración de SQL Server&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md). Para obtener información sobre cómo utilizar VPN y SSL para replicar datos en Internet, vea [Securing Replication Over the Internet](securing-replication-over-the-internet.md).  
  
     Si utiliza SSL para proteger las conexiones entre equipos en una topología de replicación, especifique un valor de **1** o **2** para el parámetro **EncryptionLevel** de cada agente de replicación (se recomienda utilizar el valor **2** ). El valor **1** especifica que se debe utilizar el cifrado, pero el agente no comprueba si el certificado de servidor SSL está firmado por una entidad de confianza; el valor **2** especifica que se debe comprobar el certificado. Los parámetros del agente se pueden especificar en los perfiles del agente y en la línea de comandos. Para más información, consulte:  
  
    -   [Trabajar con perfiles del Agente de replicación](../agents/replication-agent-profiles.md)  
  
    -   [Ver y modificar parámetros del símbolo del sistema de los agentes de replicación &#40;SQL Server Management Studio&#41;](../agents/view-and-modify-replication-agent-command-prompt-parameters.md)  
  
    -   [Conceptos de los ejecutables del Agente de replicación](../concepts/replication-agent-executables-concepts.md)  
  
-   Ejecute cada agente de replicación en una cuenta de Windows diferente y utilice Autenticación de Windows para todas las conexiones de agentes de replicación. Para obtener más información sobre cómo especificar cuentas, vea [Manage Logins and Passwords in Replication](identity-and-access-control-replication.md#manage-logins-and-passwords-in-replication) (Administrar inicios de sesión y contraseñas en la replicación).  
  
-   Conceda solamente los permisos requeridos a cada agente. Para obtener más información, vea la sección sobre los permisos necesarios para los agentes en el tema [Replication Agent Security Model](replication-agent-security-model.md).  
  
-   Asegúrese de que las cuentas del Agente de mezcla y el Agente de distribución están en la lista de acceso a la publicación (PAL). Para obtener más información, vea [Proteger el publicador](secure-the-publisher.md).  
  
-   Siga el principio de privilegios mínimos permitiendo que las cuentas de la PAL solo tengan los permisos que necesitan para realizar tareas de replicación. No agregue los inicios de sesión a ningún rol fijo de servidor que no sea necesario para la replicación.  
  
-   Configure el recurso compartido de instantánea para permitir acceso de lectura a todos los agentes de mezcla y agentes de distribución. En el caso de instantáneas para publicaciones mediante filtros con parámetros, asegúrese de que cada carpeta está configurada para permitir acceso solo a las cuentas de Agente de mezcla correctas.  
  
-   Configure el recurso compartido de instantánea para permitir acceso de escritura al Agente de instantánea.  
  
-   Si utiliza suscripciones de extracción, use un recurso de red compartido en vez de una ruta de acceso local para la carpeta de instantáneas.  
  
 Si la topología de replicación incluye equipos que no se encuentran en el mismo dominio o están en dominios que no tienen relaciones de confianza entre sí, puede utilizar Autenticación de Windows o Autenticación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para las conexiones realizadas por agentes (Para obtener más información acerca de los dominios, vea la documentación de Windows). Para obtener la máxima seguridad se recomienda que utilice Autenticación de Windows.  
  
-   Para utilizar Autenticación de Windows:  
  
    -   Agregue una cuenta de Windows local (no una cuenta de dominio) para cada agente en los nodos adecuados (utilice el mismo nombre y contraseña en cada nodo). Por ejemplo, el Agente de distribución para una suscripción de inserción se ejecuta en el distribuidor y realiza conexiones al distribuidor y suscriptor. La cuenta de Windows para el Agente de distribución debe agregarse al distribuidor y suscriptor.  
  
    -   Asegúrese de que un determinado agente (por ejemplo, el Agente de distribución de una suscripción) se ejecuta con la misma cuenta en cada equipo.  
  
-   Para utilizar Autenticación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] :  
  
    -   Agregue una cuenta de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para cada agente en los nodos adecuados (utilice el mismo nombre y contraseña en cada nodo). Por ejemplo, el Agente de distribución para una suscripción de inserción se ejecuta en el distribuidor y realiza conexiones al distribuidor y suscriptor. La cuenta de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para el Agente de distribución debe agregarse al distribuidor y al suscriptor.  
  
    -   Asegúrese de que un determinado agente (por ejemplo, el Agente de distribución de una suscripción) realiza conexiones con la misma cuenta en cada equipo.  
  
    -   En situaciones que requieren Autenticación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , el acceso a recursos compartidos de instantáneas UNC normalmente no está disponible (por ejemplo, el acceso puede estar bloqueado por un firewall). En este caso, puede transferir la instantánea a los suscriptores a través del protocolo de transferencia de archivos (FTP). Para obtener más información, vea [Transferir instantáneas mediante FTP](../transfer-snapshots-through-ftp.md).  
  
## <a name="see-also"></a>Consulte también  
 [Habilitar conexiones cifradas en el motor de base de datos &#40;Administrador de configuración de SQL Server&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)   
 [Replicación a través de Internet](../replication-over-the-internet.md)   
 [Proteger el suscriptor](secure-the-subscriber.md)   
 [Proteger el distribuidor](secure-the-distributor.md)   
 [Proteger el publicador](secure-the-publisher.md)   
 [Seguridad de Replicación de SQL Server](view-and-modify-replication-security-settings.md)  
  
  
