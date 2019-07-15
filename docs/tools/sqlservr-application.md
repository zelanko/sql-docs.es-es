---
title: sqlservr (aplicación) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- command prompt utilities [SQL Server], sqlservr
- command prompt [SQL Server], pausing/resuming instance of SQL Server
- starting instance of SQL Server
- command prompt [SQL Server], continuing instance of SQL Server
- sqlservr utility
- pausing instance of SQL Server
- stopping instance of SQL Server
- resuming SQL Server
- command prompt [SQL Server], stopping instance of SQL Server
- command prompt [SQL Server], starting instance of SQL Server
- continuing instance of SQL Server
ms.assetid: 60e8ef0a-0851-41cf-a6d8-cca1e04cbcdb
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 93a4572b44cf2be6fa8f1c0912fa7e8178e6c9a7
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/10/2019
ms.locfileid: "67733355"
---
# <a name="sqlservr-application"></a>sqlservr (aplicación)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  La aplicación **sqlservr** se inicia, se detiene, se pone en pausa y continúa una instancia de [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] desde un símbolo del sistema.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sqlservr [-sinstance_name] [-c] [-dmaster_path] [-f]   
     [-eerror_log_path] [-lmaster_log_path] [-m]  
     [-n] [-Ttrace#] [-v] [-x] [-gnumber]  
```  
  
## <a name="arguments"></a>Argumentos  
 **-s** *instance_name*  
 Especifica la instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] a la que hay que conectarse. Si no se especifica ninguna instancia con nombre, **sqlservr** inicia la instancia predeterminada de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  Al iniciar una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], debe usar la aplicación **sqlservr** en el directorio correspondiente de esa instancia. Ejecute **sqlservr** desde el directorio \MSSQL\Binn para la instancia predeterminada. Ejecute **sqlservr** desde el directorio \MSSQL$*nombre_instancia*\Binn para la instancia con nombre.  
  
 **-c**  
 Indica que una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] se inicia independientemente del Administrador de control de servicios de Windows. Esta opción se utiliza cuando se inicia [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] desde un símbolo del sistema para reducir el tiempo de inicio que necesita [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  Si usa esta opción, no puede detener [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] mediante el Administrador de servicios de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ni el comando **net stop** y, si cierra sesión en el equipo, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] se detiene.  
  
 **-d** *master_path*  
 Indica la ruta de acceso completa para el archivo de base de datos **maestra** . No hay espacios entre **-d** y *master_path*. Si no proporciona esta opción, se usarán los parámetros del Registro existentes.  
  
 **-f**  
 Inicia una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] con la configuración mínima. Esta opción resulta útil si el valor de una opción de configuración (por ejemplo, la confirmación excesiva de memoria) ha impedido el inicio del servidor.  
  
 **-e** *error_log_path*  
 Indica la ruta de acceso con autorización completa para el archivo de registro de errores. Si no se especifica, la ubicación predeterminada es *\<Unidad>* :\Archivos de programa\Microsoft SQL Server\MSSQL\Log\Errorlog para la instancia predeterminada y *\<Unidad>* :\Archivos de programa\Microsoft SQL Server\MSSQL$*nombre_instancia*\Log\Errorlog para una instancia con nombre. No hay espacios entre **-e** y *error_log_path*.  
  
 **-l** *master_log_path*  
 Indica la ruta de acceso con autorización completa para el archivo de registro de transacciones de la base de datos **maestra** . No hay espacios entre **-l** y *master_log_path*.  
  
 **-m**  
 Indica que se inicie una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en modo de usuario único. Solo un usuario puede conectar cuando [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] se inicia en modo de usuario único. No se inicia el mecanismo CHECKPOINT, que garantiza que se escriben con regularidad transacciones completadas desde la memoria caché del disco al dispositivo de base de datos. (Normalmente, esta opción se utiliza si se existen problemas en las bases de datos del sistema y necesitan repararse.) Habilita la opción **sp_configure allow updates**. De forma predeterminada, la opción **allow updates** está deshabilitada.  
  
 **-n**  
 Permite iniciar una instancia con nombre de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Sin el parámetro **-s** establecido, la instancia predeterminada intenta iniciarse. Debe cambiar al directorio BINN apropiado para la instancia en una ventana del símbolo del sistema antes de iniciar **sqlservr.exe**. Por ejemplo, si Instance1 usara \mssql$Instance1 para sus archivos binarios, el usuario debería estar en el directorio \mssql$Instance1\binn para poder iniciar **sqlservr.exe -s instance1**. Si inicia una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] con la opción **-n** , es recomendable que use también la opción **-e** ; de lo contrario los eventos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no se registrarán.  
  
 **-T** *trace#*  
 Indica que se debe iniciar una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] con una marca de seguimiento específica (*trace#* ) vigente. Las marcas de seguimiento se utilizan para iniciar el servidor con un comportamiento distinto del habitual. Para obtener más información, vea [Marcas de seguimiento &#40;Transact-SQL&#41;](../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md).  
  
> [!IMPORTANT]  
>  Cuando especifique una marca de seguimiento, use **-T** para pasar el número de la marca de seguimiento. **acepta una t minúscula (** -t [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]), pero **-t** establece otras marcas de seguimiento internas que necesitan los ingenieros de soporte técnico de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
 **-v**  
 Muestra el número de versión del servidor.  
  
 **-x**  
 Deshabilita el mantenimiento de estadísticas de tiempo de CPU y número de aciertos de caché. Permite el máximo rendimiento.  
  
 **-g** *memory_to_reserve*  
 Especifica un número entero de megabytes (MB) de memoria que [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] deja disponibles para las asignaciones de memoria en el proceso de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , pero fuera del bloque de memoria de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . La memoria fuera del bloque de memoria es el área que utiliza [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para cargar elementos como archivos `.dll` de procedimientos extendidos, proveedores OLE DB a los que hacen referencia las consultas distribuidas y objetos de automatización a los que se hace referencia en instrucciones [!INCLUDE[tsql](../includes/tsql-md.md)] . El valor predeterminado es 256 MB.  
  
 El uso de esta opción puede ayudarle a optimizar la asignación de memoria, pero solo cuando la memoria física sobrepasa el límite configurado establecido por el sistema operativo en la memoria virtual disponible para las aplicaciones. El uso de esta opción puede ser apropiado para configuraciones con mucha memoria en las que los requisitos de memoria de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no sean típicos y el espacio para direcciones virtuales del proceso de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] se utilice completamente. Si se usa esta opción de manera incorrecta, una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] podría no iniciarse o tener errores en tiempo de ejecución.  
  
 Use el valor predeterminado del parámetro **-g** , a menos que vea alguna de las siguientes advertencias en el registro de errores de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] :  
  
-   "Failed Virtual Allocate Bytes: FAIL_VIRTUAL_RESERVE \<tamaño>"  
  
-   "Failed Virtual Allocate Bytes: FAIL_VIRTUAL_COMMIT \<tamaño>"  
  
 Estos mensajes podrían indicar que [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] está intentando liberar partes del bloque de memoria de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] a fin de buscar espacio para elementos como los archivos .DLL de procedimientos almacenados extendidos u objetos de automatización. En este caso, considere la posibilidad de aumentar la cantidad de memoria reservada con el modificador **-g** .  
  
 Si usa un valor inferior al predeterminado, aumentará la cantidad de memoria disponible para el grupo de búferes y pilas de subprocesos; no obstante, esto podría suponer a su vez ventajas de rendimiento para cargas de trabajo que consuman mucha memoria en sistemas que no usen procedimientos almacenados extendidos, consultas distribuidas u objetos de automatización.  
  
## <a name="remarks"></a>Notas  
 En la mayoría de los casos, el programa sqlserver.exe solo se usa para solucionar problemas o realizar las tareas principales de mantenimiento. Si se inicia [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] desde el símbolo del sistema con sqlservr.exe, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no se inicia como servicio, de forma que [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no se puede detener mediante los comandos **net** . Los usuarios pueden conectar con [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], pero las herramientas de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] muestran el estado del servicio, de forma que el Administrador de configuración de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] indica correctamente que el servicio se ha detenido. [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] puede conectarse al servidor, pero también indica que el servicio está detenido.  
  
## <a name="compatibility-support"></a>Soporte de compatibilidad  
 El parámetro **-h**  no es compatible con [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]. Este parámetro se usaba en versiones anteriores de instancias de 32 bits de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para reservar espacio de direcciones de memoria virtual para los metadatos de Agregar memoria sin interrupción cuando AWE está habilitado. Para obtener más información, vea [Características de SQL Server en desuso y descontinuadas en SQL Server 2016](https://msdn.microsoft.com/library/0678bfbc-5d3f-44f4-89c0-13e8e52404da).  
  
## <a name="see-also"></a>Consulte también  
 [Opciones de inicio del servicio de motor de base de datos](../database-engine/configure-windows/database-engine-service-startup-options.md)  
  
  
