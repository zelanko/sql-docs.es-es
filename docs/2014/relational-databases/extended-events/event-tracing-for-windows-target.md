---
title: Seguimiento de eventos para Windows como destino | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xevents
ms.topic: conceptual
helpviewer_keywords:
- event tracing for windows target
- ETW target
- targets [SQL Server extended events], event tracing for windows target
ms.assetid: ca2bb295-b7f6-49c3-91ed-0ad4c39f89d5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e855b9de09727a4437cad99a2534aee9d960298b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62519309"
---
# <a name="event-tracing-for-windows-target"></a>seguimiento de eventos para Windows de destino
  Antes de utilizar el Seguimiento de eventos para Windows (ETW) como destino, se recomienda tener conocimientos prácticos de ETW. El Seguimiento de eventos para Windows (ETW) se utiliza junto a Extended Events o como un consumidor de eventos de Extended Events. Los vínculos externos siguientes proporcionan un punto de inicio para obtener información general sobre ETW:  
  
-   [Eventos de Windows](https://go.microsoft.com/fwlink/?LinkId=92380)  
  
-   [Mejorar la depuración y el ajuste del rendimiento con ETW](https://go.microsoft.com/fwlink/?LinkId=92381)  
  
 El destino ETW es un destino singleton, aunque el destino se puede agregar a muchas sesiones. Si un evento se provoca en muchas sesiones, solamente se difundirá al destino ETW una vez por cada vez que se produzca. El motor de Extended Events está limitado a una sola instancia por proceso.  
  
> [!IMPORTANT]  
>  Para que el destino ETW funcione, la cuenta de inicio del servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe ser miembro del grupo de usuarios del registro de rendimiento.  
  
 El proceso que hospeda el motor de Extended Events controla la configuración de los eventos presentes en una sesión ETW. El motor controla los eventos que se van a provocar y las condiciones que se deben cumplir para que se produzca un evento.  
  
 Después de enlazar a una sesión de Extended Events, que adjunta el destino ETW por primera vez en el período de duración de un proceso, el destino ETW abre una única sesión ETW en el proveedor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Si ya existe una sesión ETW, el destino ETW obtiene una referencia a la sesión existente. Esta sesión ETW se comparte con todas las instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en un equipo determinado. Esta sesión ETW recibe todos los eventos de las sesiones que tienen el destino ETW.  
  
 Dado que ETW necesita proveedores para habilitarse y así utilizar los eventos y encauzarlos a ETW, se habilitan todos los paquetes de Extended Events en la sesión. Cuando se activa un evento, el destino ETW envía el evento a la sesión en la que está habilitado el proveedor para el evento.  
  
 El destino ETW admite la publicación sincrónica de eventos en el subproceso que provoca el evento. Sin embargo, el destino ETW no admite la publicación asincrónica de eventos.  
  
 El destino ETW no admite el control de las controladoras ETW externas como logman.exe. Para generar seguimientos de ETW, se debe crear una sesión de evento con el destino ETW. Para obtener más información, vea [CREATE EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-event-session-transact-sql).  
  
> [!NOTE]  
>  Al habilitar el destino ETW se crea una sesión ETW denominada XE_DEFAULT_ETW_SESSION. Si ya existe una sesión con el nombre XE_DEFAULT_ETW_SESSION, se usa sin modificar ninguna de las propiedades de la sesión existente. XE_DEFAULT_ETW_SESSION se comparte entre todas las instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Después de iniciar una sesión XE_DEFAULT_ETW_SESSION, debe detenerla mediante una controladora ETW, como la herramienta Logman. Por ejemplo, puede ejecutar el siguiente comando en el símbolo del sistema: `logman stop XE_DEFAULT_ETW_SESSION -ets`.  
  
 En la tabla siguiente se describen las opciones disponibles para configurar el destino ETW.  
  
|Opción|Valores permitidos|Descripción|  
|------------|--------------------|-----------------|  
|default_xe_session_name|Cualquier cadena de 256 caracteres, como máximo. Este valor es opcional.|El nombre de la sesión de Extended Events. De forma predeterminada, es XE_DEFAULT_ETW_SESSION.|  
|default_etw_session_logfile_path|Cualquier cadena de 256 caracteres, como máximo. Este valor es opcional.|La ruta de acceso del archivo de registro para la sesión de Extended Events. De forma predeterminada, es %TEMP%\XEEtw.etl.|  
|default_etw_session_logfile_size_mb|Un entero sin signo. Este valor es opcional.|El tamaño del archivo de registro, en megabytes (MB), para la sesión de Extended Events. El valor predeterminado es 20 MB.|  
|default_etw_session_buffer_size_kb|Un entero sin signo. Este valor es opcional.|El tamaño de búfer en memoria, en kilobytes (kB), para la sesión de Extended Events. El valor predeterminado es 128 kB.|  
|retries|Un entero sin signo.|El número de veces que se debe reintentar publicar el evento al subsistema de ETW antes de quitar el evento. El valor predeterminado es 0.|  
  
 La configuración de estos valores es opcional. El destino ETW utiliza los valores predeterminados para estos valores.  
  
 El destino ETW es responsable de:  
  
-   Crear la sesión ETW predeterminada.  
  
-   Registrar todos los paquetes de Extended Events con ETW. Así se asegura de que ETW no quita los eventos.  
  
-   Administrar el flujo de eventos a ETW. El destino ETW crea un evento ETW con los datos de Extended Events y lo envía a la sesión ETW adecuada. Si el evento es mayor que el tamaño de búfer o los datos no caben en un evento ETW, ETW dividirá el evento en varios fragmentos.  
  
-   Mantener los paquetes de Extended Events habilitados en todo momento.  
  
 ETW utiliza las siguientes ubicaciones predeterminadas de archivos:  
  
-   El archivo de salida ETW está en %TEMP%\XEEtw.etl.  
  
    > [!IMPORTANT]  
    >  No se puede cambiar la ruta de acceso del archivo después de que la primera sesión se haya iniciado.  
  
-   Los archivos MOF (Managed Object Format) se encuentran en *\<su ruta de instalación>* \Microsoft SQL Server\Shared. Para obtener más información, vea [Formato de objetos administrados](https://go.microsoft.com/fwlink/?LinkId=92851) en MSDN.  
  
## <a name="adding-the-target-to-a-session"></a>Agregar el destino a una sesión  
 Para agregar el destino ETW a una sesión de eventos extendidos, debe incluir la siguiente instrucción al crear o modificar una sesión de eventos:  
  
```  
ADD TARGET package0.etw_classic_sync_target  
```  
  
 Para obtener más información sobre un ejemplo completo que muestra cómo usar el destino ETW, incluida la forma de ver los datos, vea [Supervisar la actividad del sistema mediante eventos extendidos](monitor-system-activity-using-extended-events.md).  
  
## <a name="see-also"></a>Consulte también  
 [Destinos de SQL Server Extended Events](../../database-engine/sql-server-extended-events-targets.md)   
 [sys.dm_xe_session_targets &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-session-targets-transact-sql)   
 [CREATE EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-event-session-transact-sql)   
 [ALTER EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-event-session-transact-sql)  
  
  
