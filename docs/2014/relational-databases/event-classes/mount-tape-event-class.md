---
title: Clase de eventos Mount Tape | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Mount Tape event class
ms.assetid: 4c595e0a-d968-47d3-a84f-9b6857342671
author: stevestein
ms.author: sstein
ms.openlocfilehash: 8298df4bfd0eaa91cf788fedbffe4e9b2a1389de
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85052881"
---
# <a name="mount-tape-event-class"></a>Mount Tape, clase de eventos
  La clase de eventos Mount Tape se produce cuando se recibe una solicitud de montaje de cinta. Utilice esta clase de eventospara supervisar solicitudes de montaje de cintas y si se realiza correcta o incorrectamente.  
  
## <a name="mount-tape-event-class-data-columns"></a>Columnas de datos de la clase de eventos Mount Tape  
  
|Nombre de columna de datos|Tipo de datos|Descripción|Identificador de columna|Filtrable|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|Nombre de la aplicación cliente que ha creado la conexión a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta columna se llena con valores que pasa la aplicación.|10|Yes|  
|ClientProcessID|`int`|Identificador que el equipo host asigna al proceso en el que se ejecuta la aplicación cliente. Esta columna de datos se rellena si el cliente proporciona el identificador de proceso del cliente.|9|Yes|  
|DatabaseID|`int`|Identificador de la base de datos especificada mediante la instrucción USE *database* o la base de datos predeterminada si no se emite la instrucción USE *database* para una determinada instancia. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] muestra el nombre de la base de datos si se captura la columna de datos ServerName en el seguimiento y el servidor está disponible. Determina el valor de una base de datos mediante la función DB_ID.|3|Yes|  
|DatabaseName|`nvarchar`|Nombre de la base de datos en la que se ejecuta la instrucción del usuario.|35|Yes|  
|Duration|`bigint`|Tiempo (en microsegundos) que tarda el evento.|13|Sí|  
|EndTime|`datetime`|En eventos Mount Request, el tiempo de espera para el montaje si se supera dicho tiempo de espera; de no ser así, es el tiempo del propio evento (en tales casos, StartTime indica el tiempo de la solicitud de montaje correspondiente).|15|Yes|  
|EventClass|`int`|Tipo de evento = 195.|27|No|  
|EventSequence|`int`|La secuencia de un evento determinado en la solicitud.|51|No|  
|EventSubClass|`int`|Tipo de la subclase de eventos.<br /><br /> 1 = Solicitud de montaje de cinta<br /><br /> 2 = Montaje de cinta completo<br /><br /> 3 = Montaje de cinta cancelado|21|Yes|  
|GroupID|`int`|Id. del grupo de carga de trabajo donde se activa el evento de Seguimiento de SQL.|66|Yes|  
|HostName|`nvarchar`|Nombre del equipo en el que se está ejecutando el cliente. Esta columna de datos se rellena si el cliente proporciona el nombre del host. Para determinar el nombre del host, utilice la función HOST_NAME.|8|Yes|  
|IsSystem|`int`|Indica si el evento ha ocurrido en un proceso del sistema o en un proceso de usuario. 1 = sistema, 0 = usuario.|60|Yes|  
|LoginName|`nvarchar`|Nombre del inicio de sesión del usuario ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Inicio de sesión de seguridad de o [!INCLUDE[msCoName](../../includes/msconame-md.md)] credenciales de inicio de sesión de Windows con el formato dominio \\ *nombreDeUsuario*).|11|Yes|  
|NTDomainName|`nvarchar`|Dominio de Windows al que pertenece el usuario.|7|Yes|  
|NTUserName|`nvarchar`|Nombre del usuario de Windows.|6|Sí|  
|nombreDeServidor|`nvarchar`|Nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de la que se realiza un seguimiento.|26|No|  
|SessionLoginName|`nvarchar`|Nombre de inicio de sesión del usuario que originó la sesión. Por ejemplo, si se conecta a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando inicioDeSesión1 y ejecuta una instrucción como inicioDeSesión2, SessionLoginName muestra inicioDeSesión1 y LoginName muestra inicioDeSesión2. En esta columna se muestran los inicios de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y de Windows.|64|Sí|  
|SPID|`int`|Id. de la sesión en la que se ha producido el evento.|12|Yes|  
|StartTime|`datetime`|Hora a la que se inició el evento, si está disponible.|14|Sí|  
|TextData|`ntext`|*nombre de dispositivo físico* [( *nombre del dispositivo lógico* )]. El nombre de dispositivo lógico se muestra solo si se ha definido en la vista de catálogo sys.backup_devices.|1|Sí|  
  
## <a name="see-also"></a>Consulte también  
 [sp_trace_setevent &#40;&#41;de Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [Copia de seguridad y restauración de bases de datos de SQL Server](../backup-restore/back-up-and-restore-of-sql-server-databases.md)  
  
  
