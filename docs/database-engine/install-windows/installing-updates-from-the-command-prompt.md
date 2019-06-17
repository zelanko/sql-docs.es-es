---
title: Instalar actualizaciones desde el símbolo del sistema | Microsoft Docs
ms.custom: ''
ms.date: 09/08/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: bc98ba2b-aae9-4d01-aa85-d4c36428cb0b
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
manager: jroth
ms.openlocfilehash: fdf35fa6ad124784f44391e5ad6b7d42cd1064a4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66794853"
---
# <a name="installing-updates-from-the-command-prompt"></a>Instalar actualizaciones desde el símbolo del sistema

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Pruebe y modifique los scripts de instalación para adaptarlos a las necesidades de su organización. 
 
## <a name="sample-syntax-for-installation"></a>Sintaxis de ejemplo para la instalación 
El nombre del paquete de actualización puede variar y es posible que incluya un componente de idioma, edición y procesador. Aplique una actualización en una línea de comandos y reemplace <nombre_paquete> por el nombre del paquete de actualización: 
 
- Actualice una sola instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y todos los componentes compartidos, como [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] y las herramientas de administración: Puede especificar la instancia mediante el parámetro InstanceName o InstanceID. Para actualizar una instancia preparada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], debe especificar el parámetro InstanceID.

    ```
    <package_name>.exe /qs /IAcceptSQLServerLicenseTerms /Action=Patch /InstanceName=MyInstance
    ```
    o Administrador de configuración de 
    ```
    <package_name>.exe /qs /IAcceptSQLServerLicenseTerms /Action=Patch /InstanceID=\<Instance ID>. 
    ```

- El programa de instalación puede integrar las últimas actualizaciones del producto con la instalación del producto principal, de modo que el producto principal y las actualizaciones aplicables se instalen al mismo tiempo. Puede preparar una instalación de la instancia del motor de base de datos para incluir la actualización del producto: 

    ```
    setup.exe /q /IAcceptSQLServerLicenseTerms /ACTION=PrepareImage /UpdateEnabled=True /UpdateSource=\<path where the update is downloaded> /INSTANCEID=\<Instance ID> /FEATURES=SQLEngine. 
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
 [Información general sobre la instalación de servicios de SQL Server](https://msdn.microsoft.com/library/6a9fd19b-2367-4908-b638-363b1e929e1e) 
 
 
