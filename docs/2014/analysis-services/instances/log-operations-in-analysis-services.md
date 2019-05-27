---
title: Las operaciones de registro en Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: aa1db060-95dc-4198-8aeb-cffdda44b140
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 74f81deb2d9f5e4fcb770217a228a8b081098d89
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66079759"
---
# <a name="log-operations-in-analysis-services"></a>Operaciones de registro en Analysis Services
  Una instancia de Analysis Services registrará las notificaciones de servidor, los errores y advertencias en el archivo msmdsrv.log: uno para cada instancia que instale. Los administradores consultan este registro para obtener información sobre eventos, tanto rutinarios como extraordinarios. En las versiones recientes, los registros se han mejorado para incluir más información. Las entradas de registro ahora incluyen información de la versión y la edición, así como del procesador, la memoria, la conectividad y los eventos de bloqueo. Puede revisar la lista completa de cambios en [Mejoras de los registros](https://support.microsoft.com/kb/2965035).  
  
 Además de la característica de registro integrada, muchos administradores y desarrolladores también usan herramientas proporcionadas por la comunidad de Analysis Services para recopilar datos sobre las operaciones de servidor, como **ASTrace**. Consulte [ejemplos de la Comunidad de Microsoft SQL Server: Analysis Services](https://sqlsrvanalysissrvcs.codeplex.com/) para los vínculos de descarga.  
  
 Este tema contiene las siguientes secciones:  
  
-   [Ubicación y tipos de registros](#bkmk_location)  
  
-   [Información general sobre la configuración del archivo de registro](#bkmk_general)  
  
-   [Archivo de registro del servicio MSMDSRV](#bkmk_msmdsrv)  
  
-   [Registros de consultas](#bkmk_querylog)  
  
-   [Archivos de minivolcado (.mdmp)](#bkmk_mdmp)  
  
-   [Sugerencias y prácticas recomendadas](#bkmk_tips)  
  
> [!NOTE]  
>  Si busca información acerca de los registros, también podría interesarle el seguimiento de las operaciones, que muestra el procesamiento y las rutas de ejecución de consultas. Objetos de seguimiento ad hoc y continuado (como el acceso al cubo de auditoría), así como recomendaciones sobre cómo utilizar mejor caja negra, SQL Server Profiler y xEvents encontrará a través de los vínculos en esta página: [Supervisar una instancia de Analysis Services](monitor-an-analysis-services-instance.md).  
  
##  <a name="bkmk_location"></a> Ubicación y tipos de registros  
 Analysis Services proporciona los registros que se describen a continuación.  
  
|Nombre de archivo o ubicación|Tipo|Se usa para|Activado de forma predeterminada|  
|---------------------------|----------|--------------|-------------------|  
|Msmdsrv.log|Registro de errores|Supervisión rutinaria y solución de problemas básicos|Sí|  
|Tabla OlapQueryLog en una base de datos relacional|Registro de consultas|Recopilación de entradas para el Asistente de optimización de uso|No|  
|Archivos SQLDmp\<guid > .mdmp archivos|Errores y excepciones|Solución de problemas a fondo|No|  
  
 Se recomienda el siguiente vínculo para recursos de información adicional que no se tratan en este tema: [Inicial sugerencias de recopilación de datos de Microsoft Support](https://blogs.msdn.com/b/as_emea/archive/2012/01/02/initial-data-collection-for-troubleshooting-analysis-services-issues.aspx).  
  
##  <a name="bkmk_general"></a> Información general sobre la configuración del archivo de registro  
 Puede encontrar secciones para cada registro en el archivo de configuración del servidor msmdsrv.ini, ubicado en la carpeta \Program Files\Microsoft SQL Server\MSAS12.MSSQLSERVER\OLAP\Config. Consulte en [Configure Server Properties in Analysis Services](../server-properties/server-properties-in-analysis-services.md) las instrucciones para editar el archivo.  
  
 Recomendados que, siempre que sea posible, establezca las propiedades de registros en la página de propiedades de servidor de Management Studio. No obstante, en algunos casos debe editar el archivo msmdsrv.ini directamente para configurar los valores que no están visibles en las herramientas administrativas.  
  
 ![Sección del archivo de configuración que muestra la configuración del registro](../media/ssas-logfilesettings.png "sección del archivo de configuración que muestra la configuración del registro")  
  
##  <a name="bkmk_msmdsrv"></a> Archivo de registro del servicio MSMDSRV  
 Analysis Services registra las operaciones del servidor en el archivo msmdsrv.log, uno por instancia, ubicado en \Archivos de programa\Microsoft SQL Server\\<instancia\>\Olap\Log.  
  
 Este archivo de registro se vacía en cada reinicio del servicio. En versiones anteriores, en ocasiones los administradores podían reiniciar el servicio con el único objetivo de vaciar el archivo de registro para evitar que creciera tanto que no pudiera usarse. Ya no es necesario. Las opciones de configuración, introducidas en SQL Server 2012 SP2 y versiones posteriores, le permiten controlar el tamaño del archivo de registro y su historial:  
  
-   `MaxFileSizeMB` especifica un tamaño de archivo de registro máximo en megabytes. El valor predeterminado es 256. Un valor de reemplazo válido debe ser un entero positivo. Cuando se alcanzan `MaxFileSizeMB`, Analysis Services cambia el nombre del archivo actual a msmdsrv{current timestamp}.log y empieza un nuevo archivo msmdsrv.log.  
  
-   `MaxNumberFiles` Especifica la retención de archivos de registro antiguos. El valor predeterminado es 0 (deshabilitado). Puede cambiarlo a un número entero positivo para mantener las versiones del archivo de registro. Cuando se alcanzan `MaxNumberFiles`, Analysis Services elimina el archivo con la marca de tiempo más antigua.  
  
 Para usar esta configuración, realice lo siguiente:  
  
1.  En el Bloc de notas, abra msmdsrv.ini.  
  
2.  Copie las dos líneas siguientes:  
  
    ```  
    <MaxFileSizeMB>256</MaxFileSizeMB>  
    <MaxNumberOfLogFiles>5</MaxNumberOfLogFiles>  
    ```  
  
3.  Pegue las dos líneas en la sección Log de msmdsrv.ini, a continuación del nombre de archivo msmdsrv.log. Ambos valores deben agregarse manualmente. No hay ningún marcador de posición para ellos en el archivo msmdsrv.ini.  
  
     El archivo con la configuración modificada debería ser similar al siguiente:  
  
    ```  
    <Log>  
    <File>msmdsrv.log</File>  
    <MaxFileSizeMB>256</MaxFileSizeMB>  
    <MaxNumberOfLogFiles>5</MaxNumberOfLogFiles>  
    <FileBufferSize>0</FileBufferSize>  
  
    ```  
  
4.  Edite los valores si los proporcionados difieren de lo que desea.  
  
5.  Guarde el archivo.  
  
6.  Reiniciar el servicio.  
  
##  <a name="bkmk_querylog"></a> Registros de consultas  
 Quizás "registro de consultas" sea un nombre poco apropiado, ya que no registra la actividad de consulta MDX o DAX de los usuarios. En su lugar, recopila datos sobre las consultas generadas por Analysis Services, que posteriormente se usan como entrada de datos en el Asistente para optimización basada en el uso. Los datos recopilados en el registro de consultas no se usan para realizar análisis directos. En concreto, los conjuntos de datos se describen en las matrices de bits, con un cero o uno que indican las partes del conjunto de datos que se incluyen en la consulta. De nuevo, estos datos sirven para el asistente.  
  
 Para realizar las tareas de supervisión y solución de problemas de consultas, muchos desarrolladores y administradores usan una herramienta de la comunidad, **ASTrace**. También puede utilizar SQL Server Profiler, xEvents o un seguimiento de Analysis Services. Consulte [Supervisar una instancia de Analysis Services](monitor-an-analysis-services-instance.md) para obtener vínculos relacionados con el seguimiento.  
  
 ¿Cuándo se debe utilizar el registro de consultas? Se recomienda habilitar el registro de consultas como parte de un ejercicio de ajuste de rendimiento de la consulta que incluye el Asistente para optimización basada en el uso. El registro de consultas no existe hasta que se habilite la característica, cree las estructuras de datos para admitirla y establece las propiedades que usa Analysis Services para localizar y rellenar el registro.  
  
 Para habilitar el registro de consultas, siga estos pasos:  
  
1.  Cree una base de datos relacional de SQL Server para almacenar el registro de consultas.  
  
2.  Conceda los permisos necesarios de la cuenta de servicio de Analysis Services en la base de datos. La cuenta necesita permisos para crear una tabla, escribir en ella y leer sus datos.  
  
3.  En SQL Server Management Studio, haga clic con el botón derecho en **Analysis Services** | **Propiedades** | **General**y establezca **CreateQueryLogTable** en true.  
  
4.  De manera opcional, cambie **QueryLogSampling** o **QueryLogTableName** si quiere tomar muestras de consultas a una tasa diferente o usar un nombre diferente para la tabla.  
  
 La tabla de registros de consultas no se creará hasta que haya ejecutado suficientes consultas MDX para cumplir los requisitos de muestreo. Por ejemplo, si mantiene el valor predeterminado de 10, debe ejecutar al menos 10 consultas antes de que se cree la tabla.  
  
 La configuración del registro de consultas se aplica a todo el servidor. La configuración que especifique se usará en todas las bases de datos que se ejecuten en este servidor.  
  
 ![Consultar la configuración del registro en Management Studio](../media/ssas-querylogsettings.png "configuración del registro de consultas en Management Studio")  
  
 Una vez especificados los ajustes de configuración, ejecute una consulta MDX varias veces. Si el muestreo está establecido en 10, ejecute la consulta 11 veces. Compruebe que se crea la tabla. En Management Studio, conecte el motor de base de datos relacional, abra la carpeta de la base de datos, abra la carpeta **Tablas** y compruebe que hay un archivo **OlapQueryLog** . Si no ve la tabla inmediatamente, actualice la carpeta para recoger cualquier cambio que haya en su contenido.  
  
 Permita que el registro de consultas acumule datos suficientes para el Asistente para optimización basada en el uso. Si los volúmenes de consultas son cíclicos, capture suficiente tráfico para tener un conjunto de datos representativo. Consulte [Asistente para optimización basada en el uso](https://msdn.microsoft.com/library/ms189706.aspx) para obtener instrucciones sobre cómo ejecutar el asistente.  
  
 Consulte [Configurar el registro de consultas de Analysis Services](https://technet.microsoft.com/library/Cc917676) para obtener más información acerca de la configuración del registro de consultas. Aunque la referencia es antigua, la configuración del registro de consultas no ha cambiado en las versiones recientes y la información que contiene se sigue aplicando.  
  
##  <a name="bkmk_mdmp"></a> Archivos de minivolcado (.mdmp)  
 Los archivos de volcado capturan los datos usados para analizar eventos extraordinarios. Analysis Services genera automáticamente archivos de minivolcado (.mdmp) en respuesta a un bloqueo del servidor, una excepción y determinados errores de configuración. La característica está habilitada, pero no envía informes de bloqueo de manera automática.  
  
 Los informes de bloqueo se configuran a través de la sección Exception en el archivo Msmdsrv.ini. Estos valores controlan la generación de archivos de volcado de memoria. El siguiente fragmento muestra los valores predeterminados:  
  
```  
<Exception>  
<CreateAndSendCrashReports>1</CreateAndSendCrashReports>  
<CrashReportsFolder/>  
<SQLDumperFlagsOn>0x0</SQLDumperFlagsOn>  
<SQLDumperFlagsOff>0x0</SQLDumperFlagsOff>  
<MiniDumpFlagsOn>0x0</MiniDumpFlagsOn>  
<MiniDumpFlagsOff>0x0</MiniDumpFlagsOff>  
<MinidumpErrorList>0xC1000000, 0xC1000001, 0xC102003F, 0xC1360054, 0xC1360055</MinidumpErrorList>  
<ExceptionHandlingMode>0</ExceptionHandlingMode>  
<CriticalErrorHandling>1</CriticalErrorHandling>  
<MaxExceptions>500</MaxExceptions>  
<MaxDuplicateDumps>1</MaxDuplicateDumps>  
</Exception>  
```  
  
 **Configurar informes de bloqueo**  
  
 A menos que el soporte técnico de Microsoft indique lo contrario, la mayoría de los administradores usan la configuración predeterminada. Este artículo de Knowledge Base anterior aún se utiliza para proporcionar instrucciones sobre cómo configurar los archivos de volcado de memoria: [Cómo configurar Analysis Services para generar archivos de volcado de memoria](https://support.microsoft.com/kb/919711).  
  
 El ajuste de configuración que se modificará con más probabilidad es `CreateAndSendCrashReports`, que se usa para determinar si se generará un archivo de volcado de memoria.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|0|Desactiva el archivo de volcado de memoria. Se omiten todas las demás opciones de la sección Exception.|  
|1|Habilita, pero no envía, el archivo de volcado de memoria (valor predeterminado).|  
|2|Habilita y envía automáticamente un informe de errores a Microsoft.|  
  
 `CrashReportsFolder` es la ubicación de los archivos de volcado. De forma predeterminada, un archivo .mdmp y los registros asociados se pueden encontrar en la carpeta \Olap\Log.  
  
 `SQLDumperFlagsOn` se usa para generar un volcado completo. De forma predeterminada, los volcados completos no están habilitados. Puede establecer esta propiedad en `0x34`.  
  
 En los vínculos siguientes encontrará más información:  
  
-   [Información más detallada sobre el uso de minivolcados en SQL Server](https://blogs.msdn.com/b/sqlcat/archive/2009/09/11/looking-deeper-into-sql-server-using-minidumps.aspx)  
  
-   [Cómo crear un archivo de volcado de modo de usuario](https://support.microsoft.com/kb/931673)  
  
-   [Cómo usar la utilidad Sqldumper.exe para generar un archivo de volcado en SQL Server](https://support.microsoft.com/kb/917825)  
  
##  <a name="bkmk_tips"></a> Sugerencias y prácticas recomendadas  
 Esta sección es un resumen de las sugerencias mencionadas en este artículo.  
  
-   Configure el archivo msmdsrv.log para controlar el tamaño y el número de archivos de registro msmdsrv. Estos ajustes no están habilitados de forma predeterminada, por lo que debe asegurarse de agregarlos después de la instalación. Consulte [Archivo de registro del servicio MSMDSRV](#bkmk_msmdsrv) en este tema.  
  
-   Revise esta entrada de blog de soporte técnico de Microsoft para obtener información sobre los recursos que se usan para obtener información sobre las operaciones del servidor: [Recopilación de datos iniciales](https://blogs.msdn.com/b/as_emea/archive/2012/01/02/initial-data-collection-for-troubleshooting-analysis-services-issues.aspx)  
  
-   Utilice ASTrace2012 en lugar de un registro de consultas para averiguar quién está consultando los cubos. El registro de consultas se usa normalmente para proporcionar datos al Asistente para la optimización basada en el uso. Los datos que captura no se leen o interpretan fácilmente. ASTrace2012 es una herramienta de la comunidad ampliamente utilizada que captura las operaciones de consulta. Consulte [ejemplos de la Comunidad de Microsoft SQL Server: Analysis Services](https://sqlsrvanalysissrvcs.codeplex.com/).  
  
## <a name="see-also"></a>Vea también  
 [Administración de una instancia de Analysis Services](analysis-services-instance-management.md)   
 [Introducción a Supervisar Analysis Services con SQL Server Profiler](introduction-to-monitoring-analysis-services-with-sql-server-profiler.md)   
 [Configurar las propiedades del servidor en Analysis Services](../server-properties/server-properties-in-analysis-services.md)  
  
  
