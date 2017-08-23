---
title: Compilar, implementar y depurar objetos personalizados | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- custom objects [Integration Services]
ms.assetid: b03685bc-5398-4c3f-901a-1219c1098fbe
caps.latest.revision: 50
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 99fdd71403b12cee8ba9f207890268cde2e1d450
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="building-deploying-and-debugging-custom-objects"></a>Generar, implementar y depurar objetos personalizados
  Después de haber escrito el código para un objeto personalizado para [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], debe compilar el ensamblado, implementarlo e integrarlo en [!INCLUDE[ssIS](../../includes/ssis-md.md)] diseñador para que esté disponible para su uso en paquetes y probarlo y depurarlo.  
  
##  <a name="top"></a>Pasos para generar, implementar y depurar un objeto personalizado para Integration Services  
 Ya ha escrito la funcionalidad personalizada para el objeto. Ahora tiene que probarlo y hacer que esté disponible para los usuarios. Los pasos son muy similares para todos los tipos de objetos personalizados que puede crear para [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 Estos son los pasos para generar, implementar y probarlo.  
  
1.  [Inicio de sesión](#signing) ensamblado que se va a generar con un nombre seguro.  
  
2.  [Crear](#building) el ensamblado.  
  
3.  [Implementar](#deploying) el ensamblado al mover o copiar a la correspondiente [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] carpeta.  
  
4.  [Instalar](#installing) el ensamblado en la caché de ensamblados global (GAC).  
  
     El objeto se agregará automáticamente al cuadro de herramientas.  
  
5.  [Solucionar problemas de](#troubleshooting) la implementación, si es necesario.  
  
6.  [Prueba](#testing) y depurar el código.  
  
 Ahora puede usar el Diseñador SSIS en SQL Server Data Tools (SSDT) para crear, mantener y ejecutar paquetes que tienen como destino versiones diferentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información sobre el efecto de esta mejora en sus extensiones personalizadas, consulte [obtener sus extensiones personalizadas de SSIS que deben admitir la compatibilidad con varias versiones de 2015 de SSDT para SQL Server 2016](https://blogs.msdn.microsoft.com/ssis/2016/04/19/getting-your-ssis-custom-extensions-to-be-supported-by-the-multi-version-support-of-ssdt-2015-for-sql-server-2016/)  
  
##  <a name="signing"></a>Firmar el ensamblado  
 Cuando se tiene pensado compartir un ensamblado, se debe instalar en la memoria caché de ensamblados global. Una vez agregado el ensamblado a la memoria caché de ensamblados global, aplicaciones como [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] pueden utilizarlo. Un requisito de la memoria caché de ensamblados global es que el ensamblado se debe firmar con un nombre seguro, que garantiza que el ensamblado es único de forma global. Un ensamblado con nombre seguro especifica un nombre completo que incluye el nombre del ensamblado, la referencia cultural, la clave pública y el número de versión. El motor en tiempo de ejecución utiliza esta información para localizar el ensamblado y distinguirlo entre otros ensamblados con el mismo nombre.  
  
 Para firmar un ensamblado con un nombre seguro, es necesario crear o tener antes un par de claves publica y privada. Este par de claves criptográficas pública y privada se usa al realizar la compilación para crear un ensamblado con nombre seguro.  
  
 Para obtener más información sobre los nombres seguros y los pasos que debe seguir para firmar un ensamblado, consulte los temas siguientes en la documentación del SDK de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]:  
  
-   Ensamblados con nombre seguro  
  
-   Crear un par de claves  
  
-   Firmar un ensamblado con un nombre seguro  
  
 Puede firmar con facilidad el ensamblado con un nombre seguro en [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] durante la generación. En el **propiedades del proyecto** cuadro de diálogo, seleccione la **firma** ficha. Seleccione la opción de **firmar el ensamblado** y, a continuación, proporcione la ruta de acceso del archivo de clave (.snk).  
  
##  <a name="building"></a>Generar el ensamblado  
 Después de iniciar el proyecto, debe generar o volver a generar el proyecto o la solución mediante el uso de los comandos disponibles en la **generar** menú de [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. La solución puede contener un proyecto independiente para una interfaz de usuario personalizada, que también se debe firmar con un nombre seguro y se puede generar al mismo tiempo.  
  
 El método más cómodo para realizar los dos pasos siguientes, desplegar el ensamblado e instalarlo en la memoria caché de ensamblados global, es crear script de estos pasos como un evento posterior a la generación en [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]. Los eventos de compilación están disponibles en la **compilar** página de propiedades del proyecto para una [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] proyecto y desde el **eventos de compilación** página de un proyecto de C#. La ruta de acceso completa es necesaria para las utilidades de símbolo del sistema como **gacutil.exe**. Son necesarias comillas alrededor de las rutas de acceso que contienen espacios en blanco y alrededor de macros como $(TargetPath) que se expanden a rutas de acceso que contienen espacios en blanco.  
  
 A continuación figura un ejemplo de una línea de comandos del evento posterior a la generación para un proveedor de registro personalizado:  
  
```  
"C:\Program Files (x86)\Microsoft SDKs\Windows\v7.0A\bin\NETFX 4.0 Tools\gacutil.exe" -u $(TargetName)  
"C:\Program Files (x86)\Microsoft SDKs\Windows\v7.0A\bin\NETFX 4.0 Tools\gacutil.exe" -i $(TargetFileName)  
copy $(TargetFileName) "C:\Program Files\Microsoft SQL Server\130\DTS\LogProviders "  
```  
  
##  <a name="deploying"></a>Implementar el ensamblado  
 El [!INCLUDE[ssIS](../../includes/ssis-md.md)] diseñador busca los objetos personalizados disponibles para su uso en paquetes enumerando los archivos se encuentran en una serie de carpetas que se crean cuando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] está instalado. Cuando el valor predeterminado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se usa la configuración de la instalación, este conjunto de carpetas se encuentra en **C:\Program Files\Microsoft SQL Server\130\DTS**. Sin embargo, si crea un programa de instalación para el objeto personalizado, se debe comprobar el valor de la **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\SSIS\Setup\DtsPath** clave del registro para comprobar la ubicación de esta carpeta.  
  
> [!NOTE]  
>  Para obtener información sobre cómo implementar los componentes personalizados que funcionen bien con la compatibilidad con varias versiones de SQL Server Data Tools, consulte [obtener sus extensiones personalizadas de SSIS que deben admitir la compatibilidad con varias versiones de 2015 de SSDT para SQL Server 2016](https://blogs.msdn.microsoft.com/ssis/2016/04/19/getting-your-ssis-custom-extensions-to-be-supported-by-the-multi-version-support-of-ssdt-2015-for-sql-server-2016/).  
  
 Puede colocar el ensamblado en la carpeta de dos maneras:  
  
-   Copiar o mover el ensamblado compilado a la carpeta adecuada después de generarlo. (Para su comodidad, puede incluir el comando de copia en un evento posterior a la generación).  
  
-   Generar el ensamblado directamente en la carpeta adecuada.  
  
 Las carpetas de implementación siguientes bajo **C:\Program Files\Microsoft SQL Server\130\DTS** se utilizan para los distintos tipos de objetos personalizados:  
  
|Objeto personalizado|Carpeta de implementación|  
|-------------------|-----------------------|  
|Tarea|Tareas|  
|Administrador de conexiones|Conexiones|  
|Proveedor de registro|LogProviders|  
|Componente de flujo de datos|PipelineComponents|  
  
> [!NOTE]  
>  Los ensamblados se copian en estas carpetas para admitir la enumeración de tareas disponibles, administradores de conexión, etc. Por consiguiente no tiene que implementar los ensamblados que contienen solo la interfaz de usuario personalizada para los objetos personalizados en estas carpetas.  
  
##  <a name="installing"></a>Instalar al ensamblado en la caché Global de ensamblados  
 Para instalar el ensamblado de tarea en la caché de ensamblados global (GAC), utilice la herramienta de línea de comandos **gacutil.exe**, o arrastre los ensamblados a los `%system%\assembly` directory. Para mayor comodidad, también puede incluir la llamada a **gacutil.exe** en un evento posterior a la compilación.  
  
 El comando siguiente instala un componente denominado *MyTask.dll* en la GAC mediante el uso de **gacutil.exe**.  
  
 `gacutil /iF MyTask.dll`  
  
 Se debe cerrar y volver a abrir el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] después de instalar una nueva versión del objeto personalizado. Si ha instalado versiones anteriores del objeto personalizado en la caché global de ensamblados, debe quitarlos antes de instalar la nueva versión. Para desinstalar un ensamblado, ejecute **gacutil.exe** y especifique el nombre del ensamblado con el `/u` opción.  
  
 Para obtener más información sobre la caché global de ensamblados, vea Herramienta Caché global de ensamblados (Gactutil.exe) en [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] Tools.  
  
##  <a name="troubleshooting"></a>Solución de problemas de la implementación  
 Si el objeto personalizado aparece en el **cuadro de herramientas** o la lista de objetos disponibles, pero no se puede agregar a un paquete, intente lo siguiente:  
  
1.  Busque en la memoria caché de ensamblados global varias versiones del componente. Si hay varias versiones del componente en la memoria caché de ensamblados global, el diseñador quizá no pueda cargar el componente. Elimine todas las instancias del ensamblado de la memoria caché de ensamblados global y vuelva a agregar el ensamblado.  
  
2.  Asegúrese de que solo existe una instancia única del ensamblado en la carpeta de implementación.  
  
3.  Actualice el cuadro de herramientas.  
  
4.  Adjuntar [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] a **devenv.exe** y establezca un punto de interrupción para recorrer el código de inicialización para asegurarse de que se produce ninguna excepción.  
  
##  <a name="testing"></a>Probar y depurar el código  
 El enfoque más sencillo para depurar los métodos en tiempo de ejecución de un objeto personalizado consiste en iniciar **dtexec.exe** de [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] después de compilar el objeto personalizado y ejecutar un paquete que utiliza el componente.  
  
 Si desea depurar los métodos en tiempo de diseño del componente, como el **validar** método, abra un paquete que utiliza el componente en una segunda instancia de [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]y asociar a su **devenv.exe** proceso.  
  
 Si desea depurar los métodos en tiempo de ejecución del componente cuando está abierto y ejecutándose un paquete [!INCLUDE[ssIS](../../includes/ssis-md.md)] diseñador, debe forzar una pausa en la ejecución del paquete para que también se pueden adjuntar a la **DtsDebugHost.exe** proceso.  
  
#### <a name="to-debug-an-objects-run-time-methods-by-attaching-to-dtexecexe"></a>Para depurar los métodos en tiempo de ejecución de un objeto adjuntándolos a dtexec.exe  
  
1.  Firme e integre el proyecto en la configuración de depuración, impleméntelo e instálelo en la memoria caché de ensamblados global tal y como se describe en este tema.  
  
2.  En el **depurar** ficha de **propiedades del proyecto**, seleccione **iniciar programa externo** como el **acción de inicio**y busque **dtexec.exe**, que se instala de forma predeterminada en C:\Program Files\Microsoft SQL Server\130\DTS\Binn.  
  
3.  En el **opciones de línea de comandos** cuadro de texto **opciones de inicio**, escriba los argumentos de línea de comandos necesarios para ejecutar un paquete que usa el componente. A menudo el argumento de la línea de comandos estará compuesto del modificador /F[ILE] seguido de la ruta de acceso y nombre de archivo del archivo .dtsx. Para obtener más información, vea [dtexec Utility](../../integration-services/packages/dtexec-utility.md).  
  
4.  Establezca los puntos de interrupción en el código fuente donde sea adecuado en los métodos en tiempo de ejecución del componente.  
  
5.  Ejecutar el proyecto.  
  
#### <a name="to-debug-a-custom-objects-design-time-methods-by-attaching-to-sql-server-data-tools"></a>Para depurar los métodos en tiempo de diseño de un objeto personalizado adjuntándolos a las herramientas de datos de SQL Server  
  
1.  Firme e integre el proyecto en la configuración de depuración, impleméntelo e instálelo en la memoria caché de ensamblados global tal y como se describe en este tema.  
  
2.  Establezca puntos de interrupción en el código fuente donde se adecuado en los métodos en tiempo de diseño del objeto personalizado.  
  
3.  Abra una segunda instancia de [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] y cargue un proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contiene un paquete que utiliza el objeto personalizado.  
  
4.  Desde la primera instancia de [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)], adjuntar a la segunda instancia de **devenv.exe** en que se carga el paquete seleccionando **adjuntar al proceso** desde el **depurar** menú de la primera instancia.  
  
5.  Ejecute el paquete desde la segunda instancia de [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)].  
  
#### <a name="to-debug-a-custom-objects-run-time-methods-by-attaching-to-sql-server-data-tools"></a>Para depurar los métodos en tiempo de ejecución de un objeto personalizado adjuntándolos a las herramientas de datos de SQL Server  
  
1.  Después de haber completado los pasos indicados en el procedimiento anterior, fuerce una pausa en la ejecución del paquete de modo que puede adjuntar a **DtsDebugHost.exe**. Puede forzar esta pausa mediante la adición de un punto de interrupción a la **OnPreExecute** eventos, o agregando una tarea Script al proyecto y escriba el script que muestra un cuadro de mensaje modal.  
  
2.  Ejecute el paquete. Cuando se produce la pausa, cambie a la instancia de [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] en el que es el proyecto de código abierto y, a continuación, seleccione **adjuntar al proceso** desde el **depurar** menú. Asegúrese de conectar a la instancia de **DtsDebugHost.exe** aparece como **administrado, x86** en el **tipo** columna, no a la instancia aparece como **x86** solo.  
  
3.  Volver al paquete en pausa y continuar más allá del punto de interrupción o haga clic en **Aceptar** para descartar el cuadro de mensajes generado por la tarea de secuencia de comandos y continuar la ejecución del paquete y la depuración.  
  
## <a name="see-also"></a>Vea también  
 [Desarrollar objetos personalizados para Integration Services](../../integration-services/extending-packages-custom-objects/developing-custom-objects-for-integration-services.md)   
 [Conservar objetos personalizados](../../integration-services/extending-packages-custom-objects/persisting-custom-objects.md)   
 [Herramientas para solucionar problemas con el desarrollo de paquetes](../../integration-services/troubleshooting/troubleshooting-tools-for-package-development.md)  
  
  
