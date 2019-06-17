---
title: Seleccionar ubicación de origen (Asistente actualización del paquete SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.is.upgradewizard.selectsourcelocation.f1
ms.assetid: 429f146e-edb4-4401-a225-f2c8468971c5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 1ba348d3a47945bf9bb4f375310c5c92e6be7705
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66055940"
---
# <a name="select-source-location-ssis-package-upgrade-wizard"></a>Seleccionar ubicación de origen (Asistente para actualización del paquete SSIS)
  Utilice la página **Seleccionar ubicación de origen** para especificar el origen desde el que se actualizan los paquetes.  
  
> [!NOTE]  
>  Esta página solo está disponible cuando se ejecuta el Asistente para actualizar paquetes [!INCLUDE[ssIS](../includes/ssis-md.md)] desde [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] o en el símbolo del sistema.  
  
 **Para ejecutar el Asistente para actualización del paquete SSIS**  
  
-   [Actualizar paquetes de Integration Services mediante el Asistente para actualizar paquetes SSIS](install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md)  
  
## <a name="static-options"></a>Opciones estáticas  
 **Origen del paquete**  
 Seleccione la ubicación de almacenamiento que contiene los paquetes que se van a actualizar. Esta opción tiene los valores que figuran en la siguiente tabla.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**Sistema de archivos**|Indica que los paquetes que se van a actualizar están en una carpeta en el equipo local.<br /><br /> Para hacer que el asistente realice una copia de seguridad de los paquetes originales antes de actualizarlos, estos deben estar almacenados en el sistema de archivos. Para obtener más información, vea el tema de procedimientos.|  
|**Almacén de paquetes SSIS**|Indica que los paquetes que se van a actualizar están en el almacén de paquetes. El almacén de paquetes consta del conjunto de carpetas del sistema de archivos que el servicio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] administra. Para obtener más información, vea [Administración de paquetes &#40;servicio SSIS&#41;](service/package-management-ssis-service.md).<br /><br /> Al seleccionar este valor, se muestran las opciones dinámicas de **Origen del paquete** correspondientes.|  
|**Microsoft SQL Server**|Indica que los paquetes que se van a actualizar son de una instancia existente de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].<br /><br /> Al seleccionar este valor, se muestran las opciones dinámicas de **Origen del paquete** correspondientes.|  
  
 **Carpeta**  
 Escriba el nombre de una carpeta que contenga los paquetes que quiere actualizar o haga clic en **Examinar** y busque la carpeta.  
  
 **Examinar**  
 Busque la carpeta que contiene los paquetes que desea actualizar.  
  
## <a name="package-source-dynamic-options"></a>Opciones dinámicas de Origen del paquete  
  
### <a name="package-source--ssis-package-store"></a>Origen del paquete = Almacén de paquetes SSIS  
 **Server**  
 Escriba el nombre del servidor que tiene los paquetes que se van a actualizar o seleccione este servidor en la lista.  
  
### <a name="package-source--microsoft-sql-server"></a>Origen del paquete = Microsoft SQL Server  
 **Server**  
 Escriba el nombre del servidor que tiene los paquetes que se van a actualizar o seleccione este servidor en la lista.  
  
 **Usar la autenticación de Windows**  
 Seleccione esta opción para utilizar la autenticación de Windows para conectarse al servidor.  
  
 **Utilizar autenticación de SQL Server**  
 Seleccione esta opción para usar la autenticación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para conectarse al servidor. Si usa la autenticación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , debe proporcionar un nombre de usuario y una contraseña.  
  
 **Nombre de usuario.**  
 Escriba el nombre de usuario que la autenticación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usará para conectarse al servidor.  
  
 **Contraseña**  
 Escriba la contraseña que la autenticación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usará para conectarse al servidor.  
  
## <a name="see-also"></a>Vea también  
 [Actualizar paquetes de Integration Services](install-windows/upgrade-integration-services-packages.md)  
  
  
