---
title: Modificar un archivo de configuración de Reporting Services (RSreportserver.config) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 958ef51f-2699-4cb2-a92e-3b4322e36a30
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: daf92c429e8d223f29a0d0d27f4ba6afca66d905
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63191155"
---
# <a name="modify-a-reporting-services-configuration-file-rsreportserverconfig"></a>Modificar un archivo de configuración de Reporting Services (RSreportserver.config)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] almacena la configuración de la aplicación en un conjunto de archivos de configuración. La instalación crea los archivos de configuración para cada instancia del servidor de informes que instala. Dentro de cada archivo, los valores se establecen durante la instalación o al usar herramientas y aplicaciones para configurar un servidor para la operación. En algunos casos, debe modificar directamente un archivo para agregar o configurar la configuración avanzada. Los parámetros de configuración se especifican como atributos o elementos XML. Si comprende XML y los archivos de configuración, puede utilizar un editor de texto o de código para modificar las opciones de configuración definibles por el usuario.  
  
 Algunos valores de configuración solo se pueden establecer a través de una herramienta. La configuración que contiene valores cifrados se debe modificar a través de la herramienta de configuración de Reporting Services, el programa de instalación o la utilidad de línea de comandos **rsconfig** . Debe ser miembro del grupo local de administradores para ejecutar estas herramientas.  
  
> [!IMPORTANT]  
>  Tenga cuidado al modificar los archivos de configuración. Si modifica un parámetro reservado para uso interno, es posible que deshabilite la instalación. En general, no se recomienda modificar los parámetros de configuración a no ser que esté intentando resolver un problema específico. Para obtener más información sobre qué valores de configuración se pueden cambiar con seguridad, vea [RSReportServer Configuration File](rsreportserver-config-configuration-file.md) o [RSReportDesigner Configuration File](rsreportdesigner-configuration-file.md). Para más información sobre los archivos de configuración, consulte la documentación del producto de [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] .  
  
 En este tema:  
  
-   [Leer y usar valores de configuración](#bkmk_read_values)  
  
-   [Sobre los valores predeterminados](#bkmk_default_values)  
  
-   [Eliminar los parámetros de configuración](#bkmk_delete_config_settings)  
  
-   [Para editar un archivo de configuración de Reporting Services](#bkmk_edit_configuation_file)  
  
##  <a name="bkmk_read_values"></a> Leer y usar valores de configuración  
 Un servidor de informes lee los archivos de configuración cuando se inicia el servicio y siempre que se guarda el archivo de configuración. Los valores nuevos y revisados surten efecto en un nuevo dominio de aplicación cuando expira el dominio de aplicación actual. Siempre que es posible, se permite que se completen las solicitudes que todavía se están procesando en el dominio de aplicación actual. Sin embargo, algunos valores requieren una operación inmediata de reciclaje de dominio de aplicación. En este caso, todas las solicitudes que se encuentran en proceso se reinician en un nuevo dominio de aplicación.  
  
 Si el servidor de informes detecta un valor no válido, registra un error en el registro de aplicación Windows y, o bien no puede iniciarse, o bien usa un valor predeterminado, dependiendo del error:  
  
-   Si el error se debe a XML con formato incorrecto, el servidor de informes no se iniciará. Si el servidor de informes se está ejecutando cuando se incluye el error, pasará por alto el archivo de configuración no válido hasta que se reinicie o hasta que el dominio de aplicación se recicle. Una vez detectado el error, no se iniciará el servidor de informes.  
  
-   Si el error es un valor de configuración no válido, el servidor usará valores predeterminados internos y registrará un error en los archivos de registro de seguimiento. En los pocos casos en los que los valores predeterminados internos no estén disponibles, el servidor devolverá el error rsServerConfigurationError si el valor de configuración no válido es vital para las operaciones del servidor. Los errores en los que se indica que la configuración crítica no es válida o que falta, se devuelven a la aplicación cliente en una página de error HTML y se anotan en el registro de eventos.  
  
 Todos los cambios del archivo de configuración, incluidos los cambios correctos, se registran en el archivo de registro de seguimiento del servidor de informes. Solo los errores se registran en el registro de eventos de la aplicación.  
  
##  <a name="bkmk_default_values"></a> Sobre los valores predeterminados  
 La mayoría de los valores de configuración tienen valores predeterminados especificados internamente en el servidor de informes. El servidor de informes usará estos valores si un valor definido por el usuario no es válido o no está especificado. Si hay que usar un valor predeterminado debido a un valor de configuración no válido, se escribe un error en el archivo de registro de seguimiento.  
  
##  <a name="bkmk_delete_config_settings"></a> Eliminar los parámetros de configuración  
 Quitar del archivo de configuración las opciones de configuración con valores predeterminados no tiene ningún efecto. La mayor parte de las opciones de configuración en realidad se definen y se configuran internamente. Si elimina un elemento del archivo de configuración, la copia interna todavía está disponible y se utiliza el valor predeterminado que se define para él.  
  
##  <a name="bkmk_edit_configuation_file"></a> Para editar un archivo de configuración de Reporting Services  
  
1.  Busque el archivo de configuración que desea editar:  
  
    -   **RSReportServer.config** se encuentra en la siguiente carpeta:  
  
        ```  
        C:\Program Files\Microsoft SQL Server\MSRS11.MSSQLSERVER\Reporting Services\ReportServer  
        ```  
  
    -   **RSReportServerServices.exe.config** se encuentra en la siguiente carpeta:  
  
        ```  
        C:\Program Files\Microsoft SQL Server\MSRS11.MSSQLSERVER\Reporting Services\ReportServer\bin  
        ```  
  
    -   **RSReportDesigner.config** se encuentra en la siguiente carpeta:  
  
        ```  
        C:\Program Files\Microsoft Visual Studio 10.0\Common7\IDE\PrivateAssemblies  
        ```  
  
2.  Guarde una copia del archivo en caso de que necesite revertir sus cambios.  
  
3.  Abra el archivo original en el Bloc de notas o en un editor de código. No use Textpad; establece la longitud del archivo antes guardarlo, lo que hace que se escriba un error de carácter no válido en el archivo de registro de seguimiento.  
  
4.  Escriba el elemento o valor que desea agregar o usar. Los elementos distinguen entre mayúsculas y minúsculas. Si va a agregar un elemento, asegúrese de que usa las mayúsculas y minúsculas correctas. Dispone de instrucciones concretas para editar archivos de configuración a la hora de personalizar extensiones de representación, de autenticación o de procesamiento de datos:  
  
    -   [Autenticación con el servidor de informes](../security/authentication-with-the-report-server.md)  
  
    -   [Configurar el Administrador de informes para pasar cookies de autenticación personalizadas](../security/configure-the-web-portal-to-pass-custom-authentication-cookies.md)  
  
    -   [Personalización de los parámetros de extensión de representación en RSReportServer.Config](../customize-rendering-extension-parameters-in-rsreportserver-config.md)  
  
5.  Guarde el archivo.  
  
6.  Compruebe los archivos de registro de seguimiento para ver que no se produjeron errores. Si observa condiciones de error es porque una opción de configuración o su valor se especificó incorrectamente. Examine el [RSReportServer Configuration File](rsreportserver-config-configuration-file.md) para ver los valores válidos para cualquier configuración que esté produciendo un error. Para obtener más información sobre cómo ver el registro de seguimiento, vea [Registro de seguimiento del servicio del servidor de informes](report-server-service-trace-log.md).  
  
## <a name="see-also"></a>Vea también  
 [Archivo de configuración RSReportServer](rsreportserver-config-configuration-file.md)   
 [Archivo de configuración ReportingServicesService](reportingservicesservice-configuration-file.md)   
 [Archivo de configuración RSReportDesigner](rsreportdesigner-configuration-file.md)   
 [Implementar una extensión de procesamiento de datos](../extensions/data-processing/deploying-a-data-processing-extension.md)   
 [Implementación de una extensión de entrega](../extensions/delivery-extension/deploying-a-delivery-extension.md)   
 [Implementación de una extensión de representación](../extensions/rendering-extension/deploying-a-rendering-extension.md)   
 [Cómo: Implementar un elemento de informe personalizado](../custom-report-items/how-to-deploy-a-custom-report-item.md)   
 [Archivos de configuración de Reporting Services](reporting-services-configuration-files.md)  
  
  
