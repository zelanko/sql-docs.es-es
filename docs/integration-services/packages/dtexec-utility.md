---
title: dtexec (utilidad) | Microsoft Docs
ms.custom: ''
ms.date: 08/26/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 7b6867fa-1039-49b3-90fb-85b84678a612
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7f2e417ddefc0094fc6320deafea40251ba77372
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "76761859"
---
# <a name="dtexec-utility"></a>dtexec (utilidad)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  La utilidad del símbolo del sistema **dtexec** se usa para configurar y ejecutar paquetes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. La utilidad **dtexec** otorga acceso a todas las características de configuración y ejecución de paquetes, como parámetros, conexiones, propiedades, variables, registro e indicadores de progreso. La utilidad **dtexec** permite cargar paquetes desde estos orígenes: el servidor de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], un archivo de proyecto .ispac, una base de datos de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el almacén de paquetes [!INCLUDE[ssIS](../../includes/ssis-md.md)] y el sistema de archivos.  
  
> **NOTA:** Cuando se utiliza la versión actual de la utilidad **dtexec** para ejecutar un paquete creado en una versión previa de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], aquella actualiza temporalmente el paquete al formato de paquete actual. Sin embargo, no puede utilizar la utilidad **dtexec** para guardar el paquete actualizado. Para obtener más información sobre cómo actualizar un paquete a la versión actual de forma permanente, consulte [Upgrade Integration Services Packages](../../integration-services/install-windows/upgrade-integration-services-packages.md).  
  
 Este tema incluye las siguientes secciones:  
  
-   [Servidor y archivos de proyecto de Integration Services](#server)  
  
-   [Consideraciones sobre la instalación en equipos de 64 bits](#bit)  
  
-   [Consideraciones sobre los equipos con instalaciones en paralelo](#side)  
  
-   [Fases de ejecución](#phases)  
  
-   [Códigos de salida devueltos](#exit)  
  
-   [Reglas de sintaxis](#syntaxRules)  
  
-   [Usar dtexec desde xp_cmdshell](#cmdshell)  

-   [Usar dtexec desde Bash](#bash)
  
-   [Sintaxis](#syntax)  
  
-   [Parámetros](#parameter)  
  
-   [Comentarios:](#remark)  
  
-   [Ejemplos](#example)  
  
##  <a name="integration-services-server-and-project-file"></a><a name="server"></a> Servidor y archivos de proyecto de Integration Services  
 Al usar **dtexec** para ejecutar paquetes en el servidor de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], **dtexec** realiza llamadas a los procedimientos almacenados [catalog.create_execution &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md), [catalog.set_execution_parameter_value &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md) y [catalog.start_execution &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md) para crear una ejecución, establecer los parámetros de los valores e iniciar la ejecución. Todos los registros de ejecución se pueden ver desde el servidor en las vistas relacionadas o mediante los informes estándar disponibles en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para más información sobre los informes, vea [Informes para el servidor de Integration Services](../../integration-services/performance/monitor-running-packages-and-other-operations.md#reports).  
  
 A continuación, se muestra un ejemplo de ejecución de un paquete en el servidor de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
```  
DTExec /ISSERVER "\SSISDB\folderB\Integration Services Project17\Package.dtsx" /SERVER "." /Envreference 2 /Par "$Project::ProjectParameter(Int32)";1 /Par "Parameter(Int32)";21 /Par "CM.sqlcldb2.SSIS_repro.InitialCatalog";ssisdb /Par "$ServerOption::SYNCHRONIZED(Boolean)";True  
```  
  
 Cuando se usa **dtexec** para ejecutar un paquete desde el archivo de proyecto de .ispac, las opciones relacionadas son /Proj[ect] y /Pack[age], que se usan para especificar el nombre de la ruta de acceso del proyecto y el nombre del flujo. Cuando convierte un proyecto al modelo de implementación de proyectos mediante la ejecución del **Asistente para la conversión de proyectos de Integration Services** desde [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], el asistente genera un archivo de proyecto .ispac. Para obtener más información, consulte [Deploy Integration Services (SSIS) Projects and Packages](../../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md) (Implementación de proyectos y paquetes de Integration Services [SSIS]).  
  
 Puede usar **dtexec** con herramientas de programación de terceros para programar paquetes que se implementan en el servidor de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
##  <a name="installation-considerations-on-64-bit-computers"></a><a name="bit"></a> Consideraciones sobre la instalación en equipos de 64 bits  
 En un equipo de 64 bits, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] instala una versión de 64 bits de la utilidad **dtexec** (dtexec.exe). Si tiene que ejecutar paquetes específicos en el modo de 32 bits, tendrá que instalar la versión de 32 bits de la utilidad **dtexec** . Para instalar la versión de 32 bits de la utilidad **dtexec** , seleccione Herramientas cliente o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] durante la instalación.  
  
 De forma predeterminada, si un equipo de 64 bits tiene instaladas tanto las versiones de 64 bits como las de 32 bits de una utilidad de líneas de comandos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , ejecutará la versión de 32 bits en el símbolo del sistema. La versión de 32 bits se ejecuta porque la ruta de acceso del directorio para la versión de 32 bits aparece en la variable de entorno PATH antes que la ruta de acceso del directorio para la versión de 64 bits. (Normalmente, la ruta de acceso al directorio de 32 bits es *\<unidad>* :\Archivos de programa (x86)\Microsoft SQL Server\110\DTS\Binn, mientras que la ruta de acceso al directorio de 64 bits es *\<unidad>* :\Archivos de programa\Microsoft SQL Server\110\DTS\Binn).  
  
> **NOTA:** Si usa el Agente SQL Server para ejecutar la utilidad, el Agente SQL Server usa la versión de 64 bits de la utilidad automáticamente. El Agente SQL Server usa el Registro, no la variable de entorno PATH, para buscar la aplicación ejecutable correcta para la utilidad.  
  
 Para garantizar que se ejecuta la versión de 64 bits de la utilidad en el símbolo del sistema, puede realizar una de las siguientes acciones:  
  
-   Abra una ventana del símbolo del sistema, cambie al directorio que contiene la versión de 64 bits de la utilidad ( *\<unidad>* :\Archivos de programa\Microsoft SQL Server\110\DTS\Binn) y, después, ejecute la utilidad desde esa ubicación.  
  
-   En el símbolo del sistema, escriba la ruta de acceso completa de la versión de 64 bits ( *\<unidad>* :\Archivos de programa\Microsoft SQL Server\110\DTS\Binn) para ejecutar la utilidad.  
  
-   Para cambiar de forma permanente el orden de las rutas de acceso en la variable de entorno PATH, coloque la ruta de acceso de 64 bits ( *\<unidad>* :\Archivos de programa\Microsoft SQL Server\110\DTS\Binn) antes que la ruta de acceso de 32 bits ( *\<unidad>* :\Archivos de programa (x86)\Microsoft SQL Server\110\DTS\Binn) en la variable.  
  
##  <a name="considerations-on-computers-with-side-by-side-installations"></a><a name="side"></a> Consideraciones sobre los equipos con instalaciones en paralelo  
 Cuando [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] se instala en un equipo que tiene [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] o [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] instalado, se instalan varias versiones de la utilidad **dtexec** .  
  
 Para asegurarse de que ejecuta la versión correcta de la utilidad, escriba la ruta de acceso completa en el símbolo del sistema ( *\<unidad>:* \Archivos de programa\Microsoft SQL Server\\<versión\>\DTS\Binn) para ejecutar la utilidad.  
  
##  <a name="phases-of-execution"></a><a name="phases"></a> Fases de ejecución  
 La utilidad tiene cuatro fases por las que pasa durante su ejecución. Las fases son las siguientes:  
  
1.  Fase de origen de comandos: el símbolo del sistema lee la lista de opciones y argumentos que se han especificado. Todas las fases siguientes se omiten si se encuentra una opción **/?** o **/HELP** .  
  
2.  Fase de carga del paquete: se carga el paquete especificado por la opción **/SQL**, **/FILE** o **/DTS**.  
  
3.  Fase de configuración: las opciones se procesan en el orden que se muestra a continuación:  
  
    -   Opciones que establecen variables, propiedades y marcas de paquetes.  
  
    -   Opciones que comprueban la versión y la compilación del paquete.  
  
    -   Opciones que configuran el comportamiento de tiempo de ejecución de la utilidad, como la creación de informes.  
  
4.  Fase de ejecución y de validación: el paquete se ejecuta o se valida sin ejecutarse si se ha especificado la opción **/VALIDATE**.  
  
##  <a name="exit-codes-returned"></a><a name="exit"></a> Códigos de salida devueltos  
 **Códigos de salida devueltos por la utilidad dtexec**  
  
 Cuando se ejecuta un paquete, **dtexec** puede devolver un código de salida. El código de salida se utiliza para rellenar la variable ERRORLEVEL, cuyo valor se puede probar en instrucciones condicionales o lógica de bifurcaciones en un archivo por lotes. En la siguiente tabla se enumeran los valores que la utilidad **dtexec** puede establecer al salir.  
  
|Value|Descripción|  
|-----------|-----------------|  
|0|El paquete se ejecutó correctamente.|  
|1|Se produjo un error en el paquete.|  
|3|El usuario canceló el paquete.|  
|4|La utilidad no pudo localizar el paquete solicitado. No se pudo encontrar el paquete.|  
|5|La utilidad no pudo cargar el paquete solicitado. No se pudo cargar el paquete.|  
|6|La utilidad encontró un error interno semántico o sintáctico en la línea de comandos.|  
  
##  <a name="syntax-rules"></a><a name="syntaxRules"></a> Reglas de sintaxis  
 **Reglas de sintaxis de la utilidad**  
  
 Todas las opciones deben comenzar con una barra diagonal (/) o un signo menos (-). Las opciones que se muestran aquí empiezan con una barra diagonal (/), aunque se puede sustituir por el signo menos (-).  
  
 Si el argumento contiene un espacio, debe ir entre comillas. Si el argumento no está entre comillas, no podrá contener espacios en blanco.  
  
 Las dobles comillas dentro de cadenas entre comillas representan comillas simples de escape.  
  
 Las opciones y los argumentos, excepto las contraseñas, no distinguen entre mayúsculas y minúsculas.  
  
##  <a name="using-dtexec-from-the-xp_cmdshell"></a><a name="cmdshell"></a> Usar dtexec desde xp_cmdshell  
 **Usar dtexec desde xp_cmdshell**  
  
 Puede ejecutar dtexec desde el símbolo del sistema **xp_cmdshell** . En el siguiente ejemplo se muestra cómo ejecutar un paquete denominado UpsertData.dtsx y pasar por alto el código de retorno:  
  
```  
EXEC xp_cmdshell 'dtexec /f "C:\UpsertData.dtsx"'  
```  
  
 En el siguiente ejemplo se muestra cómo ejecutar el mismo paquete y capturar el código de retorno:  
  
```  
DECLARE @returncode int  
EXEC @returncode = xp_cmdshell 'dtexec /f "C:\UpsertData.dtsx"'  
```  
  
> **IMPORTANTE:** En [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], la opción **xp_cmdshell** se deshabilita de forma predeterminada en las instalaciones nuevas. La opción se puede habilitar se ejecuta el procedimiento almacenado del sistema **sp_configure** . Para más información, vea [xp_cmdshell (opción de configuración del servidor)](../../database-engine/configure-windows/xp-cmdshell-server-configuration-option.md).  

##  <a name="using-dtexec-from-bash"></a><a name="bash"></a> Usar dtexec desde Bash

El shell **Bash** es un shell de Linux muy conocido que también se puede usar en Windows. Puede ejecutar dtexec desde el símbolo del sistema de Bash. Tenga en cuenta que, en Bash, un punto y coma (`;`) es un operador delimitador de comandos. Esto es especialmente importante cuando se pasan valores al paquete mediante las opciones `/Conn[ection]`, `/Par[arameter]` o `/Set`, ya que usan el punto y coma para separar el nombre y el valor del elemento proporcionado. En el siguiente ejemplo se muestra cómo escapar el punto y coma y otros elementos al usar Bash y pasar valores a un paquete:

```bash
dtexec /F MyPackage.dtsx /CONN "MyConnection"\;"\"MyConnectionString\""
```

##  <a name="syntax"></a><a name="syntax"></a> Sintaxis  
  
```  
dtexec /option [value] [/option [value]]...  
```  
  
##  <a name="parameters"></a><a name="parameter"></a> Parámetros  
  
-   **/?** [*nombre_de_opción*]: (Opcional). Muestra las opciones del símbolo del sistema u ofrece ayuda para el argumento *option_name* especificado y, después, cierra la utilidad.  
  
     Si especifica un argumento de *option_name* , **dtexec** abre los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y muestra el tema sobre la utilidad dtexec.  
  
-   **/Ca[llerInfo]** : (Opcional). Especifica información adicional para una ejecución del paquete. Al ejecutar un paquete mediante el Agente SQL Server, el agente establece este argumento para indicar que la ejecución del paquete se invoca con el Agente SQL Server. Este parámetro se omite cuando se ejecuta la utilidad **dtexec** desde la línea de comandos.  
  
-   **/CheckF[ile]** _filespec_: (Opcional). Establece la propiedad **CheckpointFileName** del paquete en la ruta de acceso y el archivo especificados en *filespec*. Este archivo se utiliza cuando se reinicia el paquete. Si se especifica esta opción y no se proporciona ningún valor para el nombre de archivo, el valor de **CheckpointFileName** para el paquete se establece en una cadena vacía. Si no se especifica esta opción, los valores del paquete se conservan.  
  
-   **/CheckP[ointing]** _{on\off}_ : (Opcional). Establece un valor que determina si el paquete utiliza puntos de comprobación durante su ejecución. El valor **on** especifica que un paquete que haya devuelto un error debe volver a ejecutarse. Cuando se vuelve a ejecutar el paquete que ha devuelto el error, el motor en tiempo de ejecución utiliza el archivo de punto de comprobación para reiniciar el paquete desde el punto de error.  
  
     El valor predeterminado es on si la opción se declara sin un valor. La ejecución del paquete devolverá errores si el valor se establece en on y no se encuentra el archivo de punto de comprobación. Si no se especifica esta opción, se conserva el valor establecido en el paquete. Para obtener más información, vea [Restart Packages by Using Checkpoints](../../integration-services/packages/restart-packages-by-using-checkpoints.md).  
  
     La opción **/CheckPointing on** de dtexec equivale a establecer en True el valor de la propiedad **SaveCheckpoints** del paquete y el de la propiedad **CheckpointUsage** en Always.  
  
-   **/Com[mandFile]** _filespec_: (Opcional). Especifica las opciones de comando que se ejecutan con **dtexec**. Se abre el archivo especificado en *filespec* y se leen sus opciones hasta que se encuentra EOF en el archivo. *filespec* es un archivo de texto. El argumento *filespec* especifica el nombre y la ruta de acceso del archivo de comandos que se debe asociar a la ejecución del paquete.  
  
-   **/Conf[igFile]** _filespec_: (Opcional). Especifica un archivo de configuración del que se van a extraer los valores. Si utiliza esta opción, puede establecer una configuración en tiempo de ejecución que difiera de la configuración especificada para el paquete durante el diseño. Puede almacenar parámetros de configuración diferentes en un archivo de configuración XML y, después, cargar los parámetros con la opción **/ConfigFile** antes de la ejecución del paquete.  
  
     Puede usar la opción **/ConfigFile** para cargar configuraciones adicionales en tiempo de ejecución que no haya especificado en tiempo de diseño. Pero no se puede usar la opción **/ConfigFile** para reemplazar los valores configurados que también haya especificado en tiempo de diseño. Para entender cómo se aplican las configuraciones de paquete, vea [Package Configurations](../../integration-services/packages/package-configurations.md).  
  
-   **/Conn[ection]** _id_or_name;connection_string [[;id_or_name;connection_string]...]_ : (Opcional). Especifica que el administrador de conexiones con el nombre o el GUID especificado se encuentra en el paquete, y especifica una cadena de conexión.  
  
     Esta opción necesita que se especifiquen los dos parámetros: es necesario especificar el nombre del administrador de conexiones o el GUID en el argumento *id_or_name* , así como especificar una cadena de conexión válida en el argumento *connection_string* . Para más información, vea [Conexiones de Integration Services &#40;SSIS&#41;](../../integration-services/connection-manager/integration-services-ssis-connections.md).  
  
     En tiempo de ejecución, puede usar la opción **/Connection** para cargar configuraciones de paquete desde una ubicación distinta de la que haya especificado en tiempo de diseño. A continuación, los valores de estas configuraciones reemplazan a los que se especificaron originalmente. Pero solo se puede usar la opción **/Connection** para las configuraciones que usen un administrador de conexiones, como las de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para más información sobre cómo se aplican las configuraciones de paquetes, vea [Configuraciones de paquetes](../../integration-services/packages/package-configurations.md) y [Compatibilidad con versiones anteriores de Integration Services](https://msdn.microsoft.com/library/611d22fa-5ac7-485e-9a40-7131e852f794).  
  
-   **/Cons[oleLog]** [[*opciones_de_visualización*];[*opciones_de_lista*;*nombre_o_guid_del_recurso*]...]: (Opcional). Muestra las entradas de registro especificadas en la consola durante la ejecución del paquete. Si se omite esta opción, no se muestran entradas de registro en la consola. Si se especifica la opción sin parámetros que limiten la visualización, se muestran todas las entradas del registro. Para limitar las entradas que se muestran en la consola, puede especificar las columnas que se mostrarán con el parámetro *displayoptions* y limitar los tipos de entrada de registro con el parámetro *list_options* .  
  
    > **NOTA:**  Al ejecutar un paquete en el servidor [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] con el parámetro **/ISSERVER**, la salida de la consola está limitada y la mayoría de las opciones de **/Cons[oleLog]** no son válidas. Todos los registros de ejecución se pueden ver desde el servidor en las vistas relacionadas o mediante los informes estándar disponibles en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para más información sobre los informes, vea [Informes para el servidor de Integration Services](../../integration-services/performance/monitor-running-packages-and-other-operations.md#reports).  
  
     Éstos son los valores de *displayoptions* :  
  
    -   N (Nombre)  
  
    -   C (Equipo)  
  
    -   O (Operador)  
  
    -   S (Nombre de origen)  
  
    -   G (GUID de origen)  
  
    -   X (GUID de ejecución)  
  
    -   M (Mensaje)  
  
    -   T (Hora de inicio y de finalización)  
  
     Los valores de *list_options* son los siguientes:  
  
    -   *I* : especifica la lista de inclusión. Solo se registran los nombres de origen o GUID que se especifican.  
  
    -   *E* : especifica la lista de exclusión. No se registran los nombres de origen o GUID que se especifican.  
  
    -   El parámetro *src_name_or_guid* especificado para la inclusión o exclusión es un nombre de evento, nombre de origen o GUID de origen.  
  
     Si usa varias opciones de **/ConsoleLog** en el mismo símbolo del sistema, estas interactúan de la siguiente manera:  
  
    -   Su orden de aparición no tiene ningún efecto.  
  
    -   Si no hay listas de inclusión presentes en la línea de comandos, las listas de exclusión se aplican a todos los tipos de entradas de registro.  
  
    -   Si hay cualquier lista de inclusión presente en la línea de comandos, las listas de exclusión se aplican sobre la unión de todas las listas de inclusión.  
  
     Para consultar varios ejemplos de la opción **/ConsoleLog** , vea la sección **Comentarios** .  
  
-   **/D[ts]** _package_path_: (Opcional). Carga un paquete desde el Almacén de paquetes SSIS. Los paquetes almacenados en el Almacén de paquetes SSIS se implementan utilizando el modelo de implementación de paquetes heredado. Para ejecutar paquetes que se implementan en el servidor de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] con el modelo de implementación de proyectos, use la opción **/ISServer** . Para obtener más información acerca de los modelos de implementación de paquetes y de proyectos, vea [Deployment of Projects and Packages](https://msdn.microsoft.com/library/hh213290.aspx).  
  
     El argumento *package_path* especifica la ruta de acceso relativa al paquete [!INCLUDE[ssIS](../../includes/ssis-md.md)] , que empieza en la raíz del Almacén de paquetes SSIS e incluye el nombre del paquete [!INCLUDE[ssIS](../../includes/ssis-md.md)] . Si la ruta de acceso o el nombre de archivo especificado en el argumento *package_path* contiene un espacio, es necesario escribir el argumento *package_path* entre comillas.  
  
     La opción **/DTS** no se puede usar con las opciones **/File** o **/SQL** . Si se especifican varias opciones, **dtexec** devuelve un error.  
  
-   **/De[crypt]**  _password_: (Opcional). Establece la contraseña de descifrado que se utiliza cuando se carga un paquete con cifrado de contraseña.  
  
-   (Opcional) Crea los archivos de volcado de depuración, .mdmp y .tmp, cuando se producen uno o varios de los eventos especificados mientras el paquete está ejecutándose. El argumento *error code* especifica el tipo de código de evento (error, advertencia o información) que desencadenará el sistema para crear los archivos de volcado de depuración. Para especificar varios códigos de evento, separe cada argumento *error code* con un signo de punto y coma (;). No incluya comillas con el argumento *error code* .  
  
     El ejemplo siguiente genera los archivos de volcado de depuración cuando se produce el error DTS_E_CANNOTACQUIRECONNECTIONFROMCONNECTIONMANAGER.  
  
    ```  
    /Dump 0xC020801C  
    ```  
  
     **/Dump** _error code_: De manera predeterminada, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] almacena los archivos de volcado de depuración en la carpeta *\<unidad>* :\Archivos de programa\Microsoft SQL Server\110\Shared\ErrorDumps.  
  
    > **NOTA:** Los archivos de volcado de depuración pueden contener información confidencial. Utilice una lista de control de acceso (ACL) para restringir el acceso a los archivos, o cópielos en una carpeta con acceso restringido. Por ejemplo, antes de enviar los archivos de depuración a los servicios de soporte técnico de Microsoft, se recomienda quitar la información importante o confidencial.  
  
     Para aplicar esta opción a todos los paquetes que ejecuta la utilidad **dtexec** , agregue un valor REG_SZ de **DumpOnCodes** a la clave del Registro HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\SSIS\Setup\DtsPath. El valor de datos de **DumpOnCodes** especifica los códigos de error que harán que el sistema cree los archivos de volcado de depuración. Varios códigos de error deben separarse mediante un punto y coma (;).  
  
     Si agrega un valor de **DumpOnCodes** a la clave del Registro y usa la opción **/Dump** , el sistema creará archivos de volcado de depuración basados en ambos valores.  
  
     Para obtener más información sobre los archivos de volcado de depuración, vea [Generating Dump Files for Package Execution](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md).  
  
-   **/DumpOnError**: (Opcional) Crea los archivos de volcado de depuración, .mdmp y .tmp, cuando se produce un error mientras el paquete se está ejecutando.  
  
     De forma predeterminada, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] almacena los archivos de volcado de depuración en la carpeta *\<unidad>* :\Archivos de programa\Microsoft SQL Server\110\Shared\ErrorDumps.  
  
    > **NOTA:** Los archivos de volcado de depuración pueden contener información confidencial. Utilice una lista de control de acceso (ACL) para restringir el acceso a los archivos, o cópielos en una carpeta con acceso restringido. Por ejemplo, antes de enviar los archivos de depuración a los servicios de soporte técnico de Microsoft, se recomienda quitar la información importante o confidencial.  
  
     Para aplicar esta opción a todos los paquetes que ejecuta la utilidad **dtexec** , agregue un valor REG_DWORD de **DumpOnError** a la clave del Registro HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\SSIS\Setup\DtsPath. El valor REG_DWORD de **DumpOnError** determina si es necesario usar la opción **/DumpOnError** con la utilidad **dtexec** :  
  
    -   Un valor de datos distinto de cero indica que el sistema creará los archivos de volcado de depuración cuando se produzca algún error, independientemente de si se usa la opción **/DumpOnError** con la utilidad **dtexec** .  
  
    -   El valor de datos cero indica que el sistema no creará los archivos de volcado de depuración, a menos que se use la opción **/DumpOnError** con la utilidad **dtexec** .  
  
     Para obtener más información sobre los archivos de volcado de depuración, vea [Generating Dump Files for Package Execution](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md).  
  
-   **/Env[Reference]** _Id. de referencia de entorno_: (Opcional). Especifica la referencia de entorno (identificador) que usa la ejecución del paquete, para un paquete que se implementa en el servidor de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Los parámetros configurados para enlazar las variables utilizarán los valores de las variables contenidas en el entorno.  
  
     Use la opción **/Env[Reference]** opción con las opciones **/ISServer** y **/Server** .  
  
     Este parámetro lo usa el Agente SQL Server.  
  --    **/F[ile]** _filespec_: (Opcional). Carga un paquete que se guarda en el sistema de archivos. Los paquetes que se guardan en el sistema de archivos se implementan utilizando el modelo de implementación de paquetes heredados. Para ejecutar paquetes que se implementan en el servidor de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] con el modelo de implementación de proyectos, use la opción **/ISServer** . Para obtener más información acerca de los modelos de implementación de paquetes y de proyectos, vea [Deployment of Projects and Packages](deploy-integration-services-ssis-projects-and-packages.md).  

  El argumento *filespec* especifica la ruta de acceso y el nombre de archivo del paquete. Puede especificar la ruta como una ruta UNC (Convención de nomenclatura universal) o como una ruta local. Si la ruta de acceso o el nombre de archivo especificado en el argumento *filespec* contiene un espacio, debe escribir el argumento *filespec* entre comillas.  
  
-   La opción **/File** no se puede usar con las opciones **/DTS** o **/SQL** . Si se especifican varias opciones, **dtexec** devuelve un error.
  
-   **/H[elp]** [*nombre_de_opción*]: (Opcional). Muestra ayuda para las opciones o para el argumento *option_name* especificado y cierra la utilidad.  
  
     Si especifica un argumento de *option_name* , **dtexec** abre los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y muestra el tema sobre la utilidad dtexec.  
  
-   **/ISServer** _packagepath_: (Opcional). Ejecuta un paquete implementado en el servidor [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . El argumento *PackagePath* especifica el nombre de archivo y la ruta de acceso completa del paquete que se ha implementado en el servidor de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Si la ruta de acceso o el nombre de archivo especificado en el argumento *PackagePath* contiene un espacio, debe escribir el argumento *PackagePath* entre comillas.  
  
     El formato del paquete es el siguiente:  
  
    ```  
    \<catalog name>\<folder name>\<project name>\package file name  
    ```  
  
     Use la opción **/Server** con la opción **/ISSERVER** . Solamente la autenticación de Windows puede ejecutar un paquete en el Servidor SSIS. Para tener acceso al paquete, use el usuario actual de Windows. Si se omite la opción /Server, se supone que se usará la instancia local predeterminada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
     La opción **/ISSERVER** no se puede usar con las opciones **/DTS**, **/SQL** o **/File** . Si se especifican varias opciones, dtexec devuelve un error.  
  
     Este parámetro lo usa el Agente SQL Server.  
  
-   **/L[ogger]** _classid_orprogid;configstring_: (Opcional). Asocia uno o más proveedores de registro con la ejecución de un paquete [!INCLUDE[ssIS](../../includes/ssis-md.md)] . El parámetro *classid_orprogid* especifica el proveedor de registro y puede especificarse como GUID de clase. *configstring* es la cadena que se utiliza para configurar el proveedor de registro.  
  
     La siguiente lista muestra los proveedores de registro disponibles:  
  
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
  
-   **/M[axConcurrent]** _concurrent_executables_: (Opcional). Especifica el número de archivos ejecutables que el paquete puede ejecutar simultáneamente. El valor especificado debe ser un valor entero no negativo ó -1. El valor -1 significa que [!INCLUDE[ssIS](../../includes/ssis-md.md)] permitirá la ejecución simultánea de un número máximo de archivos que sea igual al número total de procesadores del equipo que ejecuta el paquete, más dos.  
  
-   **/Pack[age]** _PackageName_: (Opcional). Especifica el paquete que se ejecuta. Este parámetro se utiliza principalmente al ejecutar el paquete desde [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)].  
  
-   **/P[assword]** _password_: (Opcional). Permite la recuperación de un paquete protegido por la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Esta opción se usa con la opción **/User** . Si se omite la opción **/Password** y se usa **/User** , se usará una contraseña en blanco. El valor de *password* puede entrecomillarse.  
  
    > **IMPORTANTE:** [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
-   **/Par[ameter]** [$Package:: | $Project:: | $ServerOption::] *nombre_parámetro* [(tipo_de_datos)]; *valor_literal*: (Opcional). Especifica los valores del parámetro. Se pueden especificar varias opciones de **/Parameter** . Los tipos de datos son CLR TypeCodes como cadenas. Para los parámetros que no sean de cadenas, el tipo de datos se especifica entre paréntesis seguido del nombre del parámetro.  
  
     La opción **/Parameter** solo puede se puede usar con **/ISServer** .  
  
     Utilice los prefijos $Package, $Project y $ServerOption para indicar un parámetro de paquete, un parámetro de proyecto y un parámetro de servidor, respectivamente. El tipo de parámetro predeterminado es paquete.  
  
     A continuación se muestra un ejemplo de ejecución de un paquete y se proporciona myvalue como parámetro de proyecto (myparam) y el valor entero 12 para el parámetro de paquete (anotherparam).  
  
     `Dtexec /isserver "SSISDB\MyFolder\MyProject\MyPackage.dtsx" /server "." /parameter $Project::myparam;myvalue /parameter anotherparam(int32);12`  
  
     También puede establecer propiedades del administrador de conexiones mediante parámetros. Use el prefijo CM para indicar un parámetro del administrador de conexiones.  
  
     En el ejemplo siguiente, la propiedad InitialCatalog del administrador de conexiones SourceServer se establece en `ssisdb`.  
  
    ```  
    /parameter CM.SourceServer.InitialCatalog;ssisdb  
    ```  
  
     En el ejemplo siguiente, la propiedad ServerName del administrador de conexiones SourceServer se establece en un punto (.) para indicar el servidor local.  
  
    ```  
    /parameter CM.SourceServer.ServerName;.  
    ```  
  
-   **/Proj[ect]** _ProjectFile_: (Opcional). Especifica el proyecto desde el que recuperar el paquete que se ejecuta. El argumento de *ProjectFile* especifica el nombre de archivo .ispac. Este parámetro se utiliza principalmente al ejecutar el paquete desde [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)].  
  
-   **/Rem** _comment_: (Opcional). Incluye comentarios en el símbolo del sistema o en los archivos de comandos. El argumento es opcional. El valor de *comment* es una cadena que debe incluirse entre comillas o no debe contener ningún espacio en blanco. Si no especifica ningún argumento, se inserta una línea en blanco. Los valores de*comment* se descartan durante la fase de origen de comandos.  
  
-   **/Rep[orting]** _level_ [ *;event_guid_or_name*[ *;event_guid_or_name*[...]]: (Opcional). Especifica el tipo de mensajes que se notificarán. Las opciones de informes disponibles para *level* son las siguientes:  
  
     **N** Sin informes.  
  
     **E** Se notifican los errores.  
  
     **W** Se notifican las advertencias.  
  
     **I** Se notifican los mensajes informativos.  
  
     **C** Se notifican los eventos personalizados.  
  
     **D** Se notifican los eventos de la tarea Flujo de datos.  
  
     **P** Se notifica el progreso.  
  
     **V** Informes detallados.  
  
     Los argumentos V y N se excluyen mutuamente con los otros argumentos, por lo que deben especificarse solos. Si no se especifica la opción **/Reporting** , el nivel predeterminado es **E** (errores), **W** (advertencias) y **P** (progreso).  
  
     Todos los eventos van precedidos de una marca de tiempo en el formato "AA/MM/DD HH:MM:SS" y un GUID o nombre descriptivo si está disponible.  
  
     El parámetro opcional *event_guid_or_name* es una lista de excepciones para los proveedores de registro. La excepción especifica los eventos que no se registran pero que podrían haberse registrado.  
  
     No es necesario excluir un evento si éste no se registra habitualmente de forma predeterminada.  
  
-   **/Res[tart]** {*deny | force | ifPossible*}: (Opcional). Especifica un nuevo valor para la propiedad <xref:Microsoft.SqlServer.Dts.Runtime.Package.CheckpointUsage%2A> del paquete. El significado de los parámetros es el siguiente:  
  
     *Deny* establece la propiedad <xref:Microsoft.SqlServer.Dts.Runtime.Package.CheckpointUsage%2A> en <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSCheckpointUsage.DTSCU_NEVER>.  
  
     *Force* establece la propiedad <xref:Microsoft.SqlServer.Dts.Runtime.Package.CheckpointUsage%2A> en <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSCheckpointUsage.DTSCU_ALWAYS>.  
  
     *ifPossible* establece la propiedad <xref:Microsoft.SqlServer.Dts.Runtime.Package.CheckpointUsage%2A> en <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSCheckpointUsage.DTSCU_IFEXISTS>.  
  
     Si no se especifica ningún valor, se utiliza el valor predeterminado de **force** .  
  
-   **/Set** [$Sensitive::]*ruta_de_propiedad;valor*: (Opcional). Invalida la configuración de un parámetro, variable, propiedad, contenedor, proveedor de registro, enumerador Foreach o conexión en un paquete. Cuando se usa esta opción, **/Set** cambia el argumento *propertyPath* al valor especificado. Se pueden especificar varias opciones de **/Set** .  
  
     Además de usar **/Set** con la opción **/F[ile]** , también se puede usar **/Set** con las opciones **/ISServer** o **/Project** . Si se usa **/Set** con **/Project**, **/Set** establece valores de parámetro. Si se usa **/Set** con **/ISServer**, **/Set** establece invalidaciones de propiedad. Además, al usar **/Set** con **/ISServer**, puede usar el prefijo opcional $Sensitive para indicar que la propiedad tiene que considerarse como confidencial en el servidor de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
     Puede ejecutar el Asistente para la configuración de paquetes con el objeto de determinar el valor de *propertyPath* . Las rutas de los elementos que seleccione se muestran en la página **Finalización del asistente** y se pueden copiar y pegar. Si ha utilizado el asistente exclusivamente con este fin, puede cancelarlo después de copiar las rutas de acceso.  
  
     A continuación, se muestra un ejemplo de ejecución de un paquete que se guarda en el sistema de archivos y se proporciona un nuevo valor para una variable:  
  
     `dtexec /f mypackage.dtsx /set \package.variables[myvariable].Value;myvalue`  
  
     En el siguiente ejemplo, se ejecuta un paquete desde archivo de proyecto .ispac y se establecen los parámetros de paquete y de proyecto.  
  
     `/Project c:\project.ispac /Package Package1.dtsx /SET \Package.Variables[$Package::Parameter];1 /SET \Package.Variables[$Project::Parameter];1`  
  
     Puede usar la opción **/Set** para cambiar la ubicación desde donde se cargan las configuraciones de paquete. Pero no se puede usar la opción **/Set** para invalidar un valor que se haya especificado en una configuración en tiempo de diseño. Para más información sobre cómo se aplican las configuraciones de paquetes, vea [Configuraciones de paquetes](../../integration-services/packages/package-configurations.md) y [Compatibilidad con versiones anteriores de Integration Services](https://msdn.microsoft.com/library/611d22fa-5ac7-485e-9a40-7131e852f794).  
  
-   **/Ser[ver]** _server_: (Opcional). Cuando se usa **/SQL** o **/DTS** , esta opción especifica el nombre del servidor del que se tiene que recuperar el paquete. Si se omite la opción **/Server** y se especifica **/SQL** o **/DTS** , se intentará ejecutar el paquete en un servidor local. El valor de *server_instance* se puede escribir entre comillas.  
  
     La opción **/Ser[ver]** es necesaria cuando se especifica la opción **/ISServer** .  
  
-   **/SQ[L]** _package_path_: carga un paquete que está almacenado en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], en la base de datos **msdb**. Los paquetes almacenados en la base de datos de **msdb** se implementan utilizando el modelo de implementación de paquetes. Para ejecutar paquetes que se implementan en el servidor de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] con el modelo de implementación de proyectos, use la opción **/ISServer** . Para obtener más información acerca de los modelos de implementación de paquetes y de proyectos, vea [Deployment of Projects and Packages](https://msdn.microsoft.com/library/hh213290.aspx).   
  
-   El argumento *package_path* especifica el nombre del paquete que se recuperará. Si las carpetas se incluyen en la ruta, finalizan con barras diagonales inversas ("\\"). El valor de *package_path* se puede escribir entre comillas. Si la ruta de acceso o el nombre de archivo especificado en el argumento *package_path* contiene un espacio, es necesario escribir el argumento *package_path* entre comillas.  
  
     Las opciones **/User**, **/Password**y **/Server** se pueden usar con la opción **/SQL** .  
  
     Si se omite la opción **/User** , se usará la autenticación de Windows para acceder al paquete. Si se usa la opción **/User** , el nombre de inicio de sesión de **/User** especificado se asociará con la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
     La opción **/Password** solo se usa con la opción **/User** . Si se usa la opción **/Password** , se accederá al paquete con la información de nombre de usuario y contraseña especificada. En cambio, si se omite la opción **/Password** , se usará una contraseña en blanco.  
  
    > **IMPORTANTE:** [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
-   Si se omite la opción **/Server** , se supone que se usará la instancia local predeterminada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
     La opción **/SQL** no se puede usar con las opciones **/DTS** o **/File** . Si se especifican varias opciones, **dtexec** devuelve un error.  
  
-   **/Su[m]** : (Opcional). Muestra un contador incremental que contiene el número de filas que recibirá el siguiente componente.  
  
-   **/U[ser]** _user_name_: (Opcional). Permite la recuperación de un paquete protegido por la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Esta opción solo se usa cuando se especifica **/SQL** . El valor de *user_name* se puede escribir entre comillas.  
  
    > **IMPORTANTE:**  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
-   **/Va[lidate]** : (Opcional). Detiene la ejecución del paquete después de la fase de validación sin ejecutar realmente el paquete. Durante la validación, el uso de la opción **/WarnAsError** hace que **dtexec** considere una advertencia como un error y, por lo tanto, el paquete devuelve un error cuando se produce una advertencia durante la validación.  
  
-   **/VerifyB[uild]** _major_[ *;minor*[ *;build*]]: (Opcional). Comprueba el número de compilación de un paquete con los números de compilación que se especificaron durante la fase de comprobación en los argumentos *major*, *minor*y *build* . Si se produce una discrepancia, el paquete no se ejecuta.  
  
     Los valores son enteros largos. El argumento puede tener una de las tres formas, con un valor para *major* siempre obligatorio:  
  
    -   *major*  
  
    -   *major*;*minor*  
  
    -   *major*; *minor*; *build*  
  
-   **/VerifyP[ackageID]** _packageID_: (Opcional). Comprueba el GUID del paquete que se ejecutará al compararlo con el valor especificado en el argumento *package_id* .  
  
-   **/VerifyS[igned]** : (Opcional). Hace que [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] compruebe la firma digital del paquete. Si el paquete no está firmado o la firma no es válida, se produce un error en el paquete. Para más información, vea [Identificar el origen de paquetes con firmas digitales](../../integration-services/security/identify-the-source-of-packages-with-digital-signatures.md).  
  
    > **IMPORTANTE:** Cuando se configura para comprobar la firma del paquete, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] solamente comprueba si la firma digital está presente, es válida y procede de un origen de confianza. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no comprueba si se ha cambiado el paquete.  
  
    > **NOTA:** El valor del Registro **BlockedSignatureStates** opcional puede especificar un parámetro de configuración más restrictivo que la opción de firma digital establecida en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] o en la línea de comandos de **dtexec** . En esta situación, el valor del Registro más restrictivo invalida los demás valores.  
  
-   **/VerifyV[ersionID]** _versionID_: (Opcional). Comprueba el GUID de versión de un paquete que se ejecutará al compararlo con el valor especificado en el argumento *version_id* durante la fase de validación del paquete.  
  
-   **/VLog** _[Filespec]_ : (Opcional). Escribe todos los eventos de paquete de Integration Services para los proveedores de registro que estaban habilitados cuando se diseñó el paquete. Para hacer que Integration Services habilite un proveedor de registro para los archivos de texto y escriba eventos de registro en un archivo de texto especificado, incluya una ruta de acceso y un nombre de archivo como parámetro *Filespec* .  
  
     Si no incluye el parámetro *Filespec* , Integration Services no habilitará un proveedor de registro para los archivos de texto. Integration Services solo escribirá eventos de registro para los proveedores de registro que estaban habilitados cuando se diseñó el paquete.  
  
-   **/W[arnAsError]** : (Opcional). Hace que el paquete considere una advertencia como un error y que, por consiguiente, el paquete devuelva un error si se produce una advertencia durante la validación. Si no se produce ninguna advertencia durante la validación y no se especifica la opción **/Validate** , se ejecutará el paquete.  
  
-   **/X86**: (Opcional). Hace que el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ejecute el paquete en modo de 32 bits en un equipo de 64 bits. Esta opción la establece el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuando se cumplen las condiciones:  
  
    -   El tipo de paso de trabajo es **Paquete SQL Server Integration Services**.  
  
    -   La opción **Usar motor de tiempo de ejecución de 32 bits** en la pestaña **Opciones de ejecución** del cuadro de diálogo **Nuevo paso de trabajo** está seleccionada.  
  
     También puede establecer esta opción para un paso de trabajo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizando procedimientos almacenados u Objetos de administración de SQL Server (SMO) para crear el trabajo mediante programación.  
  
     Esta opción solo la utiliza el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y se omite si se ejecuta la utilidad **dtexec** en el símbolo del sistema.  
  
##  <a name="remarks"></a><a name="remark"></a> Comentarios  
 El orden en el que se especifican las opciones de comandos puede influir en la forma en que se ejecuta el paquete:  
  
-   Las opciones se procesan en el orden en el que se encuentran en la línea de comandos. Los archivos de comandos se leen en el orden en que se encuentran en la línea de comandos. Los comandos del archivo de comandos también se procesan en el orden en que se encuentran.  
  
-   Si la misma opción, parámetro o variable aparece en la misma instrucción de línea de comandos más de una vez, tiene prioridad la última instancia de la opción.  
  
-   Las opciones **/Set** y **/ConfigFile** se procesan en el orden en el que se encuentran.  
  
##  <a name="examples"></a><a name="example"></a> Ejemplos  
 En los siguientes ejemplos se muestra cómo usar la utilidad de símbolo del sistema **dtexec** para configurar y ejecutar paquetes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 **Paquetes en ejecución**  
  
 Para ejecutar un paquete [!INCLUDE[ssIS](../../includes/ssis-md.md)] guardado en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizando la autenticación de Windows, utilice el siguiente código:  
  
```  
dtexec /sq pkgOne /ser productionServer  
```  
  
 Para ejecutar un paquete [!INCLUDE[ssIS](../../includes/ssis-md.md)] guardado en la carpeta Sistema de archivos en el almacén de paquetes SSIS, utilice el siguiente código:  
  
```  
dtexec /dts "\File System\MyPackage"  
```  
  
 Para validar un paquete que utiliza la autenticación de Windows y se guarda en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sin ejecutar el paquete, utilice el siguiente código:  
  
```  
dtexec /sq pkgOne /ser productionServer /va  
```  
  
 Para ejecutar un paquete [!INCLUDE[ssIS](../../includes/ssis-md.md)] que se guarda en el sistema de archivos, utilice el siguiente código:  
  
```  
dtexec /f "c:\pkgOne.dtsx"   
```  
  
 Para ejecutar un paquete [!INCLUDE[ssIS](../../includes/ssis-md.md)] que se guarda en el sistema de archivos y especificar opciones de registro, utilice el siguiente código:  
  
```  
dtexec /f "c:\pkgOne.dtsx" /l "DTS.LogProviderTextFile;c:\log.txt"  
```  
  
 Para ejecutar un paquete que utiliza la autenticación de Windows y se guarda en la instancia local predeterminada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], y comprobar la versión antes de que se ejecute, utilice el siguiente código:  
  
```  
dtexec /sq pkgOne /verifyv {c200e360-38c5-11c5-11ce-ae62-08002b2b79ef}  
```  
  
 Para ejecutar un paquete [!INCLUDE[ssIS](../../includes/ssis-md.md)] que se guarda en el sistema de archivos y que se ha configurado externamente, utilice el siguiente código:  
  
```  
dtexec /f "c:\pkgOne.dtsx" /conf "c:\pkgOneConfig.cfg"  
```  
  
> **NOTA:** Los argumentos *package_path* o *filespec* de las opciones /SQL, /DTS o /FILE tienen que escribirse entre comillas siempre que la ruta o el nombre del archivo contenga un espacio en blanco. Si el argumento no está entre comillas, no podrá contener espacios en blanco.  
  
 **Opción de registro**  
  
 Si hay tres tipos de entrada de registro, A, B y C, la siguiente opción **ConsoleLog** sin un parámetro muestra los tres tipos de registro con todos los campos:  
  
```  
/CONSOLELOG  
```  
  
 La siguiente opción muestra todos los tipos de registro, pero solo con las columnas Name y Message:  
  
```  
/CONSOLELOG NM  
```  
  
 La siguiente opción muestra todas las columnas, pero solo para el tipo de entrada de registro A:  
  
```  
/CONSOLELOG I;LogEntryTypeA  
```  
  
 La siguiente opción solo muestra el tipo de entrada de registro A con las columnas Name y Message:  
  
```  
/CONSOLELOG NM;I;LogEntryTypeA  
```  
  
 La siguiente opción muestra las entradas del tipo de entrada de registro A y B:  
  
```  
/CONSOLELOG I;LogEntryTypeA;LogEntryTypeB  
```  
  
 Puede lograr los mismos resultados mediante el uso de varias opciones **ConsoleLog** :  
  
```  
/CONSOLELOG I;LogEntryTypeA /CONSOLELOG I;LogEntryTypeB  
```  
  
 Si se utiliza la opción **ConsoleLog** sin parámetros, se muestran todos los campos. La inclusión de un parámetro de *list_options* hace que se muestre solo el tipo de entrada de registro A con todos los campos:  
  
```  
/CONSOLELOG NM;I;LogEntryTypeA /CONSOLELOG  
```  
  
 La siguiente opción muestra todas las entradas de registro excepto el tipo de entrada de registro A, lo que significa que se muestran los tipos de entrada de registro B y C:  
  
```  
/CONSOLELOG E;LogEntryTypeA  
```  
  
 En el siguiente ejemplo se obtienen los mismos resultados utilizando varias opciones **ConsoleLog** y una única exclusión:  
  
```  
/CONSOLELOG E;LogEntryTypeA /CONSOLELOG  
/CONSOLELOG E;LogEntryTypeA /CONSOLELOG E;LogEntryTypeA  
/CONSOLELOG E;LogEntryTypeA;LogEntryTypeA  
```  
  
 El siguiente ejemplo no muestra ningún mensaje de registro, porque cuando se encuentra un tipo de archivo de registro tanto en la lista de exclusiones como en la de inclusiones, este tipo de archivo se excluye.  
  
```  
/CONSOLELOG E;LogEntryTypeA /CONSOLELOG I;LogEntryTypeA  
```  
  
 **Opción SET**  
  
 En el ejemplo siguiente se muestra cómo usar la opción **/SET** , que permite cambiar el valor de cualquier propiedad o variable de paquete al iniciar el paquete desde la línea de comandos.  
  
```  
/SET \package\DataFlowTask.Variables[User::MyVariable].Value;newValue  
```  
  
 **Opción Project**  
  
 En el ejemplo siguiente se muestra cómo usar las opciones **/Project** y **/Package** .  
  
```  
/Project c:\project.ispac /Package Package1.dtsx  
```  
  
 En el ejemplo siguiente, se muestra cómo usar las opciones **/Project** y **/Package** , y cómo establecer los parámetros de paquete y de proyecto.  
  
```  
/Project c:\project.ispac /Package Package1.dtsx /SET \Package.Variables[$Package::Parameter];1 /SET \Package.Variables[$Project::Parameter];1  
  
```  
  
 **Opción ISServer**  
  
 En el ejemplo siguiente se muestra cómo usar la opción **/ISServer** .  
  
```  
dtexec /isserver "\SSISDB\MyFolder\MyProject\MyPackage.dtsx" /server "."  
```  
  
 En el ejemplo siguiente, se muestra cómo usar la opción **/ISServer** y cómo establecer los parámetros del administrador de conexiones y de proyecto.  
  
```  
/Server localhost /ISServer "\SSISDB\MyFolder\Integration Services Project1\Package.dtsx" /Par "$Project::ProjectParameter(Int32)";1 /Par "CM.SourceServer.InitialCatalog";SourceDB  
  
```  
  
## <a name="related-content"></a>Contenido relacionado  
 Entrada de blog [Códigos de salida, catálogo de DTEXEC y SSIS](https://www.mattmasson.com/2012/02/exit-codes-dtexec-and-ssis-catalog/), en www.mattmasson.com.  
  
  
