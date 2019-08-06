---
title: MSSQL_ENG014010 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG014010 error
ms.assetid: 6ea84f2f-e7a2-4028-9ea9-af0d2eba660e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8af9ae77562cb8ece9cb23e32c4e4ce216987715
ms.sourcegitcommit: 495913aff230b504acd7477a1a07488338e779c6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2019
ms.locfileid: "68811117"
---
# <a name="mssql_eng014010"></a>MSSQL_ENG014010
    
## <a name="message-details"></a>Detalles del mensaje  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|14010|  
|Origen del evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nombre simbólico||  
|Texto del mensaje|El servidor '%s' no está definido como servidor de suscripción.|  
  
## <a name="explanation"></a>Explicación  
 La replicación espera que todos los servidores de una topología se registren utilizando el nombre del equipo con un nombre de instancia opcional (en el caso de una instancia en clúster, el servidor virtual de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con el nombre de instancia opcional). Para que la replicación funcione correctamente, el valor que devuelve `SELECT @@SERVERNAME` por cada servidor de la topología debe coincidir con el nombre del equipo o con el nombre del servidor virtual con el nombre de la instancia opcional.  
  
 La replicación no se admite si ha registrado alguna de las instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por dirección IP o por nombre de dominio completo (FQDN). Este error puede producirse si ha registrado alguna de las instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por dirección IP o FQDN en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] al configurar la replicación.  
  
## <a name="user-action"></a>Acción del usuario  
 Compruebe que todas las instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de la topología están registradas correctamente. Si el nombre de red del equipo y el nombre de la instancia de SQL Server son diferentes, lleve a cabo una de estas acciones.  
  
-   Agregue el nombre de la instancia de SQL Server como nombre de red válido. Un método para establecer un nombre de red alternativo es agregarlo al archivo de hosts local. El archivo de hosts local se encuentra de manera predeterminada en WINDOWS\system32\drivers\etc o en WINNT\system32\drivers\etc. Para obtener más información, consulte la documentación de Windows.  
  
     Por ejemplo, si el nombre de equipo es comp1 y el equipo tiene la dirección IP 10.193.17.129, y el nombre de la instancia es inst1/instname, agregue la siguiente entrada en el archivo de hosts:  
  
     10.193.17.129 inst1  
  
-   Quite la replicación, registre cada instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y, a continuación, vuelva a restablecer la replicación. Si el valor de @@SERVERNAME no es correcto para una instancia no agrupada, siga estos pasos:  
  
    ```  
    sp_dropserver '<old_name>', 'droplogins'  
    go  
    sp_addserver '<new_name>', 'local'  
    go  
    ```  
  
     Después de ejecutar el procedimiento almacenado [sp_addserver &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addserver-transact-sql), debe reiniciar el servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para que el cambio en @@SERVERNAME surta efecto.  
  
     Si el valor de @@SERVERNAME no es correcto en una instancia en clúster, debe cambiarle el nombre usando el Administrador de clústeres. Para obtener más información,vea [Instancias de clúster de conmutación por error de AlwaysOn &#40;SQL Server&#41;](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md).  
  
## <a name="see-also"></a>Vea también  
 [@@SERVERNAME &#40;Transact-SQL&#41;](/sql/t-sql/functions/servername-transact-sql)   
 [Referencia de errores y eventos &#40;replicación&#41;](errors-and-events-reference-replication.md)  
  
  
