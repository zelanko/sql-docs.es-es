---
title: Seleccionar ubicación de destino (Asistente para actualización del paquete SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.is.upgradewizard.selectdestinationlocation.f1
ms.assetid: 89274a71-0ffe-4889-84df-f5a7d78459ef
author: chugugrace
ms.author: chugu
ms.openlocfilehash: abe5be4a11e0f7db4f6e8078395aef0fbdf8d10a
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2020
ms.locfileid: "85422042"
---
# <a name="select-destination-location-ssis-package-upgrade-wizard"></a>Seleccionar ubicación de destino (Asistente para actualización del paquete SSIS)
  Utilice la página **Seleccionar ubicación de destino** para especificar el destino en el que desee guardar los paquetes actualizados.  
  
> [!NOTE]  
>  Esta página solo está disponible cuando se ejecuta el Asistente para actualizar paquetes [!INCLUDE[ssIS](../includes/ssis-md.md)] desde [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] o en el símbolo del sistema.  
  
 **Para ejecutar el Asistente para actualización del paquete SSIS**  
  
-   [Actualizar paquetes de Integration Services mediante el Asistente para actualizar paquetes SSIS](install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md)  
  
## <a name="static-options"></a>Opciones estáticas  
 **Guardar en ubicación de origen**  
 Guarde los paquetes actualizados en la misma ubicación que la especificada en la página **Seleccionar ubicación de origen** del asistente.  
  
 Si los paquetes originales se almacenan en el sistema de archivos y desea que el asistente realice la copia de seguridad de esos paquetes, seleccione la opción **Guardar en ubicación de origen** . Para más información, vea [Actualizar paquetes de Integration Services mediante el Asistente para actualizar paquetes SSIS](install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md).  
  
 **Seleccionar nueva ubicación de destino**  
 Guarde los paquetes actualizados en la ubicación de destino que se especifica en esta página.  
  
 **Origen del paquete**  
 Especifique dónde se van a almacenar los paquetes de actualización. Esta opción tiene los valores que figuran en la siguiente tabla.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**Sistema de archivos**|Indica que los paquetes actualizados se van a guardar en una carpeta en el equipo local.|  
|**Almacén de paquetes SSIS**|Indica que los paquetes actualizados se van a guardar en el almacén de paquetes de Integration Services. El almacén de paquetes consta del conjunto de carpetas del sistema de archivos que el servicio Integration Services administra. Para obtener más información, vea [Administración de paquetes &#40;servicio SSIS&#41;](service/package-management-ssis-service.md).<br /><br /> Al seleccionar este valor, se muestran las opciones dinámicas correspondientes de **Origen del paquete** .|  
|**Microsoft SQL Server**|Indica que los paquetes actualizados se guardarán en una instancia existente de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].<br /><br /> Al seleccionar este valor, se muestran las opciones dinámicas correspondientes de **Origen del paquete** .|  
  
 **Carpeta**  
 Escriba el nombre de una carpeta en la que se guardarán los paquetes actualizados, o bien haga clic en **Examinar** y busque la carpeta.  
  
 **Examinar**  
 Busque la carpeta en la que se guardarán los paquetes actualizados.  
  
## <a name="package-source-dynamic-options"></a>Opciones dinámicas de Origen del paquete  
  
### <a name="package-source--ssis-package-store"></a>Origen del paquete = Almacén de paquetes SSIS  
 **Server**  
 Escriba el nombre del servidor en el que se guardarán los paquetes de la actualización, o seleccione un servidor en la lista.  
  
### <a name="package-source--microsoft-sql-server"></a>Origen del paquete = Microsoft SQL Server  
 **Server**  
 Escriba el nombre del servidor en el que se guardarán los paquetes de la actualización, o seleccione este servidor en la lista.  
  
 **Usar autenticación de Windows**  
 Seleccione esta opción para utilizar la autenticación de Windows para conectarse al servidor.  
  
 **Utilizar autenticación de SQL Server**  
 Seleccione esta opción para usar la autenticación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para conectarse al servidor. Si usa la autenticación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , debe proporcionar un nombre de usuario y una contraseña.  
  
 **Nombre de usuario**  
 Escriba el nombre de usuario que se usará con la autenticación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para conectarse al servidor.  
  
 **Contraseña**  
 Escriba la contraseña que se usará con la autenticación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para conectarse al servidor.  
  
## <a name="see-also"></a>Consulte también  
 [Actualizar paquetes de Integration Services](install-windows/upgrade-integration-services-packages.md)  
  
  
