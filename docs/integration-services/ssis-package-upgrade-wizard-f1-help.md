---
title: Ayuda F1 del Asistente para actualización del paquete SSIS | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
f1_keywords:
- sql13.is.upgradewizard.ssisupgradewizard.f1
- sql13.is.upgradewizard.selectsourcelocation.f1
- sql13.is.upgradewizard.selectdestinationlocation.f1
- sql13.is.upgradewizard.selectpackagemgtoptions.f1
- sql13.is.upgradewizard.selectpackages.f1
- sql13.is.upgradewizard.completewizard.f1
- sql13.is.upgradewizard.upgradingpackage.f1
ms.assetid: 7fe886ff-1ea5-48d5-9d20-d5da36dd1cd7
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b19b574a61ad5667d6617b68b8472589a2328bb1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65717838"
---
# <a name="ssis-package-upgrade-wizard-f1-help"></a>Ayuda F1 del Asistente para actualización del paquete SSIS

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Utilice el Asistente para actualizar paquetes de SSIS si quiere actualizar paquetes creados con versiones anteriores de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] al formato de paquete para la versión actual de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  
  
 **Para ejecutar el Asistente para actualización del paquete SSIS**  
  
-   [Actualizar paquetes de Integration Services mediante el Asistente para actualizar paquetes SSIS](../integration-services/install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md)  

## <a name="ssis-upgrade-wizard"></a>Asistente para actualización de SSIS
  
### <a name="options"></a>Opciones  
 **No volver a mostrar esta página.**  
 Omite la página de bienvenida la próxima vez que abre el asistente.  
 
## <a name="select-source-location-page"></a>Página Seleccionar ubicación de origen
 Utilice la página **Seleccionar ubicación de origen** para especificar el origen desde el que se actualizan los paquetes.  
  
> [!NOTE]  
>  Esta página solo está disponible cuando se ejecuta el Asistente para actualizar paquetes [!INCLUDE[ssIS](../includes/ssis-md.md)] desde [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] o en el símbolo del sistema.  
  
### <a name="static-options"></a>Opciones estáticas  
 **Origen del paquete**  
 Seleccione la ubicación de almacenamiento que contiene los paquetes que se van a actualizar. Esta opción tiene los valores que figuran en la siguiente tabla.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**Sistema de archivos**|Indica que los paquetes que se van a actualizar están en una carpeta en el equipo local.<br /><br /> Para hacer que el asistente realice una copia de seguridad de los paquetes originales antes de actualizarlos, estos deben estar almacenados en el sistema de archivos. Para obtener más información, vea el tema de procedimientos.|  
|**Almacén de paquetes SSIS**|Indica que los paquetes que se van a actualizar están en el almacén de paquetes. El almacén de paquetes consta del conjunto de carpetas del sistema de archivos que el servicio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] administra. Para obtener más información, vea [Administración de paquetes &#40;servicio SSIS&#41;](../integration-services/service/package-management-ssis-service.md).<br /><br /> Al seleccionar este valor, se muestran las opciones dinámicas de **Origen del paquete** correspondientes.|  
|**Microsoft SQL Server**|Indica que los paquetes que se van a actualizar son de una instancia existente de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].<br /><br /> Al seleccionar este valor, se muestran las opciones dinámicas de **Origen del paquete** correspondientes.|  
  
 **Carpeta**  
 Escriba el nombre de una carpeta que contenga los paquetes que quiere actualizar o haga clic en **Examinar** y busque la carpeta.  
  
 **Examinar**  
 Busque la carpeta que contiene los paquetes que desea actualizar.  
  
### <a name="package-source-dynamic-options"></a>Opciones dinámicas de Origen del paquete  
  
#### <a name="package-source--ssis-package-store"></a>Origen del paquete = Almacén de paquetes SSIS  
 **Server**  
 Escriba el nombre del servidor que tiene los paquetes que se van a actualizar o seleccione este servidor en la lista.  
  
#### <a name="package-source--microsoft-sql-server"></a>Origen del paquete = Microsoft SQL Server  
 **Server**  
 Escriba el nombre del servidor que tiene los paquetes que se van a actualizar o seleccione este servidor en la lista.  
  
 **Usar la autenticación de Windows**  
 Seleccione esta opción para utilizar la autenticación de Windows para conectarse al servidor.  
  
 **Utilizar autenticación de SQL Server**  
 Seleccione esta opción para usar la autenticación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para conectarse al servidor. Si usa la autenticación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , debe proporcionar un nombre de usuario y una contraseña.  
  
 **User name**  
 Escriba el nombre de usuario que la autenticación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usará para conectarse al servidor.  
  
 **Contraseña**  
 Escriba la contraseña que la autenticación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usará para conectarse al servidor.  
 
## <a name="select-destination-location-page"></a>Página Seleccionar ubicación de destino
 Utilice la página **Seleccionar ubicación de destino** para especificar el destino en el que desee guardar los paquetes actualizados.  
  
> [!NOTE]  
>  Esta página solo está disponible cuando se ejecuta el Asistente para actualizar paquetes [!INCLUDE[ssIS](../includes/ssis-md.md)] desde [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] o en el símbolo del sistema.  
 
### <a name="static-options"></a>Opciones estáticas  
 **Guardar en ubicación de origen**  
 Guarde los paquetes actualizados en la misma ubicación que la especificada en la página **Seleccionar ubicación de origen** del asistente.  
  
 Si los paquetes originales se almacenan en el sistema de archivos y desea que el asistente realice la copia de seguridad de esos paquetes, seleccione la opción **Guardar en ubicación de origen** . Para más información, vea [Actualizar paquetes de Integration Services mediante el Asistente para actualizar paquetes SSIS](../integration-services/install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md).  
  
 **Seleccionar nueva ubicación de destino**  
 Guarde los paquetes actualizados en la ubicación de destino que se especifica en esta página.  
  
 **Origen del paquete**  
 Especifique dónde se van a almacenar los paquetes de actualización. Esta opción tiene los valores que figuran en la siguiente tabla.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**Sistema de archivos**|Indica que los paquetes actualizados se van a guardar en una carpeta en el equipo local.|  
|**Almacén de paquetes SSIS**|Indica que los paquetes actualizados se van a guardar en el almacén de paquetes de Integration Services. El almacén de paquetes consta del conjunto de carpetas del sistema de archivos que el servicio Integration Services administra. Para más información, vea [Administración de paquetes &#40;servicio SSIS&#41;](../integration-services/service/package-management-ssis-service.md).<br /><br /> Al seleccionar este valor, se muestran las opciones dinámicas correspondientes de **Origen del paquete** .|  
|**Microsoft SQL Server**|Indica que los paquetes actualizados se guardarán en una instancia existente de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].<br /><br /> Al seleccionar este valor, se muestran las opciones dinámicas correspondientes de **Origen del paquete** .|  
  
 **Carpeta**  
 Escriba el nombre de una carpeta en la que se guardarán los paquetes actualizados, o bien haga clic en **Examinar** y busque la carpeta.  
  
 **Examinar**  
 Busque la carpeta en la que se guardarán los paquetes actualizados.  
  
### <a name="package-source-dynamic-options"></a>Opciones dinámicas de Origen del paquete  
  
#### <a name="package-source--ssis-package-store"></a>Origen del paquete = Almacén de paquetes SSIS  
 **Server**  
 Escriba el nombre del servidor en el que se guardarán los paquetes de la actualización, o seleccione un servidor en la lista.  
  
#### <a name="package-source--microsoft-sql-server"></a>Origen del paquete = Microsoft SQL Server  
 **Server**  
 Escriba el nombre del servidor en el que se guardarán los paquetes de la actualización, o seleccione este servidor en la lista.  
  
 **Usar la autenticación de Windows**  
 Seleccione esta opción para utilizar la autenticación de Windows para conectarse al servidor.  
  
 **Utilizar autenticación de SQL Server**  
 Seleccione esta opción para usar la autenticación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para conectarse al servidor. Si usa la autenticación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , debe proporcionar un nombre de usuario y una contraseña.  
  
 **User name**  
 Escriba el nombre de usuario que se usará con la autenticación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para conectarse al servidor.  
  
 **Contraseña**  
 Escriba la contraseña que se usará con la autenticación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para conectarse al servidor.  
 
## <a name="select-package-management-options-page"></a>Página Seleccionar opciones de Administración de paquetes
  Utilice la página **Seleccionar opciones de administración de paquetes** con el fin de especificar las opciones para actualizar paquetes.  
  
 **Para ejecutar el Asistente para actualización del paquete SSIS**  
  
-   [Actualizar paquetes de Integration Services mediante el Asistente para actualizar paquetes SSIS](../integration-services/install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md)  
  
### <a name="options"></a>Opciones  
 **Actualizar las cadenas de conexión para reflejar los nuevos nombres de proveedor**  
 Se actualizan las cadenas de conexión para que usen los nombres de los proveedores siguientes para la versión actual de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]:  
  
-   Proveedor OLE DB para [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client  
  
 El Asistente para actualizar paquetes de [!INCLUDE[ssIS](../includes/ssis-md.md)] solo actualiza las cadenas de conexión que se almacenan en administradores de conexiones. No actualiza las cadenas de conexión que se construyen dinámicamente utilizando el lenguaje de expresiones de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] o código en una tarea Script.  
  
 **Validar los paquetes de actualización**  
 Se validan los paquetes de actualización y se guardan solo aquéllos que superan la validación.  
  
 Si no selecciona esta opción, el asistente no validará los paquetes de actualización. Por consiguiente, el asistente guardará todos los paquetes de actualización, sin tener en cuenta si son válidos o no. El asistente guarda los paquetes de actualización en el destino que se especifica en la página **Seleccionar ubicación de destino** del asistente.  
  
 La validación agrega tiempo al proceso de actualización. Se recomienda no seleccionar esta opción con paquetes grandes que probablemente se actualizarán correctamente.  
  
 **Crear nuevo id. de paquete**  
 Se crean nuevos identificadores de paquete para los paquetes de actualización.  
  
 **Continuar el proceso de actualización cuando la actualización de un paquete genera un error**  
 Se especifica que cuando un paquete no se pueda actualizar, el Asistente para actualizar paquetes [!INCLUDE[ssIS](../includes/ssis-md.md)] continúe actualizando el resto de los paquetes.  
  
 **Conflictos con nombres de paquete**  
 Se especifica cómo debe administrar el asistente los paquetes que tienen el mismo nombre. Esta opción tiene los valores que figuran en la siguiente tabla.  
  
 **Sobrescribir archivos de paquete existentes**  
 Se reemplaza el paquete existente por el paquete de actualización del mismo nombre.  
  
 **Agregar sufijos numéricos para actualizar nombres de paquete**  
 Se agrega un sufijo numérico al nombre del paquete de actualización.  
  
 **No actualizar paquetes**  
 Se detiene la actualización de los paquetes y se muestra un error cuando se completa el asistente.  
  
 Estas opciones no están disponibles cuando se selecciona la opción **Guardar en ubicación de origen** en la página **Seleccionar ubicación de destino** del asistente.  
  
 **Omitir configuraciones**  
 No carga configuraciones de paquetes durante la actualización del paquete. Si se selecciona esta opción se reduce el tiempo necesario para actualizar el paquete.  
  
 **Realizar copia de seguridad de paquetes originales**  
 El asistente hace una copia de seguridad de los paquetes originales en una carpeta **SSISBackupFolder** . El asistente crea la carpeta **SSISBackupFolder** como una subcarpeta de la carpeta que contiene los paquetes originales y los paquetes actualizados.  
  
> [!NOTE]  
>  Esta opción solo está disponible cuando se especifica que los paquetes originales y los paquetes actualizados se almacenen en el sistema de archivos y en la misma carpeta.  

## <a name="select-packages-page"></a>Página Seleccionar paquetes
  Utilice la página **Seleccionar paquetes** para seleccionar los paquetes que se van a actualizar. Esta página enumera los paquetes que se almacenan en la ubicación que se especificó en la página **Seleccionar ubicación de origen** del asistente.  
  
### <a name="options"></a>Opciones  
 **Nombre del paquete existente**  
 Seleccione uno o varios paquetes para actualizar.  
  
 **Actualizar nombre de paquete**  
 Proporcione el nombre del paquete de destino o use el nombre predeterminado que proporciona el asistente.  
  
> [!NOTE]  
>  También puede cambiar el nombre del paquete de destino después de actualizar el paquete. En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], abra el paquete actualizado y cambie el nombre del mismo.  
  
 **Contraseña**  
 Especifique la contraseña que se utiliza para descifrar los paquetes de actualización seleccionados.  
  
 **Aplicar a la selección**  
 Aplique la contraseña especificada para descifrar los paquetes de la actualización seleccionados.  
 
## <a name="complete-the-wizard-page"></a>Página Finalización del asistente
  Utilice la página **Finalización del asistente** para revisar y confirmar las opciones de actualización del paquete que ha seleccionado. Ésta es la última página del asistente desde la que puede volver y cambiar las opciones de esta sesión del asistente.  
  
### <a name="options"></a>Opciones  
 **Resumen de opciones**  
 Revise las opciones de actualización que ha seleccionado en el asistente. Para cambiar alguna opción, haga clic en **Atrás** para volver a las páginas anteriores del asistente.
 
## <a name="upgrading-the-packages-page"></a>Página Actualizando los paquetes
  Utilice la página **Actualizando los paquetes** para ver e interrumpir el progreso de la actualización de paquetes. El Asistente para actualización del paquete [!INCLUDE[ssIS](../includes/ssis-md.md)] actualiza los paquetes seleccionados uno a uno.  
  
### <a name="options"></a>Opciones  
 **Panel Mensaje**  
 Muestra mensajes de progreso e información de resumen durante el proceso de actualización.  
  
 **Acción**  
 Vea las acciones de la actualización.  
  
 **Estado**  
 Vea el resultado de cada acción.  
  
 **de mensaje**  
 Vea los mensajes de error generados por cada acción.  
  
 **Detener**  
 Detenga la actualización del paquete.  
  
 **Informe**  
 Seleccione lo que desea hacer con el informe que contiene los resultados de la actualización del paquete:  
  
-   Ver el informe en línea.  
  
-   Guardar el informe en un archivo.  
  
-   Copiar el informe en el Portapapeles.  
  
-   Enviar el informe como un mensaje de correo electrónico.  

## <a name="view-upgraded-packages"></a>Visualización de los paquetes actualizados
### <a name="view-upgraded-packages-that-were-saved-to-a-sql-server-database-or-to-the-package-store"></a>Visualización de los paquetes actualizados que se guardaron en una base de datos de SQL Server o en el almacén de paquetes
  
En [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)], en el Explorador de objetos, conéctese a la instancia local de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]y, a continuación, expanda el nodo **Paquetes almacenados** para ver los paquetes que se actualizaron.  
  
### <a name="view-upgraded-packages-that-were-upgraded-from-sql-server-data-tools"></a>Visualización de los paquetes que se actualizaron a partir de SQL Server Data Tools  
  
En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], en el Explorador de soluciones, abra el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] y, a continuación, expanda el nodo **Paquetes SSIS** para ver los paquetes actualizados.  
  
## <a name="see-also"></a>Consulte también  
 [Actualizar paquetes de Integration Services](../integration-services/install-windows/upgrade-integration-services-packages.md)  
  
  
