---
title: "Instalar actualizaciones desde el símbolo del sistema | Microsoft Docs"
ms.custom: 
ms.date: 09/08/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: install-windows
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: bc98ba2b-aae9-4d01-aa85-d4c36428cb0b
caps.latest.revision: "18"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.openlocfilehash: c04481fbe3cb71606509483e542747140b565ca8
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="installing-updates-from-the-command-prompt"></a>Instalar actualizaciones desde el símbolo del sistema
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Pruebe y modifique los scripts de instalación para adaptarlos a las necesidades de su organización. 
 
## <a name="sample-syntax-for-installation"></a>Sintaxis de ejemplo para la instalación 
El nombre del paquete de actualización puede variar y es posible que incluya un componente de idioma, edición y procesador. Aplique una actualización en una línea de comandos y reemplace <nombre_paquete> por el nombre del paquete de actualización: 
 
- Actualice una única instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y todos los componentes compartidos, como [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] y Herramientas de administración: puede especificar la instancia bien utilizando el parámetro InstanceName o bien con el parámetro InstanceID. Para actualizar una instancia preparada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], debe especificar el parámetro InstanceID.

    ```
    <package_name>.exe /qs /IAcceptSQLServerLicenseTerms /Action=Patch /InstanceName=MyInstance
    ```
    o bien 
    ```
    <package_name>.exe /qs /IAcceptSQLServerLicenseTerms /Action=Patch /InstanceID=\<Instance ID>. 
    ```

- El programa de instalación puede integrar las últimas actualizaciones del producto con la instalación del producto principal, de modo que el producto principal y las actualizaciones aplicables se instalen al mismo tiempo. Puede preparar una instalación de la instancia del motor de base de datos para incluir la actualización del producto: 

    ```
    setup.exe /q /IAcceptSQLServerLicenseTerms /ACTION=PrepareImage /UpdateEnabled=True /UpdateEnabled=True /UpdateSource=\<path where the update is downloaded> /INSTANCEID=\<Instance ID> /FEATURES=SQLEngine. 
    ```

- Actualice solo los componentes compartidos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], como [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] y las herramientas de administración: 

    ```
    <package_name>.exe /qs /IAcceptSQLServerLicenseTerms /Action=Patch 
    ```

- Actualice todas las instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el equipo y todos los componentes compartidos, como [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] y las herramientas de administración: 

    ```
    <package_name>.exe /qs /IAcceptSQLServerLicenseTerms /Action=Patch /AllInstances. 
    ```

- Quite una actualización de una sola instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y todos los componentes compartidos, como [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] y las herramientas de administración: 

    ```
    <package_name>.exe /qs /Action=RemovePatch /InstanceName=MyInstance. 
    ```

- Quite una actualización únicamente de los componentes compartidos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], como [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] y las herramientas de administración: 

    ```
    <package_name>.exe /qs /Action=RemovePatch 
    ```

  > [!NOTE] 
  > El instalador de la actualización se asegura de que los componentes compartidos estén siempre en, o por encima de, la versión de la instancia en el nivel más alto. 
 
## <a name="supported-parameters"></a>Parámetros admitidos 
 
> [!IMPORTANT] 
> Cuando sea posible, proporcione credenciales de seguridad en tiempo de ejecución. Si debe almacenar credenciales en un archivo de script, proteja el archivo para evitar el acceso no autorizado. 
 
|Switch|Descripción| 
|------------|-----------------| 
|**/?**|Muestra la ayuda del símbolo del sistema para la instalación desatendida| 
|**/action=Patch o /action=RemovePatch**|Especifica la acción de instalación: Patch o RemovePatch.| 
|**/allinstances**|Aplica la actualización de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a todas las instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y a todos los componentes compartidos que no reconocen instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .| 
|**/instancename=nombreDeInstancia***|Aplica la actualización de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] denominada InstanceName y a todos los componentes compartidos que no reconocen instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .| 
|**/InstanceID=Inst1**|Aplica la actualización de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Inst1 y a todos los componentes compartidos que no reconocen instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .| 
|**/quiet**|Ejecuta el programa de instalación de la actualización de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en modo desatendido.| 
|**/qs**|Muestra únicamente el cuadro de diálogo de progreso de la interfaz de usuario.| 
|**/UpdateEnabled**|Especifica si el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe detectar e incluir actualizaciones del producto. Los valores válidos son True y False, o 1 y 0. De forma predeterminada, la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] incluirá las actualizaciones que encuentre.| 
|**/IAcceptSQLServerLicenseTerms**|Solo es obligatorio cuando se especifica el parámetro /Q o /QS para las instalaciones desatendidas.| 
 
 *No puede especificar este parámetro para aplicar una actualización a una instancia preparada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Debe especificar el parámetro /instanceID en su lugar. 
 
## <a name="see-also"></a>Vea también 
 [Información general sobre la instalación de servicios de SQL Server](http://msdn.microsoft.com/library/6a9fd19b-2367-4908-b638-363b1e929e1e) 
 
 
