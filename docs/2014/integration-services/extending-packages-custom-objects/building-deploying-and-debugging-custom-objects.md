---
title: Generar, implementar y depurar objetos personalizados | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- custom objects [Integration Services]
ms.assetid: b03685bc-5398-4c3f-901a-1219c1098fbe
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 131f86336c2eecb4995304fc87e15a7b910833ab
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62768991"
---
# <a name="building-deploying-and-debugging-custom-objects"></a>Generar, implementar y depurar objetos personalizados
  Después de haber escrito el código para un objeto personalizado de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], debe generar, implementar e integrar el ensamblado en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] para que esté disponible para su uso en paquetes, y probarlo y depurarlo.  
  
##  <a name="top"></a> Pasos para generar, implementar y depurar un objeto personalizado para Integration Services  
 Ya ha escrito la funcionalidad personalizada para el objeto. Ahora tiene que probarlo y hacer que esté disponible para los usuarios. Los pasos son muy similares para todos los tipos de objetos personalizados que puede crear para [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 A continuación figuran los pasos que debe seguir para generar, implementar y depurar el objeto:  
  
1.  [Firme](#signing) el ensamblado que se va a generar con un nombre seguro.  
  
2.  [Genere](#building) el ensamblado.  
  
3.  [Implemente](#deploying) el ensamblado; para ello, muévalo o cópielo en la carpeta de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] adecuada.  
  
4.  [Instale](#installing) el ensamblado en la caché global de ensamblados (GAC).  
  
     El objeto se agregará automáticamente al cuadro de herramientas.  
  
5.  [Solucione los problemas](#troubleshooting) de la implementación, si es necesario.  
  
6.  [Pruebe](#testing) y depure el código.  
  
##  <a name="signing"></a> Firmar el ensamblado  
 Cuando se tiene pensado compartir un ensamblado, se debe instalar en la memoria caché de ensamblados global. Una vez agregado el ensamblado a la memoria caché de ensamblados global, aplicaciones como [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] pueden utilizarlo. Un requisito de la memoria caché de ensamblados global es que el ensamblado se debe firmar con un nombre seguro, que garantiza que el ensamblado es único de forma global. Un ensamblado con nombre seguro especifica un nombre completo que incluye el nombre del ensamblado, la referencia cultural, la clave pública y el número de versión. El motor en tiempo de ejecución utiliza esta información para localizar el ensamblado y distinguirlo entre otros ensamblados con el mismo nombre.  
  
 Para firmar un ensamblado con un nombre seguro, es necesario crear o tener antes un par de claves publica y privada. Este par de claves criptográficas pública y privada se usa al realizar la compilación para crear un ensamblado con nombre seguro.  
  
 Para obtener más información sobre los nombres seguros y los pasos que debe seguir para firmar un ensamblado, consulte los temas siguientes en la documentación del SDK de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]:  
  
-   Ensamblados con nombre seguro  
  
-   Crear un par de claves  
  
-   Firmar un ensamblado con un nombre seguro  
  
 Puede firmar con facilidad el ensamblado con un nombre seguro en [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] durante la generación. En el cuadro de diálogo **Propiedades del proyecto**, seleccione la pestaña **Firma**. Seleccione la opción para **Firmar el ensamblado** y, a continuación, proporcione la ruta de acceso del archivo de claves (.snk).  
  
##  <a name="building"></a> Generar el ensamblado  
 Después de firmar el proyecto, debe generar o volver a generar el proyecto o la solución utilizando los comandos disponibles en el menú **Generar** de [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. La solución puede contener un proyecto independiente para una interfaz de usuario personalizada, que también se debe firmar con un nombre seguro y se puede generar al mismo tiempo.  
  
 El método más sencillo para realizar los dos pasos siguientes (implementar el ensamblado e instalarlo en la memoria caché de ensamblados global) es crear un script con estos pasos como un evento posterior a la compilación en [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]. Los eventos de compilación están disponibles en la página **Compilar** de Propiedades del proyecto para un proyecto de [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] y en la página **Eventos de compilación** para un proyecto de C#. Es necesaria la ruta de acceso completa para las utilidades de símbolo del sistema como **gacutil.exe**. Son necesarias comillas alrededor de las rutas de acceso que contienen espacios en blanco y alrededor de macros como $(TargetPath) que se expanden a rutas de acceso que contienen espacios en blanco.  
  
 A continuación figura un ejemplo de una línea de comandos del evento posterior a la generación para un proveedor de registro personalizado:  
  
```  
"C:\Program Files (x86)\Microsoft SDKs\Windows\v7.0A\bin\NETFX 4.0 Tools\gacutil.exe" -u $(TargetName)  
"C:\Program Files (x86)\Microsoft SDKs\Windows\v7.0A\bin\NETFX 4.0 Tools\gacutil.exe" -i $(TargetFileName)  
copy $(TargetFileName) "C:\Program Files\Microsoft SQL Server\120\DTS\LogProviders "  
```  
  
##  <a name="deploying"></a> Implementar el ensamblado  
 El Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] busca los objetos personalizados disponibles para su uso en paquetes enumerando los archivos buscados en una serie de carpetas que se crean cuando se instala [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Cuando el valor predeterminado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se usa la configuración de la instalación, este conjunto de carpetas se encuentra en **C:\Program Files\Microsoft SQL Server\120\DTS**. Sin embargo, si crea un programa de instalación para el objeto personalizado, se debe comprobar el valor de la **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\SSIS\Setup\DtsPath** clave del registro para comprobar la ubicación de este carpeta.  
  
 Puede colocar el ensamblado en la carpeta de dos maneras:  
  
-   Copiar o mover el ensamblado compilado a la carpeta adecuada después de generarlo. (Para su comodidad, puede incluir el comando de copia en un evento posterior a la generación).  
  
-   Generar el ensamblado directamente en la carpeta adecuada.  
  
 Las carpetas de implementación siguientes bajo **C:\Program Files\Microsoft SQL Server\120\DTS** se usan para los distintos tipos de objetos personalizados:  
  
|Objeto personalizado|Carpeta de implementación|  
|-------------------|-----------------------|  
|Tarea|Tareas|  
|Administrador de conexiones|Conexiones|  
|Proveedor de registro|LogProviders|  
|Componente de flujo de datos|PipelineComponents|  
  
> [!NOTE]  
>  Los ensamblados se copian en estas carpetas para admitir la enumeración de tareas disponibles, administradores de conexión, etc. Por consiguiente no tiene que implementar los ensamblados que contienen solo la interfaz de usuario personalizada para los objetos personalizados en estas carpetas.  
  
##  <a name="installing"></a> Instalar el ensamblado en la memoria caché de ensamblados global  
 Para instalar el ensamblado de tarea en la caché global de ensamblados (GAC), use la herramienta de línea de comandos **gacutil.exe** o arrastre los ensamblados al directorio `%system%\assembly`. Para su comodidad, puede incluir también la llamada a **gacutil.exe** en un evento posterior a la compilación.  
  
 El comando siguiente instala un componente denominado *MyTask.dll* en la GAC mediante **gacutil.exe**.  
  
 `gacutil /iF MyTask.dll`  
  
 Se debe cerrar y volver a abrir el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] después de instalar una nueva versión del objeto personalizado. Si ha instalado versiones anteriores del objeto personalizado en la caché global de ensamblados, debe quitarlos antes de instalar la nueva versión. Para desinstalar un ensamblado, ejecute **gacutil.exe** y especifique el nombre del ensamblado con la opción `/u`.  
  
 Para obtener más información sobre la caché global de ensamblados, vea Herramienta Caché global de ensamblados (Gactutil.exe) en [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] Tools.  
  
##  <a name="troubleshooting"></a> Solucionar problemas relacionados con la implementación  
 Si el objeto personalizado aparece en el **cuadro de herramientas** o en la lista de objetos disponibles, pero no puede agregarlo a un paquete, pruebe lo siguiente:  
  
1.  Busque en la memoria caché de ensamblados global varias versiones del componente. Si hay varias versiones del componente en la memoria caché de ensamblados global, el diseñador quizá no pueda cargar el componente. Elimine todas las instancias del ensamblado de la memoria caché de ensamblados global y vuelva a agregar el ensamblado.  
  
2.  Asegúrese de que solo existe una instancia única del ensamblado en la carpeta de implementación.  
  
3.  Actualice el cuadro de herramientas.  
  
4.  Adjunte [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] a **devenv.exe** y establezca un punto de interrupción para reproducir paso a paso el código de inicialización con el fin de asegurarse de que no se produce ninguna excepción.  
  
##  <a name="testing"></a> Probar y depurar el código  
 El enfoque más sencillo para depurar los métodos en tiempo de ejecución de un objeto personalizado consiste en iniciar **dtexec.exe** desde [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] después de compilar el objeto personalizado y ejecutar un paquete que use el componente.  
  
 Si desea depurar los métodos en tiempo de diseño del componente, como el `Validate` método, abra un paquete que utiliza el componente en una segunda instancia de [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]y adjuntar a su **devenv.exe** proceso.  
  
 Si también quiere depurar los métodos en tiempo de ejecución del componente cuando un paquete está abierto y ejecutándose en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)], debe forzar una pausa en la ejecución del paquete para poder adjuntarlo también al proceso **DtsDebugHost.exe**.  
  
#### <a name="to-debug-an-objects-run-time-methods-by-attaching-to-dtexecexe"></a>Para depurar los métodos en tiempo de ejecución de un objeto adjuntándolos a dtexec.exe  
  
1.  Firme e integre el proyecto en la configuración de depuración, impleméntelo e instálelo en la memoria caché de ensamblados global tal y como se describe en este tema.  
  
2.  En el **depurar** ficha de **las propiedades del proyecto**, seleccione **iniciar programa externo** como el **acción de inicio**y busque  **DTExec.exe**, que se instala de forma predeterminada en C:\Program Files\Microsoft SQL Server\120\DTS\Binn.  
  
3.  En el cuadro de texto **Opciones de la línea de comandos**, en **Opciones de inicio**, escriba los argumentos de la línea de comandos necesarios para ejecutar un paquete que usa el componente. A menudo el argumento de la línea de comandos estará compuesto del modificador /F[ILE] seguido de la ruta de acceso y nombre de archivo del archivo .dtsx. Para más información, consulte [dtexec Utility](../packages/dtexec-utility.md).  
  
4.  Establezca los puntos de interrupción en el código fuente donde sea adecuado en los métodos en tiempo de ejecución del componente.  
  
5.  Ejecute el proyecto.  
  
#### <a name="to-debug-a-custom-objects-design-time-methods-by-attaching-to-sql-server-data-tools"></a>Para depurar los métodos en tiempo de diseño de un objeto personalizado adjuntándolos a las herramientas de datos de SQL Server  
  
1.  Firme e integre el proyecto en la configuración de depuración, impleméntelo e instálelo en la memoria caché de ensamblados global tal y como se describe en este tema.  
  
2.  Establezca puntos de interrupción en el código fuente donde se adecuado en los métodos en tiempo de diseño del objeto personalizado.  
  
3.  Abra una segunda instancia de [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] y cargue un proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contiene un paquete que utiliza el objeto personalizado.  
  
4.  En la primera instancia de [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)], adjúntelo a la segunda instancia de **devenv.exe** en la que se carga el paquete seleccionando **Adjuntar al proceso** en el menú **Depurar** de la primera instancia.  
  
5.  Ejecute el paquete desde la segunda instancia de [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)].  
  
#### <a name="to-debug-a-custom-objects-run-time-methods-by-attaching-to-sql-server-data-tools"></a>Para depurar los métodos en tiempo de ejecución de un objeto personalizado adjuntándolos a las herramientas de datos de SQL Server  
  
1.  Una vez completados los pasos enumerados en el procedimiento anterior, fuerce una pausa en la ejecución del paquete para que se pueda adjuntar a **DtsDebugHost.exe**. Para forzar esta pausa, agregue un punto de interrupción al evento `OnPreExecute` o agregue una tarea Script al proyecto y escriba el script que muestra un cuadro de mensaje modal.  
  
2.  Ejecute el paquete. Cuando se produzca la pausa, cambie a la instancia de [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] en la que está abierto el código del proyecto y seleccione **Adjuntar al proceso** en el menú **Depurar**. Asegúrese de adjuntarlo a la instancia de **DtsDebugHost.exe** que se muestra como **Administrado, x86** en la columna **Tipo**, no a la instancia mostrada solo como **x86**.  
  
3.  Vuelva al paquete en pausa y continúe más allá del punto de interrupción o haga clic en **Aceptar** para descartar el cuadro de mensaje generado por la tarea Script, y continuar con la ejecución y depuración del paquete.  
  
![Icono de Integration Services (pequeño)](../media/dts-16.gif "icono de Integration Services (pequeño)")**mantenerse actualizado con Integration Services**<br /> Para obtener las descargas, artículos, ejemplos y vídeos más recientes de Microsoft, así como soluciones seleccionadas de la comunidad, visite la página de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en MSDN:<br /><br /> [Visite la página de Integration Services en MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para recibir notificaciones automáticas de estas actualizaciones, suscríbase a las fuentes RSS disponibles en la página.  
  
## <a name="see-also"></a>Vea también  
 [Desarrollar objetos personalizados para Integration Services](developing-custom-objects-for-integration-services.md)   
 [Conservar objetos personalizados](persisting-custom-objects.md)   
 [Herramientas para solucionar problemas del desarrollo de paquetes](../troubleshooting/troubleshooting-tools-for-package-development.md)  
  
  
