---
title: MSSQL_ENG014114 | Microsoft Docs
ms.custom: 
ms.date: 08/26/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- MSSQL_ENG014114 error
ms.assetid: f5f04590-e1c6-40d8-ab2b-98c791a0fc44
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0e2f6a83763be1e01adfb8ed08147cc1fb4905d2
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="mssqleng014114"></a>MSSQL_ENG014114
    
## <a name="message-details"></a>Detalles del mensaje  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|14114|  
|Origen del evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nombre simbólico||  
|Texto del mensaje|%1!' no está configurado como distribuidor.|  
  
## <a name="explanation"></a>Explicación  
 Si el mensaje de error especifica una instancia concreta, en vez de 'null', la instancia especificada no se ha configurado correctamente para que sea reconocida como distribuidor.  
  
 Si el mensaje especifica 'null' como distribuidor, no hay ninguna entrada para el servidor local en la base de datos **maestra** , o la entrada es incorrecta (quizás porque el equipo ha cambiado de nombre). La replicación espera que todos los servidores de una topología se registren utilizando el nombre del equipo con un nombre de instancia opcional (en el caso de una instancia en clúster, el servidor virtual de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con el nombre de instancia opcional). Para que la replicación funcione correctamente, el valor que devuelve `SELECT @@SERVERNAME` por cada servidor de la topología debe coincidir con el nombre del equipo o con el nombre del servidor virtual con el nombre de la instancia opcional.  
  
 La replicación no se admite si ha registrado alguna de las instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por dirección IP o por nombre de dominio completo (FQDN). Es posible que aparezca este error si registró alguna de las instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante dirección IP o FQDN en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] cuando configuró la replicación.  
  
## <a name="user-action"></a>Acción del usuario  
 Si el mensaje especifica una instancia concreta, configure el servidor como distribuidor. Para más información, vea [Configurar la distribución](../../relational-databases/replication/configure-distribution.md).  
  
 Si el mensaje no especifica una instancia concreta ('null'), compruebe que la instancia del distribuidor está correctamente registrada. Si el nombre de red del equipo y el nombre de la instancia de SQL Server son diferentes, lleve a cabo una de estas acciones.  
  
-   Agregue el nombre de la instancia de SQL Server como nombre de red válido. Un método para establecer un nombre de red alternativo es agregarlo al archivo de hosts local. El archivo de hosts local se encuentra de manera predeterminada en WINDOWS\system32\drivers\etc o en WINNT\system32\drivers\etc. Para obtener más información, consulte la documentación de Windows.  
  
     Por ejemplo, si el nombre de equipo es comp1 y el equipo tiene la dirección IP 10.193.17.129, y el nombre de la instancia es inst1/instname, agregue la siguiente entrada en el archivo de hosts:  
  
     10.193.17.129 inst1  
  
-   Deshabilite la distribución, registre la instancia y, a continuación, vuelva establecer la distribución. Si el valor de @@SERVERNAME no es correcto en una instancia que no esté en clúster, siga estos pasos:  
  
    ```  
    sp_dropserver '<old_name>', 'droplogins'  
    go  
    sp_addserver '<new_name>', 'local'  
    go  
    ```  
  
     Después de ejecutar el procedimiento almacenado [sp_addserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md), debe reiniciar el servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para que el cambio en @@SERVERNAME surta efecto.  
  
     Si el valor de @@SERVERNAME no es correcto en una instancia en clúster, debe cambiarle el nombre usando el Administrador de clústeres. Para obtener más información, vea [Always On Failover Cluster Instances (SQL Server)](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md) (Instancias de clúster de conmutación por error de Always On [SQL Server]).  
  
## <a name="see-also"></a>Vea también  
 [Referencia de errores y eventos &#40;replicación&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  

