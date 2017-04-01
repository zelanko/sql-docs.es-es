---
title: "MSSQL_ENG014117 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "error MSSQL_ENG014117"
ms.assetid: e5906a76-9511-4c47-8826-8c765b58a39d
caps.latest.revision: 18
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 17
---
# MSSQL_ENG014117
    
## Detalles del mensaje  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|14117|  
|Origen del evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nombre simbólico||  
|Texto del mensaje|%1!' no está configurado como base de datos de distribución.|  
  
## Explicación  
 Este problema puede ocurrir si se cumple uno de los siguientes supuestos o ambos:  
  
-   Falta la entrada de la base de datos de distribución especificada en **msdb..MSdistributiondbs**.  
  
-   No hay una entrada para el servidor local en la base de datos **maestra** o la entrada que hay es incorrecta.  
  
     La replicación espera que todos los servidores de una topología se registren utilizando el nombre del equipo con un nombre de instancia opcional (en el caso de una instancia en clúster, el servidor virtual de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con el nombre de instancia opcional). Para que la replicación funcione correctamente, el valor que devuelve `SELECT @@SERVERNAME` por cada servidor de la topología debe coincidir con el nombre del equipo o con el nombre del servidor virtual con el nombre de la instancia opcional.  
  
     La replicación no se admite si ha registrado alguna de las instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por dirección IP o por nombre de dominio completo (FQDN). Es posible que aparezca este error si registró alguna de las instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante dirección IP o FQDN en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] cuando configuró la replicación.  
  
## Acción del usuario  
 Compruebe que la instancia del distribuidor esté correctamente registrada. Si el nombre de red del equipo y el nombre de la instancia de SQL Server son diferentes, lleve a cabo una de estas acciones.  
  
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
  
     Después de ejecutar el [sp_addserver & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md) el procedimiento almacenado, debe reiniciar el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] service para @@SERVERNAME surta efecto el cambio.  
  
     Si el valor de @@SERVERNAME no es correcto en una instancia en clúster, debe cambiarle el nombre utilizando el Administrador de clústeres. Para obtener más información, consulte [instancias de clúster de conmutación por error AlwaysOn & #40; SQL Server & #41;](../Topic/AlwaysOn%20Failover%20Cluster%20Instances%20\(SQL%20Server\).md).  
  
 Después de comprobar que la instancia del distribuidor está correctamente registrada, asegúrese de que la base de datos de distribución aparece en **msdb..MSdistributiondbs**. Si no es así:  
  
1.  Genere un script para la configuración de la distribución. Para más información, consulte [Scripting Replication](../../relational-databases/replication/scripting-replication.md).  
  
2.  Deshabilite la distribución y, a continuación, vuelva a habilitarla. Para obtener más información, consulte [Configurar distribución](../../relational-databases/replication/configure-distribution.md).  
  
## Vea también  
 [Errores y eventos referencia & #40; Replicación y nº 41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  