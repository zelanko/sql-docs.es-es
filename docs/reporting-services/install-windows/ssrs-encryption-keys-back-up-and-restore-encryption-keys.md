---
title: Copia de seguridad y restauración de claves de cifrado de Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 05/31/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.component: install-windows
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- backing up encryption keys [Reporting Services]
- restoring encryption keys [Reporting Services]
- encryption keys [Reporting Services]
- symmetric keys [Reporting Services]
ms.assetid: 6773d5df-03ef-4781-beb7-9f6825bac979
caps.latest.revision: 14
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 980774dac04aabe5704d27b23ec789f02ace0136
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="ssrs-encryption-keys---back-up-and-restore-encryption-keys"></a>Claves de cifrado de SSRS: copia de seguridad y restauración de claves de cifrado
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Una parte importante de la configuración del servidor de informes es la creación de una copia de seguridad de la clave simétrica utilizada para cifrar información confidencial. La copia de seguridad de la clave se necesita para varias operaciones rutinarias y, además, permite volver a utilizar una base de datos del servidor de informes existente en una nueva instalación.  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]** Modo nativo de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] | Modo de SharePoint de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
 Es necesario restaurar la copia de seguridad de la clave de cifrado cuando se produce alguno de los siguientes eventos:  
  
-   Cambio de nombre de la cuenta de servicio de Windows del servidor de informes o restablecimiento de la contraseña. Cuando se usa el Administrador de configuración de Reporting Services, la creación de una copia de seguridad de la clave forma parte de la operación de cambio del nombre de la cuenta de servicio.  
  
    > [!NOTE]
    > Restablecer la contraseña no es lo mismo que cambiarla. Para restablecer una contraseña se requiere permiso para sobrescribir la información de cuenta en el controlador de dominio. El administrador del sistema es quien restablece una contraseña cuando el usuario la olvida o no conoce una contraseña determinada. Solo los restablecimientos de contraseña requieren la restauración de la clave simétrica. El cambio que se realiza periódicamente de una contraseña de cuenta no requiere que se restablezca la clave simétrica.  
  
-   Cambio de nombre del equipo o de la instancia que hospeda al servidor de informes (una instancia del servidor de informes se basa en un nombre de instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ).  
  
-   Migración de una instalación del servidor de informes o configuración de un servidor de informes para utilizar una base de datos del servidor de informes diferente.  
  
-   Recuperación de una instalación del servidor de informes debido a un error de hardware.  
  
 Solo es necesario realizar una copia de seguridad de la clave simétrica. Hay una correspondencia de uno a uno entre una base de datos del servidor de informes y una clave simétrica. Si bien solo debe realizar una copia de seguridad, es posible que necesite restaurar la clave varias veces cuando ejecute varios servidores de informes en un modelo de implementación escalada. Cada instancia del servidor de informes deberá tener su copia de la clave simétrica para bloquear y desbloquear datos en la base de datos del servidor de informes.

 La copia de seguridad de la clave simétrica es un proceso que escribe la clave en el archivo que se especifique y después la codifica mediante la contraseña que se proporcione. La clave simétrica no puede almacenarse nunca en un estado no cifrado, por lo que debe proporcionar una contraseña para cifrarla cuando la guarde en disco. Una vez creado el archivo, debe almacenarlo en una ubicación segura **y recordar la contraseña** que se usa para desbloquearlo. Para hacer copia de seguridad de la clave simétrica, puede usar las siguientes herramientas:  
  
 **Modo nativo** : el Administrador de configuración de Reporting Services o la utilidad **rskeymgmt** .  
  
 **Modo de SharePoint** : páginas de Administración central de SharePoint o PowerShell.  
  
##  <a name="bkmk_backup_sharepoint"></a> Hacer copia de seguridad de servidores de informes en modo de SharePoint  
 Para los servidores de informes en modo de SharePoint puede usar comandos de PowerShell o usar las páginas de administración para la aplicación de servicios de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para obtener más información, vea la sección "Administración de claves" de [Administrar una aplicación de servicio de SharePoint para Reporting Services](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md).  
  
##  <a name="bkmk_backup_configuration_manager"></a> Hacer copia de seguridad de las claves de cifrado - Administrador de configuración de Reporting Services (modo nativo)  
  
1.  Inicie el Administrador de configuración de Reporting Services y, a continuación, conéctese a la instancia del servidor de informes que desea configurar.  
  
2.  Haga clic en **Claves de cifrado**y, luego, seleccione **Copia de seguridad**.  
  
3.  Escriba una contraseña segura.  
  
4.  Especifique un archivo para incluir la clave almacenada. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] anexa una extensión de archivo .snk al archivo. Considere la posibilidad de almacenar el archivo en un disco diferente del servidor de informes.  
  
5.  Seleccione **Aceptar**.  
  
###  <a name="bkmk_backup_rskeymgmt"></a> Hacer copia de seguridad de las claves de cifrado - rskeymgmt (modo nativo)  
  
1.  Ejecute **rskeymgmt.exe** localmente en el equipo que hospeda el servidor de informes. Debe usar el argumento de extracción **-e** para copiar la clave, dar un nombre de archivo y especificar una contraseña. El siguiente ejemplo ilustra los argumentos que debe especificar:  
  
    ```  
    rskeymgmt -e -f d:\rsdbkey.snk -p<password>  
    ```  
  
## <a name="restore-encryption-keys"></a>Restaurar las claves de cifrado  
 La restauración de la clave de cifrado sobrescribe la clave simétrica existente que se almacena en la base de datos del servidor de informes. La restauración de una clave de cifrado reemplaza una clave que no se puede utilizar con una copia que se guardó anteriormente en el disco. La restauración de claves de cifrado se traduce en las siguientes acciones:  
  
-   Se abre la clave simétrica desde el archivo de copia de seguridad protegido mediante contraseña.  
  
-   Se cifra la clave simétrica mediante la clave pública del servicio de Windows del servidor de informes.  
  
-   Se almacena la clave simétrica cifrada en la base de datos del servidor de informes.  
  
-   Se eliminan los datos de la clave simétrica anteriormente almacenada (por ejemplo, la información de la clave que se encontraba en la base de datos del servidor de informes desde una implementación anterior).  
  
 Para restaurar la clave de cifrado, debe tener una copia de la clave de cifrado en el archivo. También debe conocer la contraseña que desbloquea la copia almacenada. Si conoce la clave y la contraseña, puede ejecutar la herramienta de configuración de Reporting Services o la utilidad **rskeymgmt** para restaurar la clave. La clave simétrica debe ser la misma que bloquea y desbloquea los datos cifrados almacenados actualmente en la base de datos del servidor de informes. Si restaura una copia que no es válida, el servidor de informes no puede obtener acceso a los datos cifrados almacenados actualmente en la base de datos del servidor de informes. Si esto sucede, es posible que deba eliminar todos los valores cifrados cuando no pueda restaurar una clave válida. Si por algún motivo no puede restaurar la clave de cifrado (por ejemplo, si no tiene una copia de seguridad), debe eliminar la clave existente y el contenido cifrado. Para más información, vea [Claves de cifrado de SSRS: eliminar y volver a crear las claves de cifrado](../../reporting-services/install-windows/ssrs-encryption-keys-delete-and-re-create-encryption-keys.md). Para obtener más información sobre la creación de claves simétrica, vea [Inicializar un servidor de informes &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md).  
  
###  <a name="bkmk_restore_configuration_manager"></a> Restaurar las claves de cifrado - Administrador de configuración de Reporting Services (modo nativo)  
  
1.  Inicie el Administrador de configuración de Reporting Services y, a continuación, conéctese a la instancia del servidor de informes que desea configurar.  
  
2.  En la página Claves de cifrado, seleccione **Restaurar**.  
  
3.  Seleccione el archivo .snk que contiene la copia de seguridad.  
  
4.  Escriba la contraseña que desbloquea el archivo.  
  
5.  Seleccione **Aceptar**. 
  
###  <a name="bkmk_restore_rskeymgmt"></a> Restaurar las claves de cifrado - rskeymgmt (modo nativo)  
  
1.  Ejecute **rskeymgmt.exe** localmente en el equipo que hospeda el servidor de informes. Use el argumento **-a** para restaurar las claves. Debe proporcionar un nombre de archivo completo y especificar una contraseña. El siguiente ejemplo ilustra los argumentos que debe especificar:  
  
    ```  
    rskeymgmt -a -f d:\rsdbkey.snk -p<password>  
    ```  
  
## <a name="see-also"></a>Ver también  
 [Configurar y administrar claves de cifrado &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)  
  
  
