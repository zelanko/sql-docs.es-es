---
title: Utilidad dtutil | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- verifying packages
- checking packages
- moving packages
- packages [Integration Services], command line options
- command prompt [Integration Services]
- SQL Server Integration Services packages, command line options
- copying packages
- existence testing [Integration Services]
- Integration Services packages, command line options
- SSIS packages, command line options
- deleting packages
- dtutil utility
- removing packages
- relocating packages
ms.assetid: 6c7975ff-acec-4e6e-82e5-a641e3a98afe
caps.latest.revision: 111
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5e565c0750db83191273c66978ae1b1816d1c1d5
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37219715"
---
# <a name="dtutil-utility"></a>dtutil, utilidad
  El **dtutil** p1ompt utilidad de símbolo se usa para administrar [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] paquetes. La utilidad puede copiar, mover, eliminar o comprobar la existencia de un paquete. Estas acciones se pueden realizar en cualquier paquete [!INCLUDE[ssIS](../includes/ssis-md.md)] almacenado en una de estas tres ubicaciones: una base de datos de [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , el almacén de paquetes [!INCLUDE[ssIS](../includes/ssis-md.md)] y el sistema de archivos. Si la utilidad tiene acceso a un paquete almacenado en **msdb**, el símbolo del sistema puede requerir un nombre de usuario y una contraseña. Si la instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] utiliza Autenticación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , el símbolo del sistema requiere un nombre de usuario y una contraseña. Si falta el nombre de usuario, **dtutil** intenta iniciar una sesión en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] con la Autenticación de Windows. El tipo de almacenamiento del paquete se identifica mediante las opciones `/SQL`, `/FILE` y `/DTS`.  
  
 La utilidad de línea de comandos **dtutil** no permite usar archivos de comandos ni redireccionamiento.  
  
 La utilidad de símbolo del sistema **dtutil** incluye las siguientes características:  
  
-   Comentarios en el símbolo del sistema, que documentan la acción del símbolo del sistema y facilitan su comprensión.  
  
-   Protección contra sobrescritura, para pedir confirmación antes de sobrescribir un paquete existente al copiar o mover paquetes.  
  
-   Ayuda de consola, para proporcionar información sobre las opciones de comando de **dtutil**.  
  
> [!NOTE]  
>  Muchas de las operaciones que dtutil realiza también se pueden llevar a cabo visualmente en [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] cuando se está conectado a una instancia de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. Para obtener más información, vea [Administración de paquetes &#40;servicio SSIS&#41;](service/package-management-ssis-service.md).  
  
 Las opciones se pueden escribir en cualquier orden. El carácter de barra vertical ("|") es el operador `OR` y se utiliza para mostrar posibles valores. Debe usar una de las opciones que están delimitadas por la `OR` canalización.  
  
 Todas las opciones deben comenzar con una barra diagonal (/) o un signo menos (-). Sin embargo, no debe incluir un espacio entre la barra diagonal o el signo menos y el texto de la opción; de lo contrario, se producirá un error en el comando.  
  
 Los argumentos deben ser cadenas que estén incluidas entre comillas o que no contengan ningún espacio en blanco.  
  
 Las comillas dobles de cadenas que están entre comillas representan comillas simples de escape.  
  
 Las opciones y los argumentos, excepto las contraseñas, no distinguen entre mayúsculas y minúsculas.  
  
 **Consideraciones sobre la instalación en equipos de 64 bits**  
  
 En un equipo de 64 bits, [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] instala una versión de 64 bits de la utilidad **dtexec** (dtexec.exe) y la utilidad **dtutil** (dtutil.exe). Para instalar las versiones de 32 bits de estas herramientas de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , debe seleccionar Herramientas cliente o [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] durante la instalación.  
  
 De forma predeterminada, si un equipo de 64 bits tiene instaladas tanto las versiones de 64 bits como las de 32 bits de una utilidad de líneas de comandos de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , ejecutará la versión de 32 bits en el símbolo del sistema. La versión de 32 bits se ejecuta porque la ruta de acceso del directorio para la versión de 32 bits aparece en la variable de entorno PATH antes que la ruta de acceso del directorio para la versión de 64 bits. (Normalmente, es la ruta de acceso del directorio de 32 bits  *\<unidad >*: \Program \Microsoft SQL Server\120\DTS\Binn archivos (x86), mientras que la ruta de acceso del directorio de 64 bits es  *\<unidad >*: \ Programa de programa\Microsoft SQL Server\120\DTS\Binn).  
  
> [!NOTE]  
>  Si usa el Agente SQL Server para ejecutar la utilidad, el Agente SQL Server usa la versión de 64 bits de la utilidad automáticamente. El Agente SQL Server usa el Registro, no la variable de entorno PATH, para buscar la aplicación ejecutable correcta para la utilidad.  
  
 Para garantizar que se ejecuta la versión de 64 bits de la utilidad en el símbolo del sistema, puede realizar una de las siguientes acciones:  
  
-   Abra una ventana de símbolo del sistema, cambie al directorio que contiene la versión de 64 bits de la utilidad *(\<unidad >*: \Program Files\Microsoft SQL Server\120\DTS\Binn), y, a continuación, ejecute la utilidad desde esa ubicación.  
  
-   En el símbolo del sistema, ejecute la utilidad escribiendo la ruta de acceso completa (*\<unidad >*: \Program Files\Microsoft SQL Server\120\DTS\Binn) a la versión de 64 bits de la utilidad.  
  
-   Cambie de forma permanente el orden de las rutas de acceso en la variable de entorno PATH colocando la ruta de acceso de 64 bits (*\<unidad >*: \Program Files\Microsoft SQL Server\120\DTS\Binn) antes de la ruta de acceso de 32 bits ( *\<unidad >*: \ \Microsoft SQL Server\120\DTS\Binn (x86) los archivos de programa) en la variable.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
dtutil /option [value] [/option [value]]...  
```  
  
#### <a name="parameters"></a>Parámetros  
  
|Opción|Descripción|  
|------------|-----------------|  
|/?|Muestra las opciones del símbolo del sistema.|  
|/C[opy] *location;destinationPathandPackageName*|Especifica una acción para copiar en un paquete [!INCLUDE[ssIS](../includes/ssis-md.md)] . El uso de este parámetro requiere que especifique primero la ubicación del paquete con la opción **/FI**, **/SQ**o **/DT** . A continuación, deberá especificar la ubicación de destino y el nombre del paquete de destino. El argumento *destinationPathandPackageName* especifica en dónde se copia el paquete [!INCLUDE[ssIS](../includes/ssis-md.md)] . Si el destino *ubicación* es `SQL`, *DestUser*, *DestPassword* y *DestServer* argumentos deben ser se especificó en el comando.<br /><br /> Cuando el `Copy` acción encuentra un paquete existente en el destino, **dtutil** pide al usuario que confirme la eliminación del paquete. El `Y` respuesta sobrescribe el paquete y el `N` respuesta finaliza el programa. Cuando el comando incluye el argumento *Quiet* , no aparece ningún mensaje y los paquetes existentes se sobrescriben.|  
|/Dec[rypt] *contraseña*|(Opcional). Establece la contraseña de descifrado que se utiliza cuando se carga un paquete con cifrado de contraseña.|  
|/Del[ete]|Elimina el paquete especificado por la opción *SQL*, *DTS* o *FILE* . Si **dtutil** no puede eliminar el paquete, el programa finaliza.|  
|/DestP[assword] *contraseña*|Especifica la contraseña utilizada con la opción de SQL para conectar con una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] de destino mediante autenticación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Se genera un error si se especifica *DESTPASSWORD* en una línea de comandos que no incluye la opción *DTSUSER* .<br /><br /> Nota: [!INCLUDE[ssNoteWinAuthentication](../includes/ssnotewinauthentication-md.md)].|  
|/DestS[erver] *instancia_servidor*|Especifica el nombre de servidor que se utiliza con cualquier acción que haga que un destino se guarde en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Se usa para identificar un servidor que no es local o que no es el predeterminado cuando se guarda un paquete [!INCLUDE[ssIS](../includes/ssis-md.md)] . Es un error especificar *DESTSERVER* en una línea de comandos que no tiene una acción asociada con [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Las acciones tales como las opciones *SIGN SQL*, *COPY SQL*o *MOVE SQL* serían comandos adecuados para combinar con esta opción.<br /><br /> Un nombre de instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] se puede especificar agregando al nombre del servidor una barra diagonal inversa y el nombre de la instancia.|  
|/DestU[ser] *nombreDeUsuario*|Especifica el nombre de usuario usado con las opciones *SIGN SQL*, *COPY SQL*y *MOVE SQL* para conectar con una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que usa autenticación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Es un error especificar *DESTUSER* en una línea de comandos que no incluye la opción *SIGN SQL*, *COPY SQL*o *MOVE SQL* .|  
|/Dump *Id. del proceso*|(Opcional) Hace que el proceso especificado, la utilidad **dtexec** o el proceso **dtsDebugHost.exe** se ponga en pausa y cree los archivos de volcado de depuración, .mdmp y .tmp.<br /><br /> Nota: Para usar la opción **/Dump**, debe tener asignado el derecho de usuario Depurar programas (SeDebugPrivilege).<br /><br /> Para buscar el *process ID* del proceso que desea poner en pausa, utilice el Administrador de tareas de Windows.<br /><br /> De forma predeterminada, [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] almacena los archivos de volcado de depuración en la carpeta  *\<unidad >*: \Program Files\Microsoft SQL Server\120\Shared\ErrorDumps.<br /><br /> Para obtener más información sobre la utilidad **dtexec** y el proceso **dtsDebugHost.exe** , vea [dtexec Utility](packages/dtexec-utility.md) y [Building, Deploying, and Debugging Custom Objects](extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md).<br /><br /> Para obtener más información sobre los archivos de volcado de depuración, vea [Generating Dump Files for Package Execution](troubleshooting/generating-dump-files-for-package-execution.md).<br /><br /> Nota: Los archivos de volcado de depuración pueden contener información confidencial. Utilice una lista de control de acceso (ACL) para restringir el acceso a los archivos, o cópielos en una carpeta con acceso restringido.|  
|/DT[S] *filespec*|Especifica que el paquete de [!INCLUDE[ssIS](../includes/ssis-md.md)] sobre el que se trabajará está situado en el almacén de paquetes [!INCLUDE[ssIS](../includes/ssis-md.md)] . El argumento *filespec* debe incluir la ruta de acceso de la carpeta, a partir de la raíz del almacén de paquetes [!INCLUDE[ssIS](../includes/ssis-md.md)] . De forma predeterminada, los nombres de las carpetas raíz en el archivo de configuración son "MSDB" y "File System". Las rutas de acceso que contienen un espacio se deben delimitar utilizando comillas dobles.<br /><br /> Si se especifica la opción DT[S] en la misma línea de comandos que cualquiera de las siguientes opciones, se devuelve DTEXEC_DTEXECERROR:<br /><br /> `FILE`<br /><br /> `SQL`<br /><br /> `SOURCEUSER`<br /><br /> `SOURCEPASSWORD`<br /><br /> `SOURCESERVER`|  
|/En[crypt] *{SQL &#124; FILE}; Path;ProtectionLevel[;password]*|(Opcional). Cifra el paquete cargado con la contraseña y el nivel de protección especificado y lo guarda en la ubicación especificada en *Path*. El *ProtectionLevel* determina si se requiere una contraseña:<br />*SQL* : la ruta es el nombre del paquete de destino.<br />*FILE* : la ruta es la ruta de acceso completa y el nombre de archivo del paquete.<br />*DTS* : esta opción no se admite actualmente.<br /><br /> Opciones de*ProtectionLevel* :<br />Nivel 0: elimina la información confidencial.<br />Nivel 1: la información confidencial se cifra mediante credenciales de usuario locales.<br />Nivel 2: la información confidencial se cifra mediante la contraseña requerida.<br />Nivel 3: el paquete se cifra mediante la contraseña requerida.<br />Nivel 4: el paquete se cifra mediante credenciales de usuario locales.<br />Nivel 5: El paquete utiliza el cifrado de almacenamiento de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .|  
|/Ex[ists]|(Opcional). Se utiliza para determinar si existe un paquete. **dtutil** intenta localizar el paquete especificado por las opciones *SQL*, *DTS* o *FILE* . Si **dtutil** no puede localizar el paquete especificado, se devuelve DTEXEC_DTEXECERROR.|  
|/FC[reate] {*SQL* &#124; *DTS*};*ParentFolderPath;NewFolderName*|(Opcional). Crea una nueva carpeta que tiene el nombre especificado en *NewFolderName*. La ubicación de la nueva carpeta viene indicada por *ParentFolderPath*.|  
|/FDe[lete] {*SQL* &#124; *DTS*}[;*ParentFolderPath;FolderName]*|(Opcional). Elimina de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] o [!INCLUDE[ssIS](../includes/ssis-md.md)] la carpeta especificada por el nombre en *FolderName*. La ubicación de la carpeta que se va a eliminar viene indicada por *ParentFolderPath*.|  
|/FDi[rectory] {*SQL* &#124; *DTS*};*FolderPath[;S]*|(Opcional). Muestra el contenido, tanto carpetas como paquetes, en una carpeta de [!INCLUDE[ssIS](../includes/ssis-md.md)] o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. El parámetro *FolderPath* opcional especifica la carpeta cuyo contenido desea ver. El parámetro *S* opcional especifica si desea ver un listado del contenido de las subcarpetas para la carpeta especificada en *FolderPath*.|  
|/FE[xists ] {*SQL* &#124; *DTS*};*FolderPath*|(Opcional). Comprueba si la carpeta especificada existe en [!INCLUDE[ssIS](../includes/ssis-md.md)] o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. El parámetro *FolderPath* es la ruta de acceso y el nombre de la carpeta que se va a comprobar.|  
|/Fi[le] *filespec*|Esta opción especifica que el paquete [!INCLUDE[ssIS](../includes/ssis-md.md)] sobre el que se trabajará está ubicado en el sistema de archivos. El valor *filespec* se puede proporcionar como ruta UNC (Convención de nomenclatura universal) o ruta local.<br /><br /> Si se especifica la opción *File* en la misma línea de comandos que cualquiera de las siguientes opciones, se devuelve DTEXEC_DTEXECERROR:<br /><br /> DTS<br /><br /> SQL<br /><br /> SOURCEUSER<br /><br /> SOURCEPASSWORD<br /><br /> SOURCESERVER|  
|/FR[ename] {*SQL* &#124; *DTS*} [;*ParentFolderPath; OldFolderName;NewFolderName]*|(Opcional). Cambia el nombre de una carpeta de [!INCLUDE[ssIS](../includes/ssis-md.md)] o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. *ParentFolderPath* es la ubicación de la carpeta cuyo nombre se desea cambiar. *OldFolderName* es el nombre actual de la carpeta y *NewFolderName* es el nuevo nombre que se dará a la carpeta.|  
|/H[elp] *opción*|Muestra una completa ayuda que enumera las opciones de **dtutil** y describe su uso. El argumento de opción es opcional. Si se incluye el argumento, el texto de la ayuda incluye información detallada acerca de la opción especificada. El siguiente ejemplo muestra la ayuda para todas las opciones:<br /><br /> `dtutil /H`<br /><br /> Los siguientes dos ejemplos muestran cómo usar la opción */H* para mostrar ayuda ampliada para una opción específica, la opción */Q [uiet]* , en este ejemplo:<br /><br /> `dtutil /Help Quiet`<br /><br /> `dtutil /H Q`|  
|/I[DRegenerate]|Especifica un nuevo GUID para el paquete y actualiza la propiedad ID del paquete. Cuando se copia un paquete, el identificador del paquete sigue siendo el mismo y, por lo tanto, los archivos de registro contienen el mismo GUID para ambos paquetes. Esta acción crea un nuevo GUID para el paquete que se acaba de copiar para distinguirlo del original.|  
|/M[ove] {*SQL* &#124; *File* &#124; *DTS*}; *rutaYNombre*|Especifica una acción para mover en un paquete [!INCLUDE[ssIS](../includes/ssis-md.md)] . Para usar este parámetro, especifique primero la ubicación del paquete con la opción **/FI**, **/SQ**o **/DT** . A continuación, especifique la acción **Move** . Esta acción requiere dos argumentos, separados por un punto y coma:<br /><br /> El argumento de destino puede especificar *SQL*, *FILE*o *DTS*. Un destino *SQL* puede incluir las opciones *DESTUSER*, *DESTPASSWORD*y *DESTSERVER* .<br /><br /> El argumento *rutaYNombre* especifica la ubicación del paquete: *SQL* usa la ruta de acceso y el nombre del paquete, *FILE* usa una ruta de acceso local o UNC y *DTS* usa una ubicación relativa con respecto a la raíz del almacén de paquetes [!INCLUDE[ssIS](../includes/ssis-md.md)] . Cuando el destino es *FILE* o *DTS*, el argumento de la ruta no incluye el nombre del archivo. En su lugar, utiliza el nombre del paquete en la ubicación especificada como nombre de archivo.<br /><br /> <br /><br /> Cuando el `MOVE` acción encuentra un paquete existente en el destino, **dtutil** le pide que confirme que desea sobrescribir el paquete. El `Y` respuesta sobrescribe el paquete y el `N` respuesta finaliza el programa. Cuando el comando incluye la opción *QUIET* , no aparece ningún mensaje y los paquetes existentes se sobrescriben.|  
|/Q[uiet]|Detiene los mensajes de confirmación que pueden aparecer cuando se ejecuta un comando que incluye la opción `COPY`, `MOVE` o `SIGN`. Esos mensajes aparecen si ya existe en el equipo de destino un paquete con el mismo nombre que el paquete especificado o si el paquete especificado ya está firmado.|  
|/R[emark] *texto*|Agrega un comentario a la línea de comandos. El argumento de comentario es opcional. Si el comentario de texto incluye espacios, el texto debe ir entre comillas. Puede incluir varias opciones REM en una línea de comandos.|  
|/Si[gn] {*SQL* &#124; *File* &#124; *DTS*}; *path*; *hash*|Firma un paquete [!INCLUDE[ssIS](../includes/ssis-md.md)] . Esta acción utiliza tres argumentos obligatorios, que están separados por punto y coma:<br /><br /> El argumento de destino puede especificar *SQL*, *FILE*o *DTS*. Un destino SQL puede incluir las opciones *DESTUSER*, *DESTPASSWORD* y *DESTSERVER* .<br /><br /> El argumento de ruta especifica la ubicación del paquete en el que se realizará la acción.<br /><br /> El argumento hash especifica un identificador de certificado expresado como una cadena hexadecimal de longitud variable.<br /><br /> <br /><br /> **\*\* Importante \*\*** Cuando se configura para comprobar la firma del paquete, [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] solamente comprueba si la firma digital está presente, es válida y procede de un origen de confianza. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] no comprueba si se ha cambiado el paquete.<br /><br /> Para más información, vea [Identificar el origen de paquetes con firmas digitales](security/identify-the-source-of-packages-with-digital-signatures.md).|  
|/SourceP[assword] *contraseña*|Especifica la contraseña que se utiliza con las opciones *SQL* y *SOURCEUSER* para habilitar la recuperación de un paquete [!INCLUDE[ssIS](../includes/ssis-md.md)] que está almacenado en una base de datos en una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que utiliza autenticación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Es un error especificar *SOURCEPASSWORD* en una línea de comandos que no incluya el `SOURCEUSER` opción.<br /><br /> Nota: [!INCLUDE[ssNoteWinAuthentication](../includes/ssnotewinauthentication-md.md)]|  
|/SourceS[erver] *instancia_servidor*|Especifica el nombre de servidor que se utiliza con la opción `SQL` para habilitar la recuperación de un paquete [!INCLUDE[ssIS](../includes/ssis-md.md)] que está almacenado en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Es un error especificar *SOURCESERVER* en una línea de comandos que no incluye la opción *SIGN SQL*, *COPY* *SQL*o *MOVE* *SQL* .<br /><br /> Un nombre de instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] se puede especificar agregando al nombre del servidor una barra diagonal inversa y el nombre de la instancia.|  
|/SourceU[ser] *nombreDeUsuario*|Especifica el nombre de usuario utilizado con las opciones *SOURCESERVER* para habilitar la recuperación de un paquete [!INCLUDE[ssIS](../includes/ssis-md.md)] almacenado en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] mediante autenticación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Es un error especificar *SOURCEUSER* en una línea de comandos que no incluye la opción *SIGN SQL*, *COPY SQL*o *MOVE SQL* .<br /><br /> Nota: [!INCLUDE[ssNoteWinAuthentication](../includes/ssnotewinauthentication-md.md)]|  
|/SQ[L] *ruta_paquete*|Especifica la ubicación de un paquete [!INCLUDE[ssIS](../includes/ssis-md.md)] . Esta opción indica que el paquete está almacenado en la base de datos **msdb** . El argumento *ruta_paquete* especifica la ruta y el nombre del paquete [!INCLUDE[ssIS](../includes/ssis-md.md)] . Los nombres de carpetas terminan con barras diagonales inversas.  Si se especifica la opción *SQL* en la misma línea de comandos que cualquiera de las siguientes opciones, se devuelve DTEXEC_DTEXECERROR:<br /><br /> *DTS*<br /><br /> *FILE*<br /><br /> *SQL*. La opción *SQL* puede estar acompañada por ninguna o una instancia de las siguientes opciones: <br />*SOURCEUSER*<br />*SOURCEPASSWORD*<br />*SOURCESERVER*<br /><br /> Si *SOURCEUSERNAME* no está incluido, se utiliza la autenticación de Windows para tener acceso al paquete. Se permite*SOURCEPASSWORD* solo si *SOURCEUSER* está presente. Si no se incluye *SOURCEPASSWORD* , se utiliza una contraseña en blanco.<br /><br /> **\*\* Importante \*\*** [!INCLUDE[ssNoteStrongPass](../includes/ssnotestrongpass-md.md)]|  
  
## <a name="dtutil-exit-codes"></a>Códigos de salida de dtutil  
 **dtutil** establece un código de salida que le avisa cuando se detectan errores de sintaxis, se usan argumentos incorrectos o se especifican combinaciones no válidas de opciones. En caso contrario, la utilidad presenta el mensaje "La operación se ha realizado correctamente". En la tabla siguiente se muestran los valores que la utilidad **dtutil** puede establecer al salir.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|0|La utilidad se ha ejecutado correctamente.|  
|1|Error de la utilidad.|  
|4|La utilidad no puede localizar el paquete solicitado.|  
|5|La utilidad no puede cargar el paquete solicitado.|  
|6|La utilidad no puede resolver la línea de comandos porque contiene errores sintácticos o semánticos.|  
  
## <a name="remarks"></a>Notas  
 No puede usar archivos de comandos o redireccionamiento con **dtutil**.  
  
 El orden de las opciones de la línea de comandos no es significativo.  
  
## <a name="examples"></a>Ejemplos  
 Los siguientes ejemplos detallan escenarios típicos de uso de la línea de comandos.  
  
### <a name="copy-examples"></a>Ejemplos de copia  
 Para copiar un paquete que está almacenado en la base de datos **msdb** de una instancia local de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] mediante la Autenticación de Windows en el Almacén de paquetes de SSIS, use la siguiente sintaxis:  
  
```  
dtutil /SQL srcPackage /COPY DTS;destFolder\destPackage   
```  
  
 Para copiar un paquete desde una ubicación del sistema de archivos a otra ubicación y asignar a la copia un nombre diferente, utilice la siguiente sintaxis:  
  
```  
dtutil /FILE c:\myPackages\mypackage.dtsx /COPY FILE;c:\myTestPackages\mynewpackage.dtsx  
```  
  
 Para copiar un paquete del sistema de archivos local en una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] hospedada en otro equipo, utilice la siguiente sintaxis:  
  
```  
dtutil /FILE c:\sourcepkg.dtsx /DestServer <servername> /COPY SQL;destpkgname  
```  
  
 Como no se han usado las opciones */DestU[ser]* y */DestP[assword]* , se asume la autenticación de Windows.  
  
 Para crear un nuevo Id. para un paquete después de copiarlo, utilice la siguiente sintaxis:  
  
```  
dtutil /I /FILE copiedpkg.dtsx   
```  
  
 Para crear un nuevo Id. para todos los paquetes de una carpeta específica, utilice la siguiente sintaxis:  
  
```  
for %%f in (C:\test\SSISPackages\*.dtsx) do dtutil.exe /I /FILE %%f  
```  
  
 Use un solo signo de porcentaje (%) al escribir el comando en el símbolo del sistema. Use un signo de porcentaje doble (%) si se utiliza el comando en un archivo por lotes.  
  
### <a name="delete-examples"></a>Ejemplos de eliminación  
 Para eliminar un paquete que está almacenado en la base de datos **msdb** en una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que usa la Autenticación de Windows, use la siguiente sintaxis:  
  
```  
dtutil /SQL delPackage /DELETE  
```  
  
 Para eliminar un paquete que está almacenado en la base de datos **msdb** en una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que usa la Autenticación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , use la siguiente sintaxis:  
  
```  
dtutil /SQL delPackage /SOURCEUSER srcUserName /SOURCEPASSWORD #8nGs*w7F /DELETE  
```  
  
> [!NOTE]  
>  Para eliminar un paquete desde un servidor con nombre, incluya el `SOURCESERVER` opción y su argumento. Solo puede especificar un servidor utilizando la opción *SQL* .  
  
 Para eliminar un paquete que está almacenado en el Almacén de paquetes SSIS, utilice la siguiente sintaxis:  
  
```  
dtutil /DTS delPackage.dtsx /DELETE  
```  
  
 Para eliminar un paquete que está almacenado en el sistema de archivos, utilice la siguiente sintaxis:  
  
```  
dtutil /FILE c:\delPackage.dtsx /DELETE  
```  
  
### <a name="exists-examples"></a>Ejemplos de existencia  
 Para determinar si un paquete existe en la base de datos **msdb** de una instancia local de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que usa la Autenticación de Windows, use la siguiente sintaxis:  
  
```  
dtutil /SQL srcPackage /EXISTS  
```  
  
 Para determinar si un paquete existe en la base de datos **msdb** de una instancia local de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que usa la Autenticación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , use la siguiente sintaxis:  
  
```  
dtutil SQL srcPackage /SOURCEUSER srcUserName /SOURCEPASSWORD *hY$d56b /EXISTS  
```  
  
> [!NOTE]  
>  Para determinar si un paquete existe en un servidor con nombre, incluya la opción `SOURCESERVER` y su argumento. Solo puede especificar un servidor con la opción SQL.  
  
 Para determinar si un paquete existe en el Almacén de paquetes local, utilice la siguiente sintaxis:  
  
```  
dtutil /DTS srcPackage.dtsx /EXISTS  
```  
  
 Para determinar si un paquete existe en el sistema de archivos local, utilice la siguiente sintaxis:  
  
```  
dtutil /FILE c:\srcPackage.dtsx /EXISTS  
```  
  
### <a name="move-examples"></a>Ejemplos de movimiento  
 Para mover un paquete que está almacenado en el Almacén de paquetes de SSIS a la base de datos **msdb** de una instancia local de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que use la Autenticación de Windows, use la siguiente sintaxis:  
  
```  
dtutil /DTS srcPackage.dtsx /MOVE SQL;destPackage  
```  
  
 Para mover un paquete que está almacenado en la base de datos **msdb** en una instancia local de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que usa la Autenticación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para la base de datos **msdb** en otra instancia local de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que usa la Autenticación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , use la sintaxis siguiente:  
  
```  
dtutil /SQL srcPackage /SOURCEUSER srcUserName /SOURCEPASSWORD $Hj45jhd@X /MOVE SQL;destPackage /DESTUSER destUserName /DESTPASSWORD !38dsFH@v  
```  
  
> [!NOTE]  
>  Para mover un paquete de un servidor con nombre a otro, incluya las opciones `SOURCES` y `DESTS` y sus argumentos. Solo puede especificar servidores utilizando la opción *SQL* .  
  
 Para mover un paquete que está almacenado en el Almacén de paquetes SSIS, utilice la siguiente sintaxis:  
  
```  
dtutil /DTS srcPackage.dtsx /MOVE DTS;destPackage.dtsx  
```  
  
 Para mover un paquete que está almacenado en el sistema de archivos, utilice la siguiente sintaxis:  
  
```  
dtutil /FILE c:\srcPackage.dtsx /MOVE FILE;c:\destPackage.dtsx  
```  
  
### <a name="sign-examples"></a>Ejemplos de firma  
 Para firmar un paquete que está almacenado en una base de datos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en una instancia local de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que utilice la autenticación de Windows, utilice la siguiente sintaxis:  
  
```  
dtutil /FILE srcPackage.dtsx /SIGN FILE;destpkg.dtsx;1767832648918a9d989fdac9819873a91f919  
```  
  
 Para obtener información sobre el certificado, use **CertMgr**. El código hash puede verse en la utilidad **CertMgr** si se selecciona el certificado y, a continuación, se hace clic en **Ver** para ver las propiedades. La pestaña **Detalles** proporciona más información acerca del certificado. El `Thumbprint` propiedad se utiliza como el valor hash, sin los espacios.  
  
> [!NOTE]  
>  El hash utilizado en este ejemplo no es real.  
  
 Para obtener más información, vea la sección CertMgr en este artículo sobre [la firma y la comprobación de código con Authenticode](http://go.microsoft.com/fwlink/?LinkId=78100).  
  
### <a name="encrypt-examples"></a>Ejemplos de cifrado  
 El siguiente ejemplo cifra el archivo PackageToEncrypt.dtsx basado en un archivo en el archivo EncryptedPackage.dts basado en un archivo, utilizando el cifrado de todo el paquete con una contraseña. La contraseña que se utiliza para el cifrado es *EncPswd*.  
  
```  
dtutil /FILE PackageToEncrypt.dtsx /ENCRYPT file;EncryptedPackage.dtsx;3;EncPswd  
```  
  
## <a name="see-also"></a>Vea también  
 [Ejecutar un paquete en SQL Server Data Tools](../../2014/integration-services/run-a-package-in-sql-server-data-tools.md)  
  
  
