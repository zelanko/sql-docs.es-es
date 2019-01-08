---
title: Proteger la carpeta de instantáneas | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server replication], security
ms.assetid: 3cd877d1-ffb8-48fd-a72b-98eb948aad27
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: cb3aa18f17219f46bc5ce6f3d25af7d4bd29c4d9
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52753957"
---
# <a name="secure-the-snapshot-folder"></a>Proteger la carpeta de instantáneas
  La carpeta de instantáneas es un directorio que almacena archivos de instantáneas. Se recomienda que sea un directorio dedicado para el almacenamiento de instantáneas. Conceda al Agente de instantáneas permiso de escritura en la carpeta y asegúrese de que el permiso de lectura se concede solamente a la cuenta de Windows que utiliza el Agente de mezcla o el Agente de distribución cuando tiene acceso a la carpeta. Para tener acceso a una carpeta de instantáneas que se encuentra en un equipo remoto, la cuenta de Windows asociada con el agente debe ser una cuenta de dominio.  
  
> [!NOTE]  
>  Control de cuentas de usuario (UAC) ayuda a los administradores a administrar sus derechos de usuario elevados (que a veces reciben el nombre de *privilegios*). Cuando se ejecuta en sistemas operativos que tienen UAC habilitado, los administradores no utilizan sus derechos administrativos. En su lugar, realizan la mayoría de acciones como usuarios estándar (no administrativos) y solo usan sus derechos administrativos de forma temporal cuando es necesario. UAC puede impedir el acceso administrativo al recurso compartido de instantáneas. Por lo tanto, debe conceder de forma explícita permisos del recurso compartido de instantáneas a las cuentas de Windows usadas por el Agente de instantáneas, el Agente de distribución y el Agente de mezcla. Debe hacerlo incluso si las cuentas de Windows pertenecen al grupo Administradores.  
  
 Al configurar un distribuidor mediante el Asistente para configurar la distribución o el Asistente para nueva publicación, la carpeta de instantáneas tiene como valor predeterminado una ruta de acceso local: X:\Program de programa\Microsoft SQL Server\\*\<instancia >* \MSSQL\ReplData. Si usa un distribuidor remoto o suscripciones de extracción, debe especificar un recurso compartido de red UNC (como \\\\<*nombre de equipo>* \instantánea) en lugar de una ruta de acceso local.  
  
 Los permisos para tener acceso a la carpeta de instantáneas deben concederse según la forma en la que se tiene acceso a la carpeta. En [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 2003 se utilizan las pestañas del siguiente cuadro de diálogo:  
  
-   Si especifica una ruta de acceso local, conceda permisos mediante la pestaña **Seguridad** del cuadro de diálogo **Propiedades** de la carpeta.  
  
-   Si especifica un recurso compartido de red, conceda permisos mediante la pestaña **Compartir** del cuadro de diálogo **Propiedades** de la carpeta.  
  
    > [!NOTE]  
    >  Si el Agente de replicación se ejecuta en el distribuidor, use la pestaña **Seguridad** del cuadro de diálogo **Propiedades** de la carpeta para conceder permisos a la cuenta de Windows que se usa para ejecutar el agente. Siga el procedimiento descrito incluso cuando se use un recurso compartido de red. Esto se aplica al Agente de mezcla y al Agente de distribución para una suscripción de inserción, y al Agente de instantáneas cuando el publicador y el distribuidor se encuentran en el mismo equipo.  
  
 Para obtener más información acerca de cómo establecer permisos para rutas de acceso locales y recursos de red compartidos, vea la documentación de Windows.  
  
> [!NOTE]  
>  Si se quita una publicación, la replicación intenta quitar la carpeta de instantáneas en el contexto de seguridad de la cuenta de servicio de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Si esta cuenta no tiene privilegios suficientes, inicie la sesión con una cuenta que tenga privilegios suficientes y quite la carpeta manualmente. Para quitar una carpeta es necesario el privilegio **Modificar** si la carpeta es una ruta de acceso local o el privilegio **Control total** si la carpeta es una ruta de acceso de red.  
  
## <a name="delivering-snapshots-through-ftp"></a>Entregar instantáneas mediante FTP  
 Para obtener la máxima seguridad se recomienda almacenar las instantáneas en un recurso compartido UNC, pero las instantáneas se pueden almacenar en un recurso compartido FTP y, a continuación, entregarse a un suscriptor mediante FTP. Al configurar el servidor FTP, asegúrese de que el directorio virtual ofrece un recurso compartido UNC subyacente que permita acceso de escritura mediante el Agente de instantáneas para la publicación.  
  
 Para configurar que un suscriptor recupere la instantánea mediante FTP, primero configure el servidor FTP con un inicio de sesión y una contraseña FTP que permitan a los suscriptores acceso de lectura (u "obtención") para que se puedan descargar los archivos de instantáneas.  
  
 Para entregar instantáneas mediante FTP, vea [Deliver a Snapshot Through FTP](../publish/deliver-a-snapshot-through-ftp.md) (Entregar una instantánea mediante FTP).  
  
 Para obtener información acerca de cómo establecer y cambiar la contraseña para tener acceso a instantáneas mediante FTP, vea la sección "Entrega de instantáneas a través de FTP" en el tema [Secure the Publisher](secure-the-publisher.md).  
  
## <a name="see-also"></a>Vea también  
 [Ubicaciones alternativas para las carpetas de instantáneas](../alternate-snapshot-folder-locations.md)   
 [Inicializar una suscripción con una instantánea](../initialize-a-subscription-with-a-snapshot.md)   
 [Replication Security Best Practices](replication-security-best-practices.md)   
 [Seguridad y protección &#40;replicación&#41;](security-and-protection-replication.md)   
 [Transferir instantáneas mediante FTP](../transfer-snapshots-through-ftp.md)  
  
  
