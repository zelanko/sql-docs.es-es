---
title: Configurar la cuenta de ejecución desatendida (Administrador de configuración de SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- no credentials option [Reporting Services]
- security [Reporting Services], unattended report processing
- unattended report processing [Reporting Services]
- credentials [Reporting Services]
- external data sources [Reporting Services]
- accounts [Reporting Services]
- reports [Reporting Services], processing
ms.assetid: 4e50733e-bd8c-4bf6-8379-98b1531bb9ca
caps.latest.revision: 8
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 0cba2bc68d83c2d0b986324e2efa7f882bac6e76
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37321925"
---
# <a name="configure-the-unattended-execution-account-ssrs-configuration-manager"></a>Configurar la cuenta de ejecución desatendida (Administrador de configuración de SSRS)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] proporciona una cuenta especial que se utiliza para el procesamiento de informes en modo desatendido y para enviar solicitudes de conexión a través de la red. La cuenta se utiliza de las formas siguientes:  
  
-   Envíe las solicitudes de conexión a través de la red para los informes que usen la autenticación de base de datos, o conéctese a los orígenes de datos de informe externos que no requieran ni usen autenticación. Para obtener más información, consulte [especificar credenciales y la información de conexión de orígenes de datos de informe](../../integration-services/connection-manager/data-sources.md) en libros en pantalla de SQL Server.  
  
-   Recuperar archivos de imagen externos utilizados en el informe. Si desea utilizar un archivo de imagen y no puede obtener acceso al mismo a través de un acceso anónimo, puede configurar la cuenta de procesamiento de informes en modo desatendido y conceder el permiso de cuenta para obtener acceso al archivo.  
  
 El procesamiento de informes en modo desatendido hace referencia a cualquier proceso de ejecución de informe activado por un evento (sea un evento controlado por programación o de actualización de datos) y no por la solicitud de un usuario. El servidor de informes utiliza la cuenta de procesamiento de informes en modo desatendido para iniciar una sesión en el equipo que hospeda el origen de datos externo. Esta cuenta es necesaria porque las credenciales de la cuenta del servicio del servidor de informes no se han utilizado nunca para conectarse a otros equipos.  
  
> [!IMPORTANT]  
>  La configuración de esta cuenta es opcional. No obstante, si no la configura, limitará sus opciones para conectarse a algunos orígenes de datos y es posible que no pueda recuperar archivos de imagen desde equipos remotos. Si configura la cuenta, debe mantenerla actualizada. Concretamente, si permite que una contraseña expire o se modifica la información de la cuenta en Active Directory, se producirá el siguiente error la próxima vez que se procese un informe: "Error de inicio de sesión (rsLogonFailed) Error de inicio de sesión: nombre de usuario desconocido o contraseña incorrecta". Resulta esencial el mantenimiento adecuado de la cuenta de procesamiento de informes en modo desatendido, aunque no recupere nunca imágenes externas o no envíe nunca solicitudes de conexión a equipos externos. Si configura la cuenta pero se da cuenta de que no la está utilizando, puede eliminarla para evitar las tareas rutinarias de mantenimiento de la cuenta.  
  
## <a name="how-to-configure-the-account"></a>Cómo configurar la cuenta  
 Debe usar una cuenta de usuario de dominio. Para cumplir su propósito específico, esta cuenta debería ser distinta de la que se utiliza para ejecutar el servicio del servidor de informes. Asegúrese de utilizar una cuenta que tenga permisos mínimos (son suficientes los permisos de acceso de solo lectura con conexión de red) y acceso limitado a aquellos equipos que proporcionan los orígenes de datos y los recursos al servidor de informes. Para obtener más información, vea [Administrador de configuración de Reporting Services &#40;modo nativo&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
 Para especificar la cuenta, puede utilizar la herramienta Configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] o la utilidad **rsconfig** . La forma más fácil de configurar la cuenta de ejecución en modo desatendido es ejecutar la herramienta Configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y especificar las credenciales en la página Cuenta de ejecución.  
  
1.  Inicie la herramienta Configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y conéctese a la instancia del servidor de informes que desee configurar. Para obtener instrucciones, vea [Administrador de configuración de Reporting Services &#40;modo nativo&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
2.  En la página Cuenta de ejecución, seleccione **Especificar una cuenta de ejecución**.  
  
3.  Especifique la cuenta y la contraseña, vuelva a especificar esta última y, a continuación, haga clic en **Aplicar**.  
  
### <a name="using-rsconfig-utility"></a>Usar la utilidad RSCONFIG  
 Otra manera de establecer la cuenta es usar la utilidad **rsconfig** . Para especificar la cuenta, use el argumento **-e** de **rsconfig**. Al especificar el argumento **-e** de **rsconfig** , se indica a la utilidad que escriba la información de la cuenta en el archivo de configuración. No es necesario especificar una ruta de acceso para RSreportserver.config. Siga estos pasos para configurar la cuenta.  
  
1.  Cree o seleccione una cuenta de dominio que tenga acceso a los equipos y servidores que proporcionen datos o servicios a un servidor de informes. Debe utilizar una cuenta que tenga permisos reducidos (por ejemplo, permisos de solo lectura).  
  
2.  Abra un símbolo del sistema: en el menú **Inicio** , haga clic en **Ejecutar**, escriba **cmd**y haga clic en **Aceptar**.  
  
3.  Escriba el siguiente comando para configurar la cuenta de una instancia de servidor de informes local:  
  
     **rsconfig -e -u\<dominio/nombreDeUsuario> -p\<password>**  
  
 **rsconfig -e** admite argumentos adicionales. Para más información sobre la sintaxis y para ver ejemplos de comandos, vea [rsconfig (utilidad) &#40;SSRS&#41;](../tools/rsconfig-utility-ssrs.md) en los Libros en pantalla de SQL Server.  
  
### <a name="how-account-information-is-stored"></a>Cómo se almacena la información de la cuenta  
 Al establecer la cuenta, la configuración siguiente se especifica en forma de valores cifrados en el archivo RSreportserver.config de una instancia local o remota del servidor de informes:  
  
```  
<UnattendedExecutionAccount>  
     <UserName></UserName>  
     <Password></Password>  
     <Domain></Domain>  
</UnattendedExecutionAccount>  
```  
  
 Una vez que establece los valores, no puede descifrarlos para verlos en texto simple. Si comete un error al escribir los valores u olvida qué valores ha especificado, debe usar la herramienta de configuración de Reporting Services o ejecutar **rsconfig -e** para empezar de nuevo.  
  
## <a name="how-to-use-the-unattended-report-processing-account"></a>Cómo usar la cuenta de procesamiento de informes en modo desatendido  
 Para recuperar los archivos de imagen, el servidor de informes utiliza automáticamente la cuenta y no se requiere ninguna acción concreta por parte del usuario. Para utilizar la cuenta con el fin de conectarse a los orígenes de datos externos que proporcionan los datos a los informes, debe especificar una opción **Tipo de credencial** en la página de propiedades del origen de datos, en el origen de datos del informe o compartido:  
  
-   En el Administrador de informes o en un sitio de SharePoint, seleccione la opción **No se necesitan credenciales** .  
  
 La cuenta de procesamiento de informes desatendido se utiliza principalmente para conectarse a los servidores externos y no como inicio de sesión en los servidores de bases de datos. Si desea usar las credenciales de la cuenta para iniciar una sesión en una base de datos, debe especificarlas en la cadena de conexión. Puede especificar **Integrated Security=SSPI** si el servidor de la base de datos admite la seguridad integrada de Windows y la cuenta usada para el procesamiento de informes desatendido tiene permiso para leer la base de datos. De lo contrario, deberá especificar el nombre de usuario y la contraseña en la cadena de conexión, donde aparecerá en texto no cifrado para cualquier usuario que tenga permiso para modificar las propiedades de conexión al origen de datos.  
  
 Aunque no se le impide usar la cuenta de procesamiento de informes desatendido para recuperar datos tras realizar una conexión, no es una práctica recomendada. Se supone que la cuenta debe usarse para funciones muy concretas. Si la usa para recuperar datos, está quebrantando el propósito para el que está destinada.  
  
## <a name="how-to-maintain-the-unattended-report-processing-account"></a>Cómo mantener la cuenta de procesamiento de informes en modo desatendido  
 Una vez que defina la cuenta, debe asegurarse de que la cuenta y la contraseña se mantengan actualizadas. Puede utilizar la herramienta Configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para actualizar los valores de configuración que almacenan información sobre esta cuenta.  
  
1.  Inicie la herramienta Configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y conéctese a la instancia del servidor de informes que desee configurar.  
  
2.  En la página Cuenta de ejecución, compruebe que se haya activado **Especificar una cuenta de ejecución** .  
  
3.  Especifique la nueva cuenta o contraseña, vuelva a escribir la contraseña y, a continuación, haga clic en **Aplicar**.  
  
## <a name="how-to-delete-the-unattended-report-processing-account"></a>Cómo eliminar la cuenta de procesamiento de informes en modo desatendido  
 Si no utiliza la cuenta, puede eliminarla para evitar las tareas rutinarias de mantenimiento de la cuenta.  
  
1.  Inicie la herramienta Configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y conéctese a la instancia del servidor de informes que desee configurar.  
  
2.  En la página Cuenta de ejecución, desactive **Especificar una cuenta de ejecución**.  
  
3.  Haga clic en **Aplicar**.  
  
 La información de cuenta se quita del archivo RSReportServer.config.  
  
## <a name="see-also"></a>Vea también  
 [Administrador de configuración de Reporting Services &#40;SUPR&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)  
  
  
