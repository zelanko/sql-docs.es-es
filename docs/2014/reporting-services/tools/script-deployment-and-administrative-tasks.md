---
title: Script para tareas administrativas y de implementación | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- scripts [Reporting Services]
- moving reports
- report servers [Reporting Services], duplicating settings
- deploying [Reporting Services], scripts
- copying report server settings
- administrative tasks [Reporting Services]
- duplicating report server environment
- migrating reports [Reporting Services]
- scripts [Reporting Services], deployments
- transferrng reports
- reports [Reporting Services], migrating
ms.assetid: d0416c9e-e3f9-456d-9870-2cfd2c49039b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d0ea3b81f69b46fbb829879f9976cb45a11ab803
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/22/2019
ms.locfileid: "72783347"
---
# <a name="script-deployment-and-administrative-tasks"></a>Script para tareas administrativas y de implementación
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] admite el uso de scripts para automatizar las tareas rutinarias de instalación, implementación y administración. La implementación de un servidor de informes es un proceso de varios pasos en el que deben usarse varias herramientas y procedimientos de configuración: no existe ningún programa o método que automatice todas las tareas.  
  
 Tampoco se recomienda automatizar siempre todos los pasos. A veces, la manera más sencilla y eficaz de realizar un paso es hacerlo manualmente o a través de una herramienta gráfica. Por ejemplo, si se desea implementar muchos informes y modelos, es mejor copiar las bases de datos del servidor de informes que escribir código para volver a crear el entorno del servidor de informes.  
  
 Algunos pasos requieren código personalizado. Por ejemplo, la configuración de las direcciones URL para el servicio web y el Administrador de informes se puede automatizar, pero solo si se escribe código personalizado que realice llamadas al proveedor WMI (Instrumental de administración de Windows) del servidor de informes. Si no se desea escribir código, deberá usarse la herramienta de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para realizar este paso.  
  
 Para ejecutar el script que configura un servidor de informes, debe ser un administrador local en el equipo que está configurando. Para obtener más información, vea [Configurar un servidor de informes para la administración remota](../report-server/configure-a-report-server-for-remote-administration.md).  
  
 En este tema se describen los enfoques recomendados para automatizar algunos pasos específicos. Se mencionan varios programas e interfaces de programación; podrá ver descripciones de cada uno de ellos más adelante en este tema.  
  
## <a name="deployment-tasks-and-how-to-automate-them"></a>Tareas de implementación y procedimientos para automatizarlas  
 En la tabla siguiente se resumen todas las tareas de instalación y configuración que son necesarias para implementar un servidor de informes. Quizás le sea de utilidad para relacionar una tarea específica con un método que le permita automatizarla o realizarla de manera desatendida.  
  
|Tarea|Método|  
|----------|--------------|  
|Instalar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|Puede ejecutar el programa de instalación desde la línea de comandos para realizar una instalación desatendida.<br /><br /> Puede usar el programa de instalación para instalar y configurar un servidor de informes, pero solo si especifica la opción de configuración predeterminada y el sistema cumple todos los requisitos de este tipo de instalación. Si no puede instalar la configuración predeterminada, deberá realizar una instalación de solo archivos.|  
|Configurar la cuenta de servicio.|La cuenta de servicio se configura inicialmente a través de la instalación. Para automatizar los cambios a la cuenta de servicio como una tarea posterior a la instalación, debe escribir código personalizado que realice llamadas al proveedor WMI del servidor de informes. No hay ninguna utilidad de símbolo del sistema o plantillas de script para configurar la cuenta de servicio mediante programación.<br /><br /> Si los requisitos de codificación evitan que automatice este paso, puede configurar con facilidad la cuenta manualmente ejecutando la herramienta de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para más información, vea [Configurar una cuenta de servicio &#40;Administrador de configuración de SSRS&#41;](../../sql-server/install/configure-a-service-account-ssrs-configuration-manager.md).|  
|Configurar el servicio web del servidor de informes y las direcciones URL del Administrador de informes.|Debe escribir código personalizado que realice llamadas al proveedor WMI del servidor de informes. No hay ninguna utilidad de línea de comandos o plantillas de script para configurar las direcciones URL.<br /><br /> Si desea evitar escribir código, puede configurar las direcciones URL manualmente ejecutando la herramienta de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para obtener más información, vea [Configurar una dirección URL &#40;Administrador de configuración de SSRS&#41;](../install-windows/configure-a-url-ssrs-configuration-manager.md).|  
|Crear la base de datos del servidor de informes.|Debe escribir código personalizado que realice llamadas al proveedor WMI del servidor de informes. No hay ninguna utilidad de símbolo del sistema o plantillas de script para crear las bases de datos del servidor de informes y RSExecRole.<br /><br /> Si desea evitar escribir código, puede crear la base de datos manualmente ejecutando la herramienta de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para más información, vea [Crear una base de datos del servidor de informes de modo nativo &#40;Administrador de configuración de SSRS&#41;](../install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md).|  
|Configurar la conexión a la base de datos del servidor de informes.|Si va a cambiar la cadena de conexión, la cuenta o la contraseña o el tipo de autenticación, ejecute la utilidad **rsconfig** para configurar la conexión. Para más información, vea [Configurar una conexión a la base de datos del servidor de informes &#40;Administrador de configuración de SSRS&#41;](../../sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md) y [rsconfig (utilidad) &#40;SSRS&#41;](rsconfig-utility-ssrs.md).<br /><br /> No puede utilizar rsconfig.exe para crear o actualizar la base de datos. La base de datos y RSExecRole deben existir ya.|  
|Configurar una implementación escalada|Para automatizar una implementación escalada, elija uno de los métodos siguientes:<br /><br /> Ejecute la utilidad rskeymgmt.exe para unir instancias del servidor de informes a una instalación existente. Para más información, vea [Agregar y quitar claves de cifrado para implementaciones escaladas &#40;Administrador de configuración de SSRS&#41;](../install-windows/add-and-remove-encryption-keys-for-scale-out-deployment.md).<br /><br /> Escriba código personalizado que se ejecute en el proveedor WMI del servidor de informes.|  
|Realizar una copia de seguridad de las claves de cifrado|Para automatizar el procedimiento de copia de seguridad de las claves de cifrado, elija uno de los métodos siguientes:<br /><br /> Ejecute la utilidad rskeymgmt.exe para realizar la copia de seguridad de las claves. Para obtener más información, vea [Hacer copia de seguridad y restaurar claves de cifrado de Reporting Services](../install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md).<br /><br /> Escriba código personalizado que se ejecute en el proveedor WMI del servidor de informes.|  
|Configurar el correo electrónico del servidor de informes|Escriba código personalizado que se ejecute en el proveedor WMI de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . El proveedor admite un subconjunto de los valores de configuración de correo electrónico.<br /><br /> Aunque el archivo RSReportServer.config incluye toda la configuración, no utilice el archivo de forma automatizada. En concreto, no utilice un archivo por lotes para copiar el archivo en otro servidor de informes. Cada archivo de configuración incluye valores específicos de la instancia actual. Dichos valores no serán válidos en otras instancias del servidor de informes.<br /><br /> Para obtener más información sobre la configuración, vea [configurar un servidor de informes para &#40;la entrega&#41;de correo electrónico SSRS Configuration Manager](../../sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md).|  
|Configurar la cuenta de ejecución desatendida|Para automatizar la configuración de la cuenta de procesamiento desatendido, elija uno de los métodos siguientes:<br /><br /> Ejecute la utilidad rsconfig.exe para configurar la cuenta. Para obtener más información, vea [Configurar la cuenta de ejecución desatendida &#40;Administrador de configuración de SSRS&#41;](../install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md).<br /><br /> Escriba código personalizado que realice llamadas al proveedor WMI del servidor de informes.|  
|Implementar contenido existente en otro servidor de informes, incluyendo la jerarquía de carpetas, las asignaciones de roles, los informes, las suscripciones, las programaciones, los orígenes de datos y los recursos.|La mejor forma de volver a crear un entorno de servidor de informes existente es copiar la base de datos del servidor de informes en una nueva instancia del servidor de informes.<br /><br /> Un método alternativo es escribir código personalizado que vuelva a crear el contenido del servidor de informes existente mediante programación. Sin embargo, tenga en cuenta que las suscripciones, las instantáneas del informe y el historial del informe no se pueden volver a crear mediante programación.<br /><br /> Algunas implementaciones pueden beneficiarse de ambas técnicas, es decir, restaurar una base de datos del servidor de informes y, después, ejecutar código personalizado con el fin de modificar la base de datos del servidor de informes para una instalación específica.<br /><br /> Para obtener un ejemplo detallado, vea [Sample Reporting Services rs.exe Script to Migrate Content between Report Servers](sample-reporting-services-rs-exe-script-to-copy-content-between-report-servers.md).<br /><br /> Para más información sobre cómo modificar la ubicación de una base de datos del servidor de informes, vea [Mover las bases de datos del servidor de informes a otro equipo &#40;Modo nativo de SSRS&#41;](../report-server/moving-the-report-server-databases-to-another-computer-ssrs-native-mode.md). Para obtener más información acerca de la creación del entorno del servidor de informes mediante programación, vea la sección "Usar script para migrar las carpetas y el contenido del servidor de informes" en este tema.|  
  
## <a name="tools-and-technologies-for-automating-server-deployment"></a>Herramientas y tecnologías para automatizar la implementación del servidor  
 En la lista siguiente se resumen los programas y las interfaces que se pueden utilizar para automatizar las tareas de implementación y mantenimiento:  
  
-   El programa de instalación se puede ejecutar en modo desatendido para instalar y, en algunos casos, configurar los componentes del servidor de informes. Debe usar la opción de instalación de solo archivos para que el programa de instalación configure una instancia de servidor de informes.  
  
-   Se pueden usar el proveedor WMI de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y las utilidades de línea de comandos de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para la configuración local y remota del servidor.  
  
     El proveedor WMI de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] expone las clases, propiedades y métodos que permiten al usuario configurar todos los aspectos de una instalación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , lo que incluye la especificación de cuentas de servicio, la configuración de direcciones URL, la creación y configuración de la base de datos del servidor de informes o la configuración de un servidor de informes para la entrega por correo electrónico. Para utilizar el proveedor WMI, es necesario escribir script o código personalizados. Para más información, vea [Obtener acceso al proveedor WMI de Reporting Services](access-the-reporting-services-wmi-provider.md).  
  
     Las utilidades de la línea de comandos (rsconfig.exe y rskeymgmt.exe) son una alternativa a escribir código. Se pueden escribir archivos por lotes que ejecuten las utilidades. Estas utilidades permiten automatizar algunas tareas de configuración, pero no todas.  
  
-   La herramienta de host del script del servidor de informes (rs.exe) puede ejecutar código personalizado de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] que se haya escrito para volver a crear o mover el contenido de un servidor de informes a otro. Con este método, se escribe script en [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)], se guarda como un archivo .rss y, después, se usa rs.exe para ejecutarlo en el servidor de informes de destino. El script escrito puede llamar a la interfaz SOAP para el servicio web del servidor de informes. Los scripts de implementación se escriben siguiendo este método porque es posible volver a crear un espacio de nombres de carpetas del servidor de informes y su contenido, así como volver a crear la seguridad basada en roles.  
  
-   En la versión [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] se introdujeron los cmdlets de PowerShell para el modo integrado de SharePoint. Puede utilizar PowerShell para configurar y administrar la integración de SharePoint.  Para obtener más información, vea [Cmdlets de PowerShell para el modo de SharePoint de Reporting Services](../powershell-cmdlets-for-reporting-services-sharepoint-mode.md).  
  
## <a name="use-scripts-to-migrate-report-server-content-and-folders"></a>Usar scripts para migrar contenido y carpetas del servidor de informes  
 Se pueden escribir scripts que dupliquen un entorno de servidor de informes en otra instancia de servidor de informes. Los scripts de implementación suelen escribirse en [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] y, a continuación, se procesan mediante la utilidad del host de script del servidor de informes.  
  
 Para obtener un ejemplo detallado, vea [Sample Reporting Services rs.exe Script to Migrate Content between Report Servers](sample-reporting-services-rs-exe-script-to-copy-content-between-report-servers.md).  
  
 Utilice scripts para copiar carpetas, orígenes de datos compartidos, recursos, informes, asignaciones de roles y parámetros de un servidor a otro. Puede escribir un script para una instancia de servidor de informes y, a continuación, ejecutarlo en otro servidor para volver a crear el espacio de nombres del servidor de informes. Si existen varios servidores de informes en la implementación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , puede ejecutar el script en cada servidor individualmente para configurar todos los servidores de la misma manera.  
  
 En la siguiente lista, se describen los pasos necesarios para migrar informes de un servidor a otro.  
  
1.  Defina la variable de script con la dirección URL del servidor de informes de origen.  
  
2.  Use los métodos <xref:ReportService2010.ReportingService2010.GetItemDefinition%2A> y <xref:ReportService2010.ReportingService2010.GetProperties%2A> para recuperar la definición de informe y las propiedades del informe.  
  
3.  Establezca la dirección URL para que señale al servidor de destino.  
  
4.  Use el método <xref:ReportService2010.ReportingService2010.CreateCatalogItem%2A> , pasando las propiedades devueltas desde <xref:ReportService2010.ReportingService2010.GetProperties%2A> y la definición del informe devuelta por <xref:ReportService2010.ReportingService2010.GetItemDefinition%2A>.  
  
 Combinando métodos de obtención y creación, puede realizar pasos similares que le permitan migrar parámetros, carpetas, orígenes de datos compartidos y recursos. Para más información sobre los métodos disponibles, vea [Referencia técnica &#40;SSRS&#41;](../technical-reference-ssrs.md).  
  
> [!NOTE]  
>  Los scripts se ejecutan con las credenciales de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows del usuario que ejecuta el script, salvo que las credenciales se establezcan explícitamente.  
  
 Para obtener más información sobre cómo ejecutar y dar formato a un archivo de script, vea [Script con la utilidad rs.exe y el servicio Web](script-with-the-rs-exe-utility-and-the-web-service.md).  
  
## <a name="using-scripts-to-set-server-properties"></a>Usar scripts para establecer propiedades del servidor  
 Puede escribir scripts que establezcan propiedades del sistema en el servidor de informes. El script de [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] .NET siguiente muestra una manera de establecer las propiedades. Este ejemplo deshabilita el control ActiveX RSClientPrint, aunque es posible sustituir `EnableClientPrinting` y `False` por cualquier nombre y valor de propiedad válidos. Para obtener una lista completa de propiedades de servidor, vea [Report Server System Properties](../report-server-web-service/net-framework/reporting-services-properties-report-server-system-properties.md).  
  
 Para utilizar el script, guárdelo en un archivo con la extensión .rss y, a continuación, utilice la utilidad de símbolo del sistema rs.exe para ejecutar el archivo en el servidor de informes. El script no está compilado, por lo que no es necesario tener instalado [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]. En este ejemplo se da por supuesto que tiene permisos en el equipo local que hospeda el servidor de informes. Si no ha iniciado una sesión con una cuenta con permisos, debe especificar la información de la cuenta mediante argumentos adicionales de la línea de comandos. Para más información, vea [Utilidad RS.exe &#40;SSRS&#41;](rs-exe-utility-ssrs.md).  
  
> [!TIP]  
>  Para obtener un ejemplo detallado, vea [Sample Reporting Services rs.exe Script to Migrate Content between Report Servers](sample-reporting-services-rs-exe-script-to-copy-content-between-report-servers.md).  
  
```vb
Public Sub Main()  
        Dim props(0) As [Property]  
        Dim setProp As New [Property]  
        setProp.Name = "EnableClientPrinting"  
        setProp.Value = "False"   
        props(0) = setProp  
        Try  
            rs.SetSystemProperties(props)  
        Catch ex As System.Web.Services.Protocols.SoapException  
            Console.Write(ex.Detail.InnerXml)  
        Catch e as Exception  
            Console.Write(e.Message)  
        End Try  
End Sub  
```  
  
## <a name="see-also"></a>Ver también  
 [Método GenerateDatabaseCreationScript &#40;MSReportServer_ConfigurationSetting de WMI&#41;](../wmi-provider-library-reference/configurationsetting-method-generatedatabasecreationscript.md)   
 [Método GenerateDatabaseRightsScript &#40;MSReportServer_ConfigurationSetting de WMI&#41;](../wmi-provider-library-reference/configurationsetting-method-generatedatabaserightsscript.md)   
 [Método GenerateDatabaseUpgradeScript &#40;MSReportServer_ConfigurationSetting de WMI&#41;](../wmi-provider-library-reference/configurationsetting-method-generatedatabaseupgradescript.md)   
 [Instale SQL Server 2014 desde el símbolo del sistema](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)    
 [Instalar el servidor de informes en modo nativo de Reporting Services](../install-windows/install-reporting-services-native-mode-report-server.md)   
 [Servidor de informes de Reporting Services &#40;modo nativo&#41;](../report-server/reporting-services-report-server-native-mode.md)   
 [Utilidades del símbolo del sistema del servidor de informes &#40;SSRS&#41;](report-server-command-prompt-utilities-ssrs.md)   
 [Planeación de la compatibilidad &#40;con exploradores de&#41; Reporting Services y Power View Reporting Services 2014](../browser-support-for-reporting-services-and-power-view.md)    
 [Herramientas de Reporting Services](reporting-services-tools.md)  
