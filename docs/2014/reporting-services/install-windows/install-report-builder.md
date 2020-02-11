---
title: Instalar la versión independiente de Generador de informes (Generador de informes) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 6b2291bb-1d20-4d08-81cb-a16dd8e01faf
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 60a96db6a7568c2af22242f10f96e7a2abf13937
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "73637830"
---
# <a name="install-the-stand-alone-version-of-report-builder-report-builder"></a>Instalar la versión independiente del Generador de informes (Generador de informes)
  Puede instalar Generador de informes desde el [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Feature Pack en el centro de descarga de [Microsoft](https://www.microsoft.com/download/details.aspx?id=53613) o en una ubicación como una carpeta pública en la que se haya descargado el paquete de Windows Installer ReportBuilder3_x86. msi para generador de informes.  
  
 También puede realizar una instalación de línea de comandos del Generador de informes y especificar argumentos para personalizar la instalación. Además de los parámetros estándar intrínsecos de MSI, puede usar los parámetros personalizados que proporciona el Generador de informes: RBINSTALLDIR y REPORTSERVERURL. RBINSTALLDIR especifica la carpeta de instalación raíz para el Generador de informes. REPORTSERVERURL especifica el servidor de informes predeterminado que usa el Generador de informes para guardar los informes en el servidor.  
  
 Si quiere realizar una instalación completamente silenciosa, sin ninguna interacción con la interfaz de usuario, especifique la opción **/quiet** . Por diseño, la marca de la opción quiet suprime los errores de instalación. Por lo tanto, es recomendable que, cuando use la opción quiet, incluya la opción **/l** que especifica el registro.  
  
> [!IMPORTANT]  
>  Las características de seguridad de Windows Vista y Windows 7 exigen permisos elevados para ejecutar operaciones de línea de comandos y solicitarán permiso para ejecutar la línea de comandos. La instalación no es silenciosa. Para que la instalación sea silenciosa, es necesario ejecutar la línea de comandos como administrador.  
  
### <a name="to-install-report-builder-from-the-download-site"></a>Instalar Generador de informes desde el sitio de descarga  
  
1.  Vaya a [Microsoft SQL Server 2012 generador de informes](https://go.microsoft.com/fwlink/?LinkID=219138) y busque la sección generador de informes de la Página Web.  
  
2.  Haga clic en **paquete x86**.  
  
3.  En el cuadro de diálogo **descarga de archivos** , haga clic en **Ejecutar**.  
  
    > [!IMPORTANT]  
    >  Descargue solo archivos de fuentes de confianza.  
  
4.  En el cuadro de diálogo Internet Explorer, haga clic en **Ejecutar**.  
  
    > [!IMPORTANT]  
    >  Ejecute solo archivos de fuentes de confianza.  
  
5.  Se iniciará el Asistente del Generador de informes de Microsoft SQL Server.  
  
6.  En la página **Bienvenido al Asistente para la instalación** , haga clic en **siguiente**.  
  
7.  En la página **contrato de licencia** , lea el contrato y, a continuación, seleccione la opción acepto **los términos del contrato de licencia** . Haga clic en **Next**.  
  
8.  Especifique su nombre y el nombre de su compañía. Haga clic en **Next**.  
  
9. En la página **selección de características** , puede hacer clic en **examinar** o en el costo del **disco**. Haga clic en **Next**.  
  
    -   Haga clic en **examinar** para ver la ubicación predeterminada de generador de informes y actualizarla.  
  
        > [!NOTE]  
        >  La carpeta de instalación predeterminada para Generador de informes \<es unidad>archivos de programa\Microsoft SQL Server.  
  
    -   Haga clic en **costo del disco** para obtener información sobre el espacio en disco que consume generador de informes.  
  
        > [!NOTE]  
        >  Si un volumen no tiene suficiente espacio disponible en disco, se muestra resaltado.  
  
10. En la página **Servidor de destino predeterminado** , puede especificar la dirección URL al servidor de informes de destino si difiere del valor predeterminado. Haga clic en **Next**.  
  
    > [!NOTE]  
    >  Si tiene previsto trabajar con el Generador de informes cuando esté conectado a un servidor de informes, conviene que especifique en este momento la dirección URL al servidor. Sin embargo, también puede hacerlo desde el cuadro de diálogo **Opciones** cuando esté trabajando en generador de informes.  
  
11. Haga clic en **instalar** para completar la instalación de generador de informes.  
  
### <a name="to-install-report-builder-from-a-share"></a>Instalar el Generador de informes desde un recurso compartido  
  
1.  Póngase en contacto con el administrador para obtener información sobre la ubicación del archivo ReportBuilder3_x86.msi.msi que necesitará ejecutar para instalar el Generador de informes en el equipo local.  
  
2.  Busque el archivo ReportBuilder3_x86.msi.msi, que es el paquete de Windows Installer (MSI) para el Generador de informes, y haga clic en él.  
  
     Se iniciará el Asistente del Generador de informes de Microsoft SQL Server.  
  
3.  En la página **Bienvenido al Asistente para la instalación** , haga clic en **siguiente**.  
  
4.  En la página **contrato de licencia** , lea el contrato y, a continuación, seleccione la opción acepto **los términos del contrato de licencia** . Haga clic en **Next**.  
  
5.  Especifique su nombre y el nombre de su compañía. Haga clic en **Next**.  
  
6.  En la página **selección de características** , puede hacer clic en **examinar** o en el costo del **disco**. Haga clic en **Next**.  
  
    -   Haga clic en **examinar** para ver la ubicación predeterminada de generador de informes y actualizarla.  
  
        > [!NOTE]  
        >  La carpeta de instalación predeterminada para Generador de informes \<es unidad>archivos de programa\Microsoft SQL Server.  
  
    -   Haga clic en **costo del disco** para obtener información sobre el espacio en disco que consume generador de informes.  
  
        > [!NOTE]  
        >  Si un volumen no tiene suficiente espacio disponible en disco, se muestra resaltado.  
  
7.  En la página **Servidor de destino predeterminado** , puede especificar la dirección URL al servidor de informes de destino si difiere del valor predeterminado. Haga clic en **Next**.  
  
    > [!NOTE]  
    >  Si tiene previsto trabajar con el Generador de informes cuando esté conectado a un servidor de informes, conviene que especifique en este momento la dirección URL al servidor. Sin embargo, también puede hacerlo desde el cuadro de diálogo **Opciones** cuando esté trabajando en generador de informes.  
  
8.  Haga clic en **instalar** para completar la instalación de generador de informes.  
  
### <a name="to-install-report-builder-from-the-command-line"></a>Instalar el Generador de informes desde la línea de comandos  
  
1.  Vaya a [Microsoft SQL Server 2012 generador de informes](https://go.microsoft.com/fwlink/?LinkID=219138) y busque la sección generador de informes.  
  
2.  Haga clic en **paquete x86**.  
  
3.  Haga clic en Guardar.  
  
4.  Opcionalmente, vaya a la ubicación en la que se va a guardar, compruebe que la opción **Guardar como** está **Windows Installer paquete**y, a continuación, haga clic en **Guardar**.  
  
5.  En el menú **Inicio** , haga clic en **Ejecutar**.  
  
6.  En el cuadro de texto Abrir, escriba `cmd.`  
  
7.  En la ventana del Símbolo del sistema, navegue hasta la carpeta en la que guardó ReportBuilder3_x86.msi.  
  
8.  Escriba un comando con el formato siguiente:  
  
     `msiexec/i ReportBuilder3_.msi /option [value] [/option [value]]`  
  
     Las dos opciones específicas para la instalación del Generador de informes son: RBINSTALLDIR y REPORTSERVERURL. No se requiere que incluya estos argumentos en la línea de comandos. El siguiente es el comando de línea base:  
  
     `msiexec /i ReportBuilder3_x86.msi /quiet`  
  
9. Para ejecutar el comando, presione ENTRAR.  
  
## <a name="see-also"></a>Consulte también  
 [Instalación, desinstalación y compatibilidad Generador de informes](../install-uninstall-and-report-builder-support.md)   
 [Desinstale la versión independiente de Generador de informes &#40;Generador de informes&#41;](install-report-builder.md)  
  
  
