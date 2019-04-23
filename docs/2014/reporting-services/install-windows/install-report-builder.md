---
title: Instalar la versión independiente del generador de informes (generador de informes) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 6b2291bb-1d20-4d08-81cb-a16dd8e01faf
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 830854a26d3f9b05465ee37aac6a9b7584750fe2
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/22/2019
ms.locfileid: "59956531"
---
# <a name="install-the-stand-alone-version-of-report-builder-report-builder"></a>Instalar la versión independiente del Generador de informes (Generador de informes)
  Puede instalar el generador de informes desde el [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] feature pack de en el [Microsoft Download Center](https://go.microsoft.com/fwlink/?LinkID=168472) o una ubicación como la carpeta pública a la que tiene el ReportBuilder3_x86.msi, el paquete de Windows Installer para el generador de informes se ha descargado.  
  
 También puede realizar una instalación de línea de comandos del Generador de informes y especificar argumentos para personalizar la instalación. Además de los parámetros estándar intrínsecos de MSI, puede usar los parámetros personalizados que proporciona el generador de informes: RBINSTALLDIR y REPORTSERVERURL. RBINSTALLDIR especifica la carpeta de instalación raíz para el Generador de informes. REPORTSERVERURL especifica el servidor de informes predeterminado que usa el Generador de informes para guardar los informes en el servidor.  
  
 Si quiere realizar una instalación completamente silenciosa, sin ninguna interacción con la interfaz de usuario, especifique la opción **/quiet** . Por diseño, la marca de la opción quiet suprime los errores de instalación. Por lo tanto, es recomendable que, cuando use la opción quiet, incluya la opción **/l** que especifica el registro.  
  
> [!IMPORTANT]  
>  Las características de seguridad de Windows Vista y Windows 7 exigen permisos elevados para ejecutar operaciones de línea de comandos y solicitarán permiso para ejecutar la línea de comandos. La instalación no es silenciosa. Para que la instalación sea silenciosa, es necesario ejecutar la línea de comandos como administrador.  
  
### <a name="to-install-report-builder-from-the-download-site"></a>Instalar Generador de informes desde el sitio de descarga  
  
1.  Vaya a [generador de informes de Microsoft SQL Server 2012](https://go.microsoft.com/fwlink/?LinkID=219138) y busque la sección Generador de informes de la página Web.  
  
2.  Haga clic en **X86 paquete**.  
  
3.  En el **de descarga del archivo** cuadro de diálogo, haga clic en **ejecutar**.  
  
    > [!IMPORTANT]  
    >  Descargue solo archivos de fuentes de confianza.  
  
4.  En el cuadro de diálogo de Internet Explorer, haga clic en **ejecutar**.  
  
    > [!IMPORTANT]  
    >  Ejecute solo archivos de fuentes de confianza.  
  
5.  Se iniciará el Asistente del Generador de informes de Microsoft SQL Server.  
  
6.  En el **el Asistente para instalación** página, haga clic en **siguiente**.  
  
7.  En el **contrato de licencia** página, lea el contrato y, a continuación, seleccione el **acepto los términos del contrato de licencia** opción. Haga clic en **Siguiente**.  
  
8.  Especifique su nombre y el nombre de su compañía. Haga clic en **Siguiente**.  
  
9. En el **selección de características** , opcionalmente, haga clic en **examinar** o **espacio en disco**. Haga clic en **Siguiente**.  
  
    -   Haga clic en **examinar** para ver la ubicación predeterminada del generador de informes y actualizarla.  
  
        > [!NOTE]  
        >  La carpeta de instalación predeterminada para el generador de informes es \<unidad > archivos de programa\Microsoft SQL Server.  
  
    -   Haga clic en **espacio en disco** obtener información sobre el generador de informes cuánto espacio en disco consume.  
  
        > [!NOTE]  
        >  Si un volumen no tiene suficiente espacio disponible en disco, se muestra resaltado.  
  
10. En la página **Servidor de destino predeterminado** , puede especificar la dirección URL al servidor de informes de destino si difiere del valor predeterminado. Haga clic en **Siguiente**.  
  
    > [!NOTE]  
    >  Si tiene previsto trabajar con el Generador de informes cuando esté conectado a un servidor de informes, conviene que especifique en este momento la dirección URL al servidor. Sin embargo, también puede hacer esto desde el **opciones** cuadro de diálogo cuando se trabaja en el generador de informes.  
  
11. Haga clic en **instalar** para completar la instalación del generador de informes.  
  
### <a name="to-install-report-builder-from-a-share"></a>Instalar el Generador de informes desde un recurso compartido  
  
1.  Póngase en contacto con el administrador para obtener información sobre la ubicación del archivo ReportBuilder3_x86.msi.msi que necesitará ejecutar para instalar el Generador de informes en el equipo local.  
  
2.  Busque el archivo ReportBuilder3_x86.msi.msi, que es el paquete de Windows Installer (MSI) para el Generador de informes, y haga clic en él.  
  
     Se iniciará el Asistente del Generador de informes de Microsoft SQL Server.  
  
3.  En el **el Asistente para instalación** página, haga clic en **siguiente**.  
  
4.  En el **contrato de licencia** página, lea el contrato y, a continuación, seleccione el **acepto los términos del contrato de licencia** opción. Haga clic en **Siguiente**.  
  
5.  Especifique su nombre y el nombre de su compañía. Haga clic en **Siguiente**.  
  
6.  En el **selección de características** , opcionalmente, haga clic en **examinar** o **espacio en disco**. Haga clic en **Siguiente**.  
  
    -   Haga clic en **examinar** para ver la ubicación predeterminada del generador de informes y actualizarla.  
  
        > [!NOTE]  
        >  La carpeta de instalación predeterminada para el generador de informes es \<unidad > archivos de programa\Microsoft SQL Server.  
  
    -   Haga clic en **espacio en disco** obtener información sobre el generador de informes cuánto espacio en disco consume.  
  
        > [!NOTE]  
        >  Si un volumen no tiene suficiente espacio disponible en disco, se muestra resaltado.  
  
7.  En la página **Servidor de destino predeterminado** , puede especificar la dirección URL al servidor de informes de destino si difiere del valor predeterminado. Haga clic en **Siguiente**.  
  
    > [!NOTE]  
    >  Si tiene previsto trabajar con el Generador de informes cuando esté conectado a un servidor de informes, conviene que especifique en este momento la dirección URL al servidor. Sin embargo, también puede hacer esto desde el **opciones** cuadro de diálogo cuando se trabaja en el generador de informes.  
  
8.  Haga clic en **instalar** para completar la instalación del generador de informes.  
  
### <a name="to-install-report-builder-from-the-command-line"></a>Instalar el Generador de informes desde la línea de comandos  
  
1.  Vaya a [generador de informes de Microsoft SQL Server 2012](https://go.microsoft.com/fwlink/?LinkID=219138) y busque la sección Generador de informes.  
  
2.  Haga clic en **X86 paquete**.  
  
3.  Haga clic en Guardar.  
  
4.  Si lo desea, vaya a la ubicación para guardar, compruebe el **Guardar como** opción es **paquete de Windows Installer**y, a continuación, haga clic en **guardar**.  
  
5.  En el menú **Inicio** , haga clic en **Ejecutar**.  
  
6.  En el cuadro de texto Abrir, escriba `cmd.`  
  
7.  En la ventana del Símbolo del sistema, navegue hasta la carpeta en la que guardó ReportBuilder3_x86.msi.  
  
8.  Escriba un comando con el formato siguiente:  
  
     `msiexec/i ReportBuilder3_.msi /option [value] [/option [value]]`  
  
     Las dos opciones específicas a instalar el generador de informes son: RBINSTALLDIR y REPORTSERVERURL. No se requiere que incluya estos argumentos en la línea de comandos. El siguiente es el comando de línea base:  
  
     `msiexec /i ReportBuilder3_x86.msi /quiet`  
  
9. Para ejecutar el comando, presione ENTRAR.  
  
## <a name="see-also"></a>Vea también  
 [Instalar, desinstalar y asistencia del generador de informes](../install-uninstall-and-report-builder-support.md)   
 [Desinstalar la versión independiente del generador de informes &#40;generador de informes&#41;](install-report-builder.md)  
  
  
