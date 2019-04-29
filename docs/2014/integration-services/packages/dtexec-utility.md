---
title: DTExec (utilidad) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 7b6867fa-1039-49b3-90fb-85b84678a612
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 540f600d5005e8288aafe19ef59d4b7e894a99b0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62890245"
---
# <a name="dtexec-utility"></a>DTExec (utilidad)
  El `dtexec` utilidad de símbolo del sistema se usa para configurar y ejecutar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] paquetes. El `dtexec` utilidad proporciona acceso a todas las paquete configuración y ejecución de características, como parámetros, conexiones, propiedades, variables, registro y los indicadores de progreso. El `dtexec` utilidad le permite cargar paquetes desde estos orígenes: el [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] server, un archivo de proyecto .ispac, una [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de datos, el [!INCLUDE[ssIS](../../includes/ssis-md.md)] paquete Store y el sistema de archivos.  
  
> [!NOTE]  
>  Cuando se usa la versión de la `dtexec` utilidad que se incluye con [!INCLUDE[ssISversion11](../../includes/ssisversion11-md.md)] para ejecutar un [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] o un [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] paquete, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] actualiza temporalmente el paquete a [!INCLUDE[ssISversion11](../../includes/ssisversion11-md.md)]. Sin embargo, no puede usar el `dtexec` utilidad para guardar estos cambios actualizados. Para obtener más información acerca de cómo actualizar de forma permanente un paquete a [!INCLUDE[ssISversion11](../../includes/ssisversion11-md.md)], consulte [actualizar paquetes de Integration Services](../install-windows/upgrade-integration-services-packages.md).  
  
 En este tema, se incluyen las siguientes secciones:  
  
-   [Servidor de Integration Services y el archivo de proyecto](#server)  
  
-   [Consideraciones sobre la instalación en equipos de 64 bits](#bit)  
  
-   [Consideraciones sobre los equipos con instalaciones en paralelo](#side)  
  
-   [Fases de ejecución](#phases)  
  
-   [Códigos de salida devueltos](#exit)  
  
-   [Reglas de sintaxis](#syntaxRules)  
  
-   [Usar dtexec desde xp_cmdshell](#cmdshell)  
  
-   [Sintaxis](#syntax)  
  
-   [Parámetros](#parameter)  
  
-   [Comentarios](#remark)  
  
-   [Ejemplos](#example)  
  
##  <a name="server"></a> Servidor de Integration Services y el archivo de proyecto  
 Cuando usas `dtexec` para ejecutar paquetes en el [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] server, `dtexec` llamadas la [catalog.create_execution &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database), [catalog.set_execution_parameter_ valor &#40;base de datos de SSISDB&#41; ](/sql/integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database) y [catalog.start_execution &#40;base de datos de SSISDB&#41; ](/sql/integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database) procedimientos almacenados para crear una ejecución, establecer valores de parámetro e iniciar el ejecución. Todos los registros de ejecución pueden verse en el servidor en las vistas relacionadas o mediante informes estándar disponibles en [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]. Para obtener más información acerca de los informes, vea [informes para el servidor de Integration Services](../reports-for-the-integration-services-server.md).  
  
 El siguiente es un ejemplo de ejecución de un paquete en el [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] server.  
  
```  
DTExec /ISSERVER "\SSISDB\folderB\Integration Services Project17\Package.dtsx" /SERVER "." /Envreference 2 /Par "$Project::ProjectParameter(Int32)";1 /Par "Parameter(Int32)";21 /Par "CM.sqlcldb2.SSIS_repro.InitialCatalog";ssisdb /Par "$ServerOption::SYNCHRONIZED(Boolean)";True  
```  
  
 Cuando usas `dtexec` para ejecutar un paquete desde el archivo de proyecto .ispac, las opciones relacionadas son: /Proj [ect] y /Pack [age], que se usan para especificar el nombre de la secuencia de ruta de acceso y el paquete del proyecto. Al convertir un proyecto al modelo de implementación de proyectos ejecutando el **Integration Services Project Conversion Wizard** desde [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], el asistente genera un archivo Project. Para obtener más información, consulte [Deploy Projects to Integration Services Server](../deploy-projects-to-integration-services-server.md).  
  
 Puede usar `dtexec` con terceros de programación de herramientas para programar paquetes que se implementan en el [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] server.  
  
##  <a name="bit"></a> Consideraciones sobre la instalación en equipos de 64 bits  
 En un equipo de 64 bits, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] instala una versión de 64 bits de la `dtexec` utilidad (dtexec.exe). Si tiene que ejecutar ciertos paquetes en modo de 32 bits, tendrá que instalar la versión de 32 bits de la `dtexec` utilidad. Para instalar la versión de 32 bits de la `dtexec` utilidad, debe seleccionar herramientas cliente o [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] durante la instalación.  
  
 De forma predeterminada, un equipo de 64 bits que tiene las versiones de 64 bits y 32 bits de un [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] instalada la utilidad de línea de comandos ejecutará la versión de 32 bits en el símbolo del sistema. La versión de 32 bits se ejecuta porque la ruta del directorio para la versión de 32 bits aparece en la variable de entorno PATH antes de la ruta de acceso de directorio para la versión de 64 bits. (Normalmente, es la ruta de acceso del directorio de 32 bits  *\<unidad >*: \Program \Microsoft SQL Server\110\DTS\Binn archivos (x86), mientras que la ruta de acceso del directorio de 64 bits es  *\<unidad >*: \ Programa de programa\Microsoft SQL Server\110\DTS\Binn).  
  
> [!NOTE]  
>  Si utiliza al Agente SQL Server para ejecutar la utilidad, Agente SQL Server utiliza automáticamente la versión de 64 bits de la utilidad. Agente SQL Server usa el registro, no la variable de entorno PATH, para encontrar el ejecutable correcto para la utilidad.  
  
 Para asegurarse de que ejecuta la versión de 64 bits de la utilidad en el símbolo del sistema, puede realizar una de las siguientes acciones:  
  
-   Abra una ventana de símbolo del sistema, cambie al directorio que contiene la versión de 64 bits de la utilidad (*\<unidad >*: \Program Files\Microsoft SQL Server\110\DTS\Binn), y, a continuación, ejecute la utilidad desde esa ubicación.  
  
-   En el símbolo del sistema, ejecute la utilidad escribiendo la ruta de acceso completa (*\<unidad >*: \Program Files\Microsoft SQL Server\110\DTS\Binn) a la versión de 64 bits de la utilidad.  
  
-   Cambie de forma permanente el orden de las rutas de acceso en la variable de entorno PATH colocando la ruta de acceso de 64 bits (*\<unidad >*: \Program Files\Microsoft SQL Server\110\DTS\Binn) antes de la ruta de acceso de 32 bits ( *\<unidad >*: \ \Microsoft SQL Server\110\DTS\Binn (x86) los archivos de programa) en la variable.  
  
##  <a name="side"></a> Consideraciones sobre los equipos con instalaciones en paralelo  
 Cuando [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] está instalado en un equipo que tenga [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] o [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] instalada, varias versiones de la `dtexec` utilidad están instalados.  
  
 Para asegurarse de que ejecuta la versión correcta de la utilidad, en el símbolo que se ejecute la utilidad escribiendo la ruta de acceso completa (*\<unidad >*: \Program Files\Microsoft SQL Server\\< versión\>\ DTS\Binn).  
  
##  <a name="phases"></a> Fases de ejecución  
 La utilidad tiene cuatro fases que pasa a través de mientras se ejecuta. Las fases son como sigue:  
  
1.  Fase de origen de comando: El símbolo del sistema lee la lista de opciones y argumentos que se han especificado. ¿Todas las fases posteriores se omiten si un **/?** o **/ayuda** se encontró la opción.  
  
2.  Fase de carga del paquete: El paquete especificado por el `/SQL`, **/archivo**, o `/DTS` opción se carga.  
  
3.  Fase de configuración: Las opciones se procesan en este orden:  
  
    -   Opciones que establecen las marcas de paquetes, variables y propiedades.  
  
    -   Opciones que comprueban la versión del paquete y de compilación.  
  
    -   Opciones que permiten configurar el comportamiento de tiempo de ejecución de la utilidad, como los informes.  
  
4.  Fase de ejecución y validación: El paquete se ejecuta o se valida sin ejecutarse si el **/validar** especificó la opción.  
  
##  <a name="exit"></a> Códigos de salida devueltos  
 **Códigos de salida devueltos por la utilidad dtexec**  
  
 Cuando se ejecuta un paquete, `dtexec` puede devolver un código de salida. El código de salida se usa para rellenar la variable ERRORLEVEL, cuyo valor se puede probar en instrucciones condicionales o lógica de bifurcación dentro de un archivo por lotes. En la tabla siguiente se enumera los valores que el `dtexec` utilidad puede establecer al salir.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|0|El paquete se ejecutó correctamente.|  
|1|Error en el paquete.|  
|3|El paquete cancelado por el usuario.|  
|4|La utilidad no pudo localizar el paquete solicitado. No se encontró el paquete.|  
|5|La utilidad no pudo cargar el paquete solicitado. No se pudo cargar el paquete.|  
|6|La utilidad encontró un error interno de los errores sintácticos o semánticos en la línea de comandos.|  
  
##  <a name="syntaxRules"></a> Reglas de sintaxis  
 **Reglas de sintaxis de la utilidad**  
  
 Todas las opciones deben comenzar con una barra diagonal (/) o un signo menos (-). Las opciones que se muestran aquí se inician con una barra diagonal (/), pero se puede sustituir el signo menos (-).  
  
 Un argumento debe estar entre comillas si contiene un espacio. Si el argumento no está entre comillas, el argumento no puede contener espacios en blanco.  
  
 Las dobles comillas dentro de las cadenas entre comillas representan comillas simples con escape.  
  
 Opciones y argumentos no distinguen mayúsculas de minúsculas, excepto por las contraseñas.  
  
##  <a name="cmdshell"></a> Usar dtexec desde xp_cmdshell  
 **Usar dtexec desde xp_cmdshell**  
  
 Puede ejecutar dtexec desde el **xp_cmdshell** símbolo del sistema. El ejemplo siguiente muestra cómo ejecutar un paquete denominado UpsertData.dtsx y pasar por alto el código de retorno:  
  
```  
EXEC xp_cmdshell 'dtexec /f "C:\UpsertData.dtsx"'  
```  
  
 El ejemplo siguiente muestra cómo ejecutar el mismo paquete y capturar el código de retorno:  
  
```  
DECLARE @returncode int  
EXEC @returncode = xp_cmdshell 'dtexec /f "C:\UpsertData.dtsx"'  
```  
  
> [!IMPORTANT]  
>  En [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], **xp_cmdshell** opción está deshabilitada de forma predeterminada en las instalaciones nuevas. La opción puede habilitarse ejecutando el **sp_configure** procedimiento almacenado del sistema. Para obtener más información, consulte [xp_cmdshell Server Configuration Option](../../database-engine/configure-windows/xp-cmdshell-server-configuration-option.md).  
  
##  <a name="syntax"></a> Sintaxis  
  
```  
dtexec /option [value] [/option [value]]...  
```  
  
##  <a name="parameter"></a> Parámetros  
  
-   **/?** [*option_name*]: Opcional. Muestra las opciones de línea de comandos o muestra ayuda para el elemento especificado *option_name* y, a continuación, cierra la utilidad.  
  
     Si especifica un *option_name* argumento, `dtexec` inicia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] libros en pantalla y muestra el tema utilidad dtexec.  
  
-   **/Ca[llerInfo]**:   
                  Opcional. Especifica información adicional para la ejecución del paquete. Al ejecutar un paquete con el Agente SQL Server, el agente establece este argumento para indicar que la ejecución del paquete se invoca al Agente SQL Server. Este parámetro se omite cuando el `dtexec` utilidad se ejecuta desde la línea de comandos.  
  
-   **/CheckF [ile]** _filespec_:   
                  Opcional. Establece el `CheckpointFileName` propiedad del paquete en la ruta de acceso y el archivo especificados en *filespec*. Este archivo se usa cuando se reinicia el paquete. Si se especifica esta opción y se proporciona ningún valor para el nombre de archivo, el `CheckpointFileName` para el paquete se establece en una cadena vacía. Si no se especifica esta opción, se conservan los valores en el paquete.  
  
-   **/Checkp [ointing]** _{on\off}_:   
                  Opcional. Establece un valor que determina si el paquete usará puntos de comprobación durante la ejecución del paquete. El valor **en** especifica que un paquete con error se va a ejecutar. Cuando se vuelve a ejecutar el paquete con error, el motor de tiempo de ejecución utiliza el archivo de punto de comprobación para reiniciar el paquete desde el punto de error.  
  
     El valor predeterminado es en si la opción se declara sin un valor. Se producirá un error en la ejecución del paquete si el valor está activado y no se encuentra el archivo de punto de comprobación. Si no se especifica esta opción, se conserva el valor establecido en el paquete. Para obtener más información, vea [Reiniciar paquetes de usando puntos de comprobación](restart-packages-by-using-checkpoints.md).  
  
     El **/CheckPointing en** opción de dtexec es equivalente a establecer el `SaveCheckpoints` propiedad del paquete en True y el `CheckpointUsage` propiedad como siempre.  
  
-   **/Com[mandFile]** _filespec_:   
                  (Opcional). Especifica las opciones de comando que se ejecutan con `dtexec`. El archivo especificado en *filespec* se abre y se leen sus opciones desde el archivo hasta que se encuentra EOF en el archivo. *filespec* es un archivo de texto. El *filespec* argumento especifica el nombre de archivo y ruta de acceso del archivo de comandos para asociar a la ejecución del paquete.  
  
-   **/Conf[igFile]** _filespec_: Opcional. Especifica un archivo de configuración que se extraerán valores. Con esta opción, puede establecer una configuración de tiempo de ejecución que difiera de la configuración que se especificó en tiempo de diseño para el paquete. Puede almacenar valores de configuración diferentes en un archivo de configuración XML y, a continuación, cargar la configuración antes de la ejecución del paquete mediante el uso de la **/configFile** opción.  
  
     Puede usar el **/configFile** opción para cargar configuraciones adicionales en tiempo de ejecución que no especificó en tiempo de diseño. Sin embargo, no puede usar el **/configFile** opción para reemplazar los valores configurados que también especificó en tiempo de diseño. Para comprender cómo se aplican las configuraciones de paquetes, consulte [las configuraciones de paquetes](../package-configurations.md).  
  
-   **/Conn [ection]** _id_or_name; connection_string [[; id_or_name; connection_string]...]_ :   
                  Opcional. Especifica que el Administrador de conexiones con el GUID o el nombre especificado se encuentra en el paquete y especifica una cadena de conexión.  
  
     Esta opción requiere que se especifiquen ambos parámetros: el nombre de administrador de conexiones o GUID debe proporcionarse en el *id_or_name* argumento y una cadena de conexión válida deben especificarse en el *connection_string* argumento. Para obtener más información, consulte [Integration Services &#40;SSIS&#41; conexiones](../connection-manager/integration-services-ssis-connections.md).  
  
     En tiempo de ejecución, puede usar el **/Connection** opción para cargar las configuraciones de paquetes desde una ubicación distinta de la ubicación que especificó en tiempo de diseño. Los valores de estas configuraciones, a continuación, reemplazan los valores que se especificaron originalmente. Sin embargo puede usar el **/Connection** opción solo para las configuraciones, como [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que usen un administrador de conexiones. Para comprender cómo se aplican las configuraciones de paquetes, consulte [las configuraciones de paquetes](../package-configurations.md) y [cambios de comportamiento en las características de Integration Services en SQL Server 2014](../behavior-changes-to-integration-services-features-in-sql-server-2014.md).  
  
-   **/Cons[oleLog]** [[*displayoptions*];[*list_options*;*src_name_or_guid*]...]: Opcional. Muestra especificado las entradas del registro en la consola durante la ejecución del paquete. Si se omite esta opción, no hay entradas del registro se muestran en la consola. Si se especifica la opción sin parámetros que limiten la visualización, se mostrará cada entrada de registro. Para limitar las entradas que se muestran en la consola, puede especificar las columnas que se va a mostrar con el *displayoptions* parámetro y limitar los tipos de la entrada de registro mediante el uso de la *list_options* parámetro.  
  
    > [!NOTE]  
    >  Al ejecutar un paquete en el [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] servidor mediante el `/ISSERVER` , parámetro de salida de la consola está limitada y la mayoría de los **/cons [oleLog]** opciones no son aplicables. Todos los registros de ejecución pueden verse en el servidor en las vistas relacionadas o mediante informes estándar disponibles en [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]. Para obtener más información acerca de los informes, vea [informes para el servidor de Integration Services](../reports-for-the-integration-services-server.md).  
  
     El *displayoptions* valores son los siguientes:  
  
    -   N (nombre)  
  
    -   C (equipo)  
  
    -   O (operador)  
  
    -   S (nombre de origen)  
  
    -   G (GUID de origen)  
  
    -   X (GUID de ejecución)  
  
    -   M (mensaje)  
  
    -   T (hora de inicio y final)  
  
     El *list_options* valores son los siguientes:  
  
    -   *Puedo* -especifica la lista de inclusión. Solo los nombres de origen o GUID que se especifican se registran.  
  
    -   *E* -especifica la lista de exclusión. No se registran los nombres de origen o GUID que se especifican.  
  
    -   El *src_name_or_guid* los parámetros especificados para la inclusión o exclusión es un nombre de evento, nombre de origen o GUID de origen.  
  
     Si utiliza varias **/ConsoleLog** opciones en el mismo símbolo, interactúan como sigue:  
  
    -   Su orden de aparición no tiene ningún efecto.  
  
    -   Si no hay ninguna lista de inclusión está presente en la línea de comandos, las listas de exclusión se aplican a todos los tipos de entradas de registro.  
  
    -   Si las listas de inclusión están presentes en la línea de comandos, las listas de exclusión se aplican a la unión de todas las listas de inclusión.  
  
     Para obtener ejemplos de la **/ConsoleLog** opción, vea el **comentarios** sección.  
  
-   **/D[ts]** _package_path_:   
                  Opcional. Carga un paquete de SSIS paquete Store. Los paquetes almacenados en el Store del paquete de SSIS, se implementan utilizando el modelo de implementación de paquetes heredados. Para ejecutar paquetes que se implementan en el [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] servidor mediante el modelo de implementación de proyectos, use el `/ISServer` opción. Para obtener más información acerca de los modelos de implementación de paquete y proyecto, vea [implementación de proyectos y paquetes](deploy-integration-services-ssis-projects-and-packages.md).  
  
     El *package_path* argumento especifica la ruta de acceso relativa de la [!INCLUDE[ssIS](../../includes/ssis-md.md)] empaquetar, empezando por la raíz de Store de paquete de SSIS e incluye el nombre de la [!INCLUDE[ssIS](../../includes/ssis-md.md)] paquete. Si el nombre de archivo o ruta de acceso especificada en el *package_path* argumento contiene un espacio, debe escribir entre comillas el *package_path* argumento.  
  
     El `/DTS` opción no se puede usar junto con el `/File` o `/SQL` opción. Si se especifican varias opciones, `dtexec` se produce un error.  
  
-   **/De[crypt]**  _password_: Opcional. Establece la contraseña de descifrado que se utiliza cuando carga un paquete con cifrado de contraseña.  
  
-   **/Dump** _código de error_:  
                  Opcional crea el volcado de depuración de archivos, .mdmp y .tmp, cuando se producen uno o varios eventos especificados mientras se ejecuta el paquete. El *código de error* argumento especifica el tipo de información, advertencia o error de código de evento-que activará el sistema para crear archivos de volcado de depuración. Para especificar varios códigos de evento, separe cada *código de error* argumento por un punto y coma (;). No incluya comillas con el *código de error* argumento.  
  
     El ejemplo siguiente genera los archivos de volcado de depuración cuando se produce el error DTS_E_CANNOTACQUIRECONNECTIONFROMCONNECTIONMANAGER.  
  
    ```  
    /Dump 0xC020801C  
    ```  
  
     De forma predeterminada, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] almacena los archivos de volcado de depuración en la carpeta  *\<unidad >*: \Program Files\Microsoft SQL Server\110\Shared\ErrorDumps.  
  
    > [!NOTE]  
    >  Depurar archivos de volcado de memoria pueden contener información confidencial. Usar una lista de control de acceso (ACL) para restringir el acceso a los archivos, o copie los archivos en una carpeta con acceso restringido. Por ejemplo, antes de enviar que a Microsoft los archivos de depuración de servicios de soporte técnico, se recomienda que quite cualquier información importante o confidencial.  
  
     Para aplicar esta opción a todos los paquetes que el `dtexec` ejecuciones de utilidad, agregue un **DumpOnCodes** valor REG_SZ a la clave del Registro HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\SSIS\Setup\DtsPath. El valor de datos en **DumpOnCodes** especifica el código de error o códigos que desencadenarán el sistema para crear archivos de volcado de depuración. Varios códigos de error deben estar separados por puntos y coma (;).  
  
     Si agrega un **DumpOnCodes** valor a la clave del registro y usar el **/Dump** opción, el sistema creará archivos de volcado de depuración que se basan en ambos valores.  
  
     Para obtener más información sobre los archivos de volcado de depuración, consulte [Generating Dump Files for Package Execution](../troubleshooting/generating-dump-files-for-package-execution.md).  
  
-   **/DumpOnError**:   
                  Opcional. Crea los archivos de volcado de depuración, .mdmp y .tmp, cuando se produce un error mientras se ejecuta el paquete.  
  
     De forma predeterminada, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] almacena los archivos de volcado de depuración en la carpeta  *\<unidad >*: carpeta \Archivos de \Program Files\Microsoft SQL Server\110\Shared\ErrorDumps.  
  
    > [!NOTE]  
    >  Depurar archivos de volcado de memoria pueden contener información confidencial. Usar una lista de control de acceso (ACL) para restringir el acceso a los archivos, o copie los archivos en una carpeta con acceso restringido. Por ejemplo, antes de enviar que a Microsoft los archivos de depuración de servicios de soporte técnico, se recomienda que quite cualquier información importante o confidencial.  
  
     Para aplicar esta opción a todos los paquetes que el `dtexec` ejecuciones de utilidad, agregue un **DumpOnError** valor REG_DWORD a la clave del Registro HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\SSIS\Setup\DtsPath. El valor de la **DumpOnError** valor REG_DWORD determina si el **/DumpOnError** opción debe utilizarse con el `dtexec` utilidad:  
  
    -   Un valor distinto de cero indica que el sistema creará archivos de volcado de depuración cuando se produce algún error, independientemente de si usa la **/DumpOnError** opción con la `dtexec` utilidad.  
  
    -   Un valor cero indica que el sistema no creará la depuración archivos de volcado de memoria a menos que use el **/DumpOnError** opción con la `dtexec` utilidad.  
  
     Para obtener más información sobre los archivos de volcado de depuración, consulte [Generating Dump Files for Package Execution](../troubleshooting/generating-dump-files-for-package-execution.md)  
  
-   `/Env[Reference]` *Id. de referencia de entorno*:   
                  Opcional. Especifica la referencia de entorno (ID) que se usa por la ejecución del paquete, para un paquete que se implementa en el [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] server. Los parámetros configurados para enlazar las variables usará los valores de las variables que se encuentran en el entorno.  
  
     Usa `/Env[Reference]` opción junto con el `/ISServer` y `/Server` opciones.  
  
     Este parámetro se utiliza el Agente SQL Server.  
  
-   **/F [ile]** _filespec_:   
                  Opcional. Carga un paquete que se guarda en el sistema de archivos. Paquetes que se guardan en el sistema de archivos, se implementan mediante el modelo de implementación de paquetes heredados. Para ejecutar paquetes que se implementan en el [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] servidor mediante el modelo de implementación de proyectos, use el `/ISServer` opción. Para obtener más información acerca de los modelos de implementación de paquete y proyecto, vea [implementación de proyectos y paquetes](deploy-integration-services-ssis-projects-and-packages.md)  
  
     El *filespec* argumento especifica la ruta de acceso y el nombre del paquete. Puede especificar la ruta de acceso como una ruta de acceso de convención de nomenclatura Universal (UNC) o una ruta de acceso local. Si el nombre de archivo o ruta de acceso especificada en el *filespec* argumento contiene un espacio, debe escribir entre comillas el *filespec* argumento.  
  
     El `/File` opción no se puede usar junto con el `/DTS` o `/SQL` opción. Si se especifican varias opciones, `dtexec` se produce un error.  
  
-   **/H [elp]** [*option_name*]: Opcional. Muestra ayuda para las opciones, o muestra ayuda para el elemento especificado *option_name* y cierra la utilidad.  
  
     Si especifica un *option_name* argumento, `dtexec` inicia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] libros en pantalla y muestra el tema utilidad dtexec.  
  
-   `/ISServer` *PackagePath*:  
                  Opcional. Se ejecuta un paquete que se implementa en el [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] server. El *PackagePath* argumento especifica la ruta de acceso y el nombre completo del paquete implementado en el [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] server. Si el nombre de archivo o ruta de acceso especificada en el *PackagePath* argumento contiene un espacio, debe escribir entre comillas el *PackagePath* argumento.  
  
     El formato de paquete es como sigue:  
  
    ```  
    \<catalog name>\<folder name>\<project name>\package file name  
    ```  
  
     Usa `/Server` opción junto con el `/ISSERVER` opción. Autenticación de Windows sólo puede ejecutar un paquete en el servidor SSIS. El usuario actual de Windows se usa para tener acceso al paquete. Si se omite la opción/Server, la instancia local predeterminada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se da por hecho.  
  
     El `/ISSERVER` opción no se puede usar junto con el `/DTS`, `/SQL` o `/File` opción. Si se especifican varias opciones, dtexec devuelve un error.  
  
     Este parámetro se utiliza el Agente SQL Server.  
  
-   **/L[ogger]** _classid_orprogid;configstring_:  
                  Opcional. Asocia uno o varios proveedores de registro de la ejecución de un [!INCLUDE[ssIS](../../includes/ssis-md.md)] paquete. El *classid_orprogid* parámetro especifica el proveedor de registro y puede especificarse como GUID de clase. El *configstring* es la cadena que se usa para configurar el proveedor de registro.  
  
     En la lista siguiente se muestra los proveedores de registro disponibles:  
  
    -   Archivo de texto:  
  
        -   ProgID: DTS.LogProviderTextFile.1  
  
        -   ClassID: {59B2C6A5-663F-4C20-8863-C83F9B72E2EB}  
  
    -   [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]:  
  
        -   ProgID: DTS.LogProviderSQLProfiler.1  
  
        -   ClassID: {5C0B8D21-E9AA-462E-BA34-30FF5F7A42A1}  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
        -   ProgID: DTS.LogProviderSQLServer.1  
  
        -   ClassID: {6AA833A1-E4B2-4431-831B-DE695049DC61}  
  
    -   Registro de eventos de Windows:  
  
        -   ProgID: DTS.LogProviderEventLog.1  
  
        -   ClassID: {97634F75-1DC7-4F1F-8A4C-DAF0E13AAA22}  
  
    -   Archivo XML:  
  
        -   ProgID: DTS.LogProviderXMLFile.1  
  
        -   ClassID: {AFED6884-619C-484F-9A09-F42D56E1A7EA}  
  
-   **/M[axConcurrent]** _concurrent_executables_:  
                  Opcional. Especifica el número de archivos ejecutables que el paquete puede ejecutar simultáneamente. El valor especificado debe ser un entero no negativo o -1. El valor -1 significa que [!INCLUDE[ssIS](../../includes/ssis-md.md)] permitirá un número máximo de ejecutables que es iguales al número total de procesadores del equipo que ejecuta el paquete, más dos en ejecución simultánea.  
  
-   **/Pack[age]** _PackageName_:  
                  Opcional. Especifica el paquete que se ejecuta. Este parámetro se utiliza principalmente al ejecutar el paquete desde [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)].  
  
-   **/P [assword]** _contraseña_:  
                  Opcional. Permite la recuperación de un paquete que está protegido por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación. Esta opción se utiliza junto con el **/User** opción. Si el **/Password** opción se omite y el **/User** se usa la opción, se usa una contraseña en blanco. El *contraseña* valor puede ir entre comillas.  
  
    > [!IMPORTANT]  
    >  [!INCLUDE[ssNoteWinAuthentication](../../../includes/ssnotewinauthentication-md.md)]  
  
-   **/Par[ameter]** [$Package:: | $Project:: | $ServerOption::] *parameter_name* [(data_type)]; *literal_value*: Opcional. Especifica los valores de parámetro. Varios **/parámetro** se pueden especificar las opciones. Los tipos de datos son CLR TypeCodes como cadenas. Para un parámetro que no son de cadena, el tipo de datos se especifica entre paréntesis después del nombre de parámetro.  
  
     El **/parámetro** opción puede utilizarse solo con el `/ISServer` opción.  
  
     Utilice los prefijos $Package, $Project y $ServerOption para indicar un parámetro de paquete, el parámetro de proyecto y un parámetro de servidor, respectivamente. El tipo de parámetro predeterminado es paquete.  
  
     El siguiente es un ejemplo de ejecución de un paquete y se proporciona myvalue para el parámetro de proyecto (myparam) y el valor entero 12 para el parámetro de paquete (anotherparam).  
  
     `Dtexec /isserver "SSISDB\MyFolder\MyProject\MyPackage.dtsx" /server "." /parameter $Project::myparam;myvalue /parameter anotherparam(int32);12`  
  
     También puede establecer conexión propiedades del administrador mediante el uso de parámetros. Use el prefijo CM para denotar un parámetro de conexión de administrador.  
  
     En el ejemplo siguiente, la propiedad InitialCatalog del Administrador de conexiones SourceServer se establece en `ssisdb`.  
  
    ```  
    /parameter CM.SourceServer.InitialCatalog;ssisdb  
    ```  
  
     En el ejemplo siguiente, la propiedad ServerName del Administrador de conexiones SourceServer se establece en un punto (.) para indicar el servidor local.  
  
    ```  
    /parameter CM.SourceServer.ServerName;.  
    ```  
  
-   **/Proj[ect]** _ProjectFile_:  
                  Opcional. Especifica el proyecto desde el que se va a recuperar el paquete que se ejecuta. El *ProjectFile* argumento especifica el nombre del archivo .ispac. Este parámetro se utiliza principalmente al ejecutar el paquete desde [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)].  
  
-   **/ Rem** _comentario_:  
                  Opcional. Incluye comentarios en el símbolo del sistema o en archivos de comandos. El argumento es opcional. El valor de *comentario* es una cadena que debe incluirse entre comillas o no contener ningún espacio en blanco. Si no se especifica ningún argumento, se inserta una línea en blanco. Los valores de*comment* se descartan durante la fase de origen de comandos.  
  
-   **/Rep [orting]** _nivel_ [*; event_guid_or_name*[*; event_guid_or_name*[...]]: Opcional. Especifica qué tipos de mensajes que se notificarán. Opciones de los informes disponibles para *nivel* son los siguientes:  
  
     **N** ningún informe.  
  
     `E` Los errores se notifican.  
  
     **W** se notifican las advertencias.  
  
     `I` Se notifican los mensajes informativos.  
  
     **C** se notifican los eventos personalizados.  
  
     **D.** se notifican los eventos de tarea de flujo de datos.  
  
     **P** se informa del progreso.  
  
     **V** informes detallados.  
  
     Los argumentos V y N se excluyen mutuamente para todos los demás argumentos; deben especificarse solas. Si el **/Reporting** opción no se especifica, el nivel predeterminado es `E` (errores), **W** (advertencias) y **P** (progreso).  
  
     Todos los eventos van precedidos de una marca de tiempo en el formato "MM/DD/AA hh: mm:" y un GUID o nombre descriptivo si está disponible.  
  
     El parámetro opcional *event_guid_or_name* es una lista de excepciones para los proveedores de registro. La excepción especifica los eventos que no se ha iniciado la sesión que en caso contrario, es posible que se han registrado.  
  
     No es necesario excluir un evento si el evento no se registra habitualmente de forma predeterminada  
  
-   **/Res[tart]** {*deny | force | ifPossible*}: Opcional. Especifica un nuevo valor para el <xref:Microsoft.SqlServer.Dts.Runtime.Package.CheckpointUsage%2A> propiedad del paquete. El significado de los parámetros son los siguientes:  
  
     *Denegar* conjuntos <xref:Microsoft.SqlServer.Dts.Runtime.Package.CheckpointUsage%2A> propiedad <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSCheckpointUsage.DTSCU_NEVER>.  
  
     *Forzar* conjuntos <xref:Microsoft.SqlServer.Dts.Runtime.Package.CheckpointUsage%2A> propiedad <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSCheckpointUsage.DTSCU_ALWAYS>.  
  
     *ifPossible* conjuntos <xref:Microsoft.SqlServer.Dts.Runtime.Package.CheckpointUsage%2A> propiedad <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSCheckpointUsage.DTSCU_IFEXISTS>.  
  
     El valor predeterminado de **forzar** se utiliza si se especifica ningún valor.  
  
-   **/Set** [$Sensitive::]*propertyPath;value*: Opcional. Invalida la configuración de un parámetro, variable, propiedad, contenedor, proveedor de registro, enumerador Foreach o conexión en un paquete. Cuando se usa esta opción, **/Set** cambios el *propertyPath* argumento en el valor especificado. Varios **/Set** opciones se pueden especificar.  
  
     Además de utilizar el **/conjunto de** opción con la **/F [ile]** opción, también puede usar el **/conjunto** opción con el `/ISServer` opción o el `/Project` opción. Cuando se usa **/Set** con `/Project`, **/Set** establece los valores de parámetro. Cuando usas **/Set** con `/ISServer`, **/Set** establece invalidaciones de propiedad. Además, cuando usa **/Set** con `/ISServer`, puede usar el prefijo opcional $Sensitive para indicar que la propiedad se debe tratar como confidencial en el [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] server.  
  
     Puede determinar el valor de *propertyPath* ejecutando el Asistente para configuración de paquetes. Las rutas de acceso para los elementos que seleccione se muestran en la última **finalización del asistente** página y se pueden copiar y pegar. Si ha utilizado al Asistente solo para este propósito, puede cancelar al asistente después de copiar las rutas de acceso.  
  
     Este es un ejemplo de ejecución de un paquete que se guarda en el sistema de archivos y proporcionando un nuevo valor para una variable:  
  
     `dtexec /f mypackage.dtsx /set \package.variables[myvariable].Value;myvalue`  
  
     El siguiente ejemplo se ejecuta un paquete desde el proyecto de .ispac de archivos y configuración de parámetros de paquete y proyecto.  
  
     `/Project c:\project.ispac /Package Package1.dtsx /SET \Package.Variables[$Package::Parameter];1 /SET \Package.Variables[$Project::Parameter];1`  
  
     Puede usar el **/Set** opción para cambiar la ubicación del paquete que se cargan las configuraciones. Sin embargo, no puede usar el **/Set** opción para invalidar un valor que se especificó en una configuración en tiempo de diseño. Para comprender cómo se aplican las configuraciones de paquetes, consulte [las configuraciones de paquetes](../package-configurations.md) y [cambios de comportamiento en las características de Integration Services en SQL Server 2014](../behavior-changes-to-integration-services-features-in-sql-server-2014.md).  
  
-   `/Ser[ver]` *server*:  
                  Opcional. Cuando el `/SQL` o `/DTS` , esta opción especifica el nombre del servidor desde el que se va a recuperar el paquete. Si se omite el `/Server` opción y la `/SQL` o `/DTS` se especifica la opción, se intenta la ejecución del paquete en el servidor local. El *server_instance* valor puede ir entre comillas.  
  
     El `/Ser[ver]` opción es necesaria cuando el `/ISServer` se especifica la opción.  
  
-   **/SQ [L]** _package_path_:  
                  Carga un paquete que se almacena en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], en `msdb` base de datos. Los paquetes almacenados en el `msdb` base de datos, se implementan utilizando el modelo de implementación de paquetes. Para ejecutar paquetes que se implementan en el [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] servidor mediante el modelo de implementación de proyectos, use el `/ISServer` opción. Para obtener más información acerca de los modelos de implementación de paquete y proyecto, vea [implementación de proyectos y paquetes](deploy-integration-services-ssis-projects-and-packages.md).  
  
     El *package_path* argumento especifica el nombre del paquete que se recuperará. Si las carpetas se incluyen en la ruta, finalizan con barras diagonales inversas ("\\"). El *package_path* valor puede estar entre comillas. Si el nombre de archivo o ruta de acceso especificada en el *package_path* argumento contiene un espacio, debe escribir entre comillas el *package_path* argumento.  
  
     Puede usar el **/User**, **/Password**, y `/Server` opciones junto con el `/SQL` opción.  
  
     Si se omite el **/User** opción, la autenticación de Windows se usa para tener acceso al paquete. Si usas el **/User** opción, el **/User** está asociado el nombre de inicio de sesión especificado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación.  
  
     El **/Password** opción solo se usa junto con el **/User** opción. Si usas el **/Password** opción, el paquete se obtiene acceso con la información de nombre y la contraseña de usuario especificada. Si se omite el **/Password** se usa la opción, una contraseña en blanco.  
  
    > [!IMPORTANT]  
    >  [!INCLUDE[ssNoteWinAuthentication](../../../includes/ssnotewinauthentication-md.md)]  
  
     Si el `/Server` opción se omite, la instancia local predeterminada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se da por hecho.  
  
     El `/SQL` opción no se puede usar junto con el `/DTS` o `/File` opción. Si se especifican varias opciones, `dtexec` se produce un error.  
  
-   **/Su [m]**: Opcional. Muestra un contador incremental que contiene el número de filas que se recibirá el siguiente componente.  
  
-   **/U[ser]** _user_name_:  
                  Opcional. Permite la recuperación de un paquete que está protegido por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación. Esta opción se usa solo cuando el `/SQL` se especifica la opción. El *user_name* valor puede estar entre comillas.  
  
    > [!IMPORTANT]  
    >  [!INCLUDE[ssNoteWinAuthentication](../../../includes/ssnotewinauthentication-md.md)]  
  
-   **/Va[lidate]**:  
                  Opcional. Detiene la ejecución del paquete después de la fase de validación sin ejecutar realmente el paquete. Durante la validación, el uso de la **/WarnAsError** opción causas `dtexec` trate una advertencia como un error; por lo tanto, el paquete da error si se produce una advertencia durante la validación.  
  
-   **/VerifyB [uild]** _principales_[*; minor*[*; compilación*]]: Opcional. Comprueba el número de compilación de un paquete con los números de compilación que se especificaron durante la fase de comprobación en el *principales*, *menores*, y *compilar* argumentos. Si se produce un error de coincidencia, no se ejecutará el paquete.  
  
     Los valores son enteros largos. El argumento puede tener uno de tres formas, con un valor para *principales* siempre obligatorio:  
  
    -   *major*  
  
    -   *major*;*minor*  
  
    -   *major*; *minor*; *build*  
  
-   **/VerifyP[ackageID]** _packageID_:  
                  Opcional. Comprueba el GUID del paquete que se ejecutará al compararlo con el valor especificado en el *idDePaquete* argumento.  
  
-   **/VerifyS[igned]**:  
                  Opcional. Hace que [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para comprobar la firma digital del paquete. Si el paquete no está firmado o la firma no es válida, se produce un error en el paquete. Para obtener más información, consulte [identificar el origen de paquetes con firmas digitales](../security/identify-the-source-of-packages-with-digital-signatures.md).  
  
    > [!IMPORTANT]  
    >  Cuando se configura para comprobar la firma del paquete, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] solo comprueba si la firma digital está presente, es válida y procede de un origen de confianza. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no comprueba si se ha cambiado el paquete.  
  
    > [!NOTE]  
    >  El elemento opcional **BlockedSignatureStates** valor del registro puede especificar una configuración más restrictivo que la opción de firma digital establecida en [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] o en el `dtexec` línea de comandos. En esta situación, la configuración del registro más restrictiva invalida los demás valores.  
  
-   **/VerifyV[ersionID]** _versionID_: Opcional. Comprueba la versión de GUID de un paquete que se ejecutará al compararlo con el valor especificado en el *version_id* argumento durante la fase de validación del paquete.  
  
-   **/Vlog** _[especificaciónDeArchivo]_: Opcional. Escribe todos los eventos de paquetes de Integration Services en los proveedores de registro que estaban habilitados cuando se diseñó el paquete. Para hacer que Integration Services habilite un proveedor de registro para archivos de texto y escribir los eventos del registro en un archivo de texto especificado, incluya una ruta de acceso y un nombre como el *Filespec* parámetro.  
  
     Si no incluye el *Filespec* parámetro, Integration Services no habilitará un proveedor de registro para archivos de texto. Integration Services solo escribirá eventos de registro para los proveedores de registro que estaban habilitados cuando se diseñó el paquete.  
  
-   **/W[arnAsError]**:  
                  Opcional. Hace que el paquete considere una advertencia como un error; por lo tanto, el paquete se producirá un error si se produce una advertencia durante la validación. Si se produce ninguna advertencia durante la validación y el **/validar** opción no se especifica, se ejecuta el paquete.  
  
-   **/X86**: Opcional. Hace que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente para ejecutar el paquete en modo de 32 bits en un equipo de 64 bits. Esta opción se establece [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente cuando se cumplen las condiciones siguientes:  
  
    -   El tipo de paso de trabajo es **paquete SQL Server Integration Services**.  
  
    -   El **Use 32 bits en tiempo de ejecución** opción el **opciones de ejecución** pestaña de la **nuevo paso de trabajo** está seleccionado el cuadro de diálogo.  
  
     También puede establecer esta opción para un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] paso de trabajo del agente mediante el uso de procedimientos almacenados o SQL Server Management Objects (SMO) para crear mediante programación del trabajo.  
  
     Esta opción solo se usa por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente. Esta opción se omite si se ejecuta el `dtexec` utilidad en el símbolo del sistema.  
  
##  <a name="remark"></a> Comentarios  
 La manera en que se ejecuta el paquete puede influir en el orden en que se especifican opciones de comando:  
  
-   Las opciones se procesan en el orden en que se encuentran en la línea de comandos. Archivos de comandos se leen de medida que se encuentran en la línea de comandos. Los comandos en el archivo de comandos también se procesan en el orden en que se encuentran.  
  
-   Si la misma opción, parámetro o variable aparece en la misma instrucción de línea de comandos más de una vez, la última instancia de la opción tiene prioridad.  
  
-   **/Set** y **/configFile** las opciones se procesan en el orden en que se encuentran.  
  
##  <a name="example"></a> Ejemplos  
 Los ejemplos siguientes muestran cómo usar el `dtexec` utilidad de línea de comandos para configurar y ejecutar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] paquetes.  
  
 **Paquetes en ejecución**  
  
 Para ejecutar un [!INCLUDE[ssIS](../../includes/ssis-md.md)] paquete guardado en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante la autenticación de Windows, use el código siguiente:  
  
```  
dtexec /sq pkgOne /ser productionServer  
```  
  
 Para ejecutar un [!INCLUDE[ssIS](../../includes/ssis-md.md)] paquete se guarda en la carpeta de sistema de archivos en el Store del paquete de SSIS, utilice el siguiente código:  
  
```  
dtexec /dts "\File System\MyPackage"  
```  
  
 Para validar un paquete que usa la autenticación de Windows y se guarda en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sin ejecutar el paquete, use el código siguiente:  
  
```  
dtexec /sq pkgOne /ser productionServer /va  
```  
  
 Para ejecutar un [!INCLUDE[ssIS](../../includes/ssis-md.md)] paquete que se guarda en el sistema de archivos, use el código siguiente:  
  
```  
dtexec /f "c:\pkgOne.dtsx"   
```  
  
 Para ejecutar un [!INCLUDE[ssIS](../../includes/ssis-md.md)] paquete que se guarda en el sistema de archivos y especifica las opciones de registro, use el código siguiente:  
  
```  
dtexec /f "c:\pkgOne.dtsx" /l "DTS.LogProviderTextFile;c:\log.txt"  
```  
  
 Para ejecutar un paquete que usa la autenticación de Windows y se guarda en la instancia local predeterminada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]y comprobar la versión antes de ejecutarlo, use el código siguiente:  
  
```  
dtexec /sq pkgOne /verifyv {c200e360-38c5-11c5-11ce-ae62-08002b2b79ef}  
```  
  
 Para ejecutar un [!INCLUDE[ssIS](../../includes/ssis-md.md)] paquete que se guarda en el sistema de archivos y configurado externamente, use el código siguiente:  
  
```  
dtexec /f "c:\pkgOne.dtsx" /conf "c:\pkgOneConfig.cfg"  
```  
  
> [!NOTE]  
>  El *package_path* o *filespec* argumentos de la /SQL opciones de, /DTS o /FILE deben incluirse entre comillas si el nombre de archivo o ruta de acceso contiene un espacio. Si el argumento no está entre comillas, el argumento no puede contener espacios en blanco.  
  
 **Opción de registro**  
  
 Si hay tres tipos de entrada de A, registro B y C, la siguiente **ConsoleLog** opción sin un parámetro muestra los tres tipos de registro con todos los campos:  
  
```  
/CONSOLELOG  
```  
  
 La siguiente opción muestra todos los tipos de registro, pero con solo las columnas Name y Message:  
  
```  
/CONSOLELOG NM  
```  
  
 La siguiente opción muestra todas las columnas, pero solo para la entrada de registro, escriba A:  
  
```  
/CONSOLELOG I;LogEntryTypeA  
```  
  
 La siguiente opción aparece sólo registro entrada tipo A, con las columnas Name y Message:  
  
```  
/CONSOLELOG NM;I;LogEntryTypeA  
```  
  
 La siguiente opción muestra las entradas del registro para los tipos de entrada de registro A y B:  
  
```  
/CONSOLELOG I;LogEntryTypeA;LogEntryTypeB  
```  
  
 Puede lograr los mismos resultados utilizando varias **ConsoleLog** opciones:  
  
```  
/CONSOLELOG I;LogEntryTypeA /CONSOLELOG I;LogEntryTypeB  
```  
  
 Si el **ConsoleLog** opción se usa sin parámetros, se muestran todos los campos. La inclusión de un *list_options* parámetro hace que se muestra solo una tipo, de la entrada de registro con todos los campos:  
  
```  
/CONSOLELOG NM;I;LogEntryTypeA /CONSOLELOG  
```  
  
 A continuación muestran todas las entradas de registro, salvo que significa que es de tipo de entrada de registro, que muestra los tipos de entrada de registro B y C:  
  
```  
/CONSOLELOG E;LogEntryTypeA  
```  
  
 El ejemplo siguiente obtiene los mismos resultados utilizando varias **ConsoleLog** opciones y una única exclusión:  
  
```  
/CONSOLELOG E;LogEntryTypeA /CONSOLELOG  
/CONSOLELOG E;LogEntryTypeA /CONSOLELOG E;LogEntryTypeA  
/CONSOLELOG E;LogEntryTypeA;LogEntryTypeA  
```  
  
 El ejemplo siguiente no muestra ningún mensaje de registro, porque cuando un tipo de archivo de registro se encuentra en las listas incluidas y excluidas, se excluirán.  
  
```  
/CONSOLELOG E;LogEntryTypeA /CONSOLELOG I;LogEntryTypeA  
```  
  
 **Opción SET**  
  
 El ejemplo siguiente muestra cómo usar el **/Set** opción, que permite cambiar el valor de cualquier propiedad del paquete o una variable cuando se inicia el paquete desde la línea de comandos.  
  
```  
/SET \package\DataFlowTask.Variables[User::MyVariable].Value;newValue  
```  
  
 **Opción Project**  
  
 El ejemplo siguiente muestra cómo usar el `/Project` y `/Package` opción.  
  
```  
/Project c:\project.ispac /Package Package1.dtsx  
```  
  
 El ejemplo siguiente muestra cómo usar el `/Project` y `/Package` opciones y establecer los parámetros de paquete y proyecto.  
  
```  
/Project c:\project.ispac /Package Package1.dtsx /SET \Package.Variables[$Package::Parameter];1 /SET \Package.Variables[$Project::Parameter];1  
  
```  
  
 **Opción ISServer**  
  
 El ejemplo siguiente muestra cómo usar el `/ISServer` opción.  
  
```  
dtexec /isserver "\SSISDB\MyFolder\MyProject\MyPackage.dtsx" /server "."  
```  
  
 El ejemplo siguiente muestra cómo usar el `/ISServer` opción y establecer la conexión y proyecto parámetros del administrador.  
  
```  
/Server localhost /ISServer "\SSISDB\MyFolder\Integration Services Project1\Package.dtsx" /Par "$Project::ProjectParameter(Int32)";1 /Par "CM.SourceServer.InitialCatalog";SourceDB  
  
```  
  
## <a name="related-tasks"></a>Tareas relacionadas  
 [Ejecutar un paquete en SQL Server Data Tools](../run-a-package-in-sql-server-data-tools.md)  
  
## <a name="related-content"></a>Contenido relacionado  
 Entrada de blog, [códigos de salida, DTEXEC y SSIS Catalog](https://www.mattmasson.com/2012/02/exit-codes-dtexec-and-ssis-catalog/), en www.mattmasson.com.  
  
  
