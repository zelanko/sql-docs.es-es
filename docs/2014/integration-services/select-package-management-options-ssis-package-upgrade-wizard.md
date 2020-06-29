---
title: Seleccionar opciones de Administración de paquetes (Asistente para actualización del paquete SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.is.upgradewizard.selectpackagemgtoptions.f1
ms.assetid: 810fc020-51cd-43ed-9f35-af99b4f35947
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 38bb9102551c56d82bc3cf32ca31e02f7eed4625
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2020
ms.locfileid: "85422002"
---
# <a name="select-package-management-options-ssis-package-upgrade-wizard"></a>Seleccionar opciones de administración de paquetes (Asistente para actualización del paquete SSIS)
  Utilice la página **Seleccionar opciones de administración de paquetes** con el fin de especificar las opciones para actualizar paquetes.  
  
 **Para ejecutar el Asistente para actualización del paquete SSIS**  
  
-   [Actualizar paquetes de Integration Services mediante el Asistente para actualizar paquetes SSIS](install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md)  
  
## <a name="options"></a>Opciones  
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
  
 Para más información, vea [Actualizar paquetes de Integration Services mediante el Asistente para actualizar paquetes SSIS](install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md).  
  
## <a name="see-also"></a>Consulte también  
 [Actualizar paquetes de Integration Services](install-windows/upgrade-integration-services-packages.md)  
  
  
