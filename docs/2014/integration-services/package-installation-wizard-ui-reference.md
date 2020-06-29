---
title: Referencia de interfaz de usuario del Asistente para la instalación de paquetes | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.deploymentwizard.confirminstallation.f1
- sql12.dts.deploymentwizard.deploydtspackages.f1
- sql12.dts.deploymentwizard.selectinstfolder.f1
- sql12.dts.deploymentwizard.specifytargetsqlserver.f1
- sql12.dts.deploymentwizard.welcome.f1
- sql12.dts.deploymentwizard.finish.f1
- sql12.dts.deploymentwizard.configurepackages.f1
- sql12.dts.deploymentwizard.packagevalidation.f1
helpviewer_keywords:
- Package Installer Wizard
ms.assetid: 6fca44d9-5001-4644-bcf3-c2d10a674b97
author: chugugrace
ms.author: chugu
ms.openlocfilehash: cc500615774a67bae70e9c9fa8845db166f44466
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2020
ms.locfileid: "85423882"
---
# <a name="package-installation-wizard-ui-reference"></a>Referencia de la interfaz de usuario del Asistente para la instalación de paquetes
  Use el **Asistente para la instalación de paquetes** para implementar un proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , incluidos los paquetes y los distintos archivos que contienen, así como las dependencias del paquete.  
  
 Antes de implementar paquetes, puede crear configuraciones y después implementarlas con los paquetes. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] utiliza configuraciones para actualizar dinámicamente las propiedades de los paquetes y los objetos de paquete en tiempo de ejecución. Por ejemplo, la cadena de conexión de una conexión OLE DB puede establecerse dinámicamente en tiempo de ejecución proporcionando una configuración que asigne un valor a la propiedad que contiene la cadena de conexión.  
  
 No se puede ejecutar el Asistente para la instalación de paquetes hasta que se genere un proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] y se cree una utilidad de implementación. Para más información, consulte [Deploy Packages by Using the Deployment Utility](../../2014/integration-services/deploy-packages-by-using-the-deployment-utility.md).  
  
 En las siguientes secciones se describen las páginas del asistente.  
  
## <a name="welcome-to-the-package-installation-wizard-page"></a>Asistente para la instalación de paquetes (página principal)  
 Use el **Asistente para la instalación de paquetes** para implementar un proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] para el que ha creado una utilidad de implementación de paquetes.  
  
 **No volver a mostrar esta página**  
 Seleccione para omitir la página de inicio al volver a ejecutar el asistente.  
  
 **Siguiente**  
 Va a la siguiente página del asistente.  
  
 **Finalizar**  
 Salte a la página Salir del Asistente para la instalación de paquetes. Puede usar esta opción tras volver a las páginas anteriores del asistente para revisar las elecciones o si ha especificado todas las opciones requeridas.  
  
## <a name="configure-packages-page"></a>Página Configurar paquetes  
 Utilice la página **Configurar paquetes** para modificar la configuración de los paquetes.  
  
### <a name="options"></a>Opciones  
 **Archivo de configuración**  
 Para modificar el contenido de un archivo de configuración, seleccione el archivo en la lista.  
  
 **Related Topics:** [Create Package Configurations](../../2014/integration-services/create-package-configurations.md)  
  
 **Ruta de acceso**  
 Muestra la ruta de acceso de la propiedad que debe configurarse.  
  
 **Tipo**  
 Muestra el tipo de datos de la propiedad.  
  
 **Valor**  
 Especifique el valor de la configuración.  
  
 **Siguiente**  
 Va a la siguiente página del asistente.  
  
 **Finalizar**  
 Salte a la página Salir del Asistente para la instalación de paquetes. Puede usar esta opción tras volver a las páginas anteriores del asistente para revisar las elecciones o si ha especificado todas las opciones requeridas.  
  
## <a name="confirm-installation-page"></a>Página Confirmar la instalación  
 Use la página **Confirmar la instalación** para iniciar la instalación de paquetes, ver el estado y ver la información que utilizará el asistente para instalar los archivos del proyecto especificado.  
  
 **Siguiente**  
 Instale los paquetes y sus dependencias y vaya a la siguiente página del asistente una vez completada la instalación.  
  
 **Estado**  
 Muestra el progreso de la instalación del paquete.  
  
 **Finalizar**  
 Vaya a la página Salir del Asistente para la instalación de paquetes. Utilice esta opción si ha comprobado las páginas del asistente para revisar sus elecciones y ha especificado todas las opciones necesarias.  
  
## <a name="deploy-ssis-packages-page"></a>Página Implementar paquetes SSIS  
 Use la página **Implementar paquetes SSIS** para especificar dónde instalar paquetes de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] y sus dependencias.  
  
### <a name="options"></a>Opciones  
 **Implementación en el sistema de archivos**  
 Implementa paquetes y dependencias en una carpeta determinada del sistema de archivos.  
  
 **Implementación en SQL Server**  
 Implementa paquetes y dependencias en una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Use esta opción si [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] comparte paquetes entre servidores. Las dependencias de paquetes se instalan en la carpeta especificada del sistema de archivos.  
  
 **Validar los paquetes después de la instalación**  
 Indica si se van a validar los paquetes después de la instalación.  
  
 **Siguiente**  
 Va a la siguiente página del asistente.  
  
 **Finalizar**  
 Salte a la página Salir del Asistente para la instalación de paquetes. Puede usar esta opción tras volver a las páginas anteriores del asistente para revisar las elecciones o si ha especificado todas las opciones requeridas.  
  
## <a name="packages-validation-page"></a>Página Validación de paquetes  
 Use la página **Validación de paquetes** para ver el progreso y los resultados de la validación del paquete.  
  
 **Siguiente**  
 Va a la siguiente página del asistente.  
  
## <a name="select-installation-folder-page"></a>Página Seleccionar la carpeta de instalación  
 Use la página **Seleccionar la carpeta de instalación** para especificar la carpeta del sistema de archivos en la que desea instalar los paquetes y sus dependencias.  
  
### <a name="options"></a>Opciones  
 **Carpeta**  
 Permite especificar la ruta y la carpeta en la que se desea copiar el paquete y sus dependencias.  
  
 **Examinar**  
 Permite ir a la carpeta de destino mediante el cuadro de diálogo **Buscar carpeta** .  
  
 **Siguiente**  
 Va a la siguiente página del asistente.  
  
 **Finalizar**  
 Salte a la página Salir del Asistente para la instalación de paquetes. Puede usar esta opción tras volver a las páginas anteriores del asistente para revisar las elecciones o si ha especificado todas las opciones requeridas.  
  
## <a name="specify-target-sql-server-page"></a>Página Especificar el SQL Server de destino  
 Use la página **Especificar el SQL Server de destino** para especificar las opciones de implementación del paquete en una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
### <a name="options"></a>Opciones  
 **Nombre del servidor**  
 Especifique el nombre del servidor en el que se implementarán los paquetes.  
  
 **Utilizar autenticación de Windows**  
 Permite especificar si se usará la autenticación de Windows al iniciar una sesión en el servidor. Para obtener una mayor seguridad, es recomendable utilizar la autenticación de Windows.  
  
 **Usar autenticación SQL Server**  
 Permite especificar si el paquete debe usar la autenticación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] al iniciar una sesión en el servidor. Si usa la autenticación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , debe proporcionar un nombre de usuario y una contraseña.  
  
 **Nombre de usuario**  
 Especifique un nombre de usuario.  
  
 **Contraseña**  
 Especifique una contraseña.  
  
 **Ruta de acceso de paquete**  
 Especifique el nombre de la carpeta lógica o escribe "/" para la carpeta predeterminada.  
  
 Para seleccionar la carpeta en el cuadro de diálogo **paquete SSIS** , haga clic en examinar (...). Sin embargo, el cuadro de diálogo no proporciona un medio para seleccionar la carpeta predeterminada. Si desea utilizar la carpeta predeterminada, tiene que escribir "/" en el cuadro de texto.  
  
> [!NOTE]  
>  Si no escribe una ruta de acceso del paquete válida, aparece el mensaje de error siguiente: "Uno o más argumentos no son válidos."  
  
 **Basar el cifrado en el almacenamiento del servidor**  
 Seleccione estas características de seguridad del [!INCLUDE[ssDE](../includes/ssde-md.md)] para contribuir a proteger los paquetes.  
  
 **Siguiente**  
 Va a la siguiente página del asistente.  
  
 **Finalizar**  
 Salte a la página Salir del Asistente para la instalación de paquetes. Puede usar esta opción tras volver a las páginas anteriores del asistente para revisar las elecciones o si ha especificado todas las opciones requeridas.  
  
## <a name="finish-the-package-installation-page"></a>Página Salir del Asistente para la instalación de paquetes  
 Use la página **Salir del Asistente para la instalación de paquetes** para ver un resumen de los resultados de la instalación del paquete. Esta página muestra información, como el nombre del proyecto implementado de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , los paquetes instalados, los archivos de configuración y la ubicación de la instalación.  
  
 **Finalizar**  
 Para salir del asistente, haga clic en **Finalizar**.  
  
## <a name="see-also"></a>Consulte también  
 [Implementación de paquetes &#40;SSIS&#41;](packages/legacy-package-deployment-ssis.md)  
  
  
