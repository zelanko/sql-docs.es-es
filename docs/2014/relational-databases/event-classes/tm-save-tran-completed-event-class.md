---
title: 'TM: Save Tran Completed, clase de eventos | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- 'TM: Save Tran Completed event class'
ms.assetid: e6b37780-5ad8-4d50-89a3-d8a22496faac
author: stevestein
ms.author: sstein
ms.openlocfilehash: 4ed85038d9cfc6281d1f9dbd84d4c0b0afeb43b3
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85027987"
---
# <a name="tm-save-tran-completed-event-class"></a>TM: Save Tran Completed, clase de eventos
  La clase de eventos TM: Save Tran Completed indica que ha finalizado una solicitud SAVE TRANSACTION. La solicitud fue enviada desde el cliente mediante la interfaz de administración de transacciones.  
  
## <a name="tm-save-tran-completed-event-class-data-columns"></a>Columnas de datos de la clase de evento TM: Save Tran Completed  
  
|Nombre de columna de datos|Tipo de datos|Descripción|Identificador de columna|Filtrable|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|Nombre de la aplicación cliente que ha creado la conexión a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta columna se rellena con los valores que pasa la aplicación, en lugar de con el nombre que se muestra para el programa.|10|Yes|  
|ClientProcessID|`int`|Identificador que el equipo host asigna al proceso en el que se ejecuta la aplicación cliente. Esta columna de datos se rellena si el cliente proporciona su identificador de proceso.|9|Yes|  
|DatabaseID|`int`|IDENTIFICADOR de la base de datos especificada por la instrucción USE *Database* o la base de datos predeterminada si no se ha emitido ninguna instrucción use *Database* para una instancia determinada. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] muestra el nombre de la base de datos si se captura la columna de datos ServerName en el seguimiento y el servidor está disponible. Determina el valor de una base de datos mediante la función DB_ID.|3|Yes|  
|DatabaseName|`nvarchar`|Nombre de la base de datos en la que se ejecuta la instrucción del usuario.|35|Yes|  
|Error|`int`|Número de error de un evento dado. Con frecuencia, es el número de error almacenado en la vista de catálogo sys.messages.|31|Yes|  
|EventClass|`int`|Tipo de evento = 192.|27|No|  
|EventSequence|`int`|Secuencia de un evento determinado de la solicitud.|51|No|  
|GroupID|`int`|Id. del grupo de carga de trabajo donde se activa el evento de Seguimiento de SQL.|66|Yes|  
|HostName|`nvarchar`|Nombre del equipo en el que se está ejecutando el cliente. Esta columna de datos se rellena si el cliente proporciona el nombre del host. Para determinar el nombre del host, utilice la función HOST_NAME.|8|Yes|  
|IsSystem|`int`|Indica si el evento ha ocurrido en un proceso del sistema o en un proceso de usuario. 1 = sistema, 0 = usuario.|60|Yes|  
|LoginName|`nvarchar`|Nombre del inicio de sesión del usuario (inicio de sesión de seguridad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o credenciales de inicio de sesión de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows con el formato DOMINIO\nombreDeUsuario).|11|Sí|  
|LoginSid|`image`|SID (número de identificación de seguridad) del usuario que ha iniciado la sesión. Puede buscar esta información en la vista de catálogo sys.server_principals. Cada SID es único para cada inicio de sesión en el servidor.|41|Sí|  
|NTDomainName|`nvarchar`|Dominio de Windows al que pertenece el usuario.|7|Yes|  
|NTUserName|`nvarchar`|Nombre del usuario de Windows.|6|Yes|  
|RequestID|`int`|Identificador de la solicitud que contiene la instrucción.|49|Sí|  
|nombreDeServidor|`nvarchar`|Nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de la que se realiza un seguimiento.|26|No|  
|SessionLoginName|`nvarchar`|Nombre de inicio de sesión del usuario que originó la sesión. Por ejemplo, si se conecta a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando inicioDeSesión1 y ejecuta una instrucción como inicioDeSesión2, SessionLoginName muestra inicioDeSesión1 y LoginName muestra inicioDeSesión2. En esta columna se muestran los inicios de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y de Windows.|64|Sí|  
|SPID|`int`|Identificador de la sesión en la que se produjo el evento.|12|Yes|  
|StartTime|`datetime`|Hora a la que se inició el evento, si está disponible.|14|Yes|  
|Correcto|`int`|1 = correcto. 0 = error (por ejemplo, 1 significa que se ha comprobado un permiso correctamente y 0 significa que se ha producido un error en la comprobación).|23|Sí|  
|TextData|`ntext`|Valor de texto que depende de la clase de eventos capturada en el seguimiento.|1|Sí|  
|TransactionID|`bigint`|Id. de la transacción asignado por el sistema.|4|Yes|  
|XactSequence|`bigint`|Token que describe la transacción actual.|50|Sí|  
  
## <a name="see-also"></a>Consulte también  
 [Eventos extendidos](../extended-events/extended-events.md)   
 [sp_trace_setevent &#40;&#41;de Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [SAVE TRANSACTION &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/save-transaction-transact-sql)  
  
  
