---
title: Instalar actualizaciones desde el símbolo del sistema | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: bc98ba2b-aae9-4d01-aa85-d4c36428cb0b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 51ad82519e8afd5e4a871046465e0cafec2f783e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62774989"
---
# <a name="installing-updates-from-the-command-prompt"></a>Instalar actualizaciones desde el símbolo del sistema
  Pruebe y modifique los scripts de instalación para adaptarlos a las necesidades de su organización.  
  
## <a name="sample-syntax-for-installation"></a>Sintaxis de ejemplo para la instalación  
 El nombre del paquete de actualización puede variar y es posible que incluya un componente de idioma, edición y procesador. Aplique una actualización en una línea de comandos y reemplace <nombre_paquete> por el nombre del paquete de actualización:  
  
-   Actualizar una instancia única de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y todos los componentes comparten, como [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] y herramientas de administración: Puede especificar la instancia mediante el parámetro InstanceName o InstanceID. Para actualizar una instancia preparada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], debe especificar el parámetro InstanceID<nombre_paquete>.exe /qs /IAcceptSQLServerLicenseTerms /Action=Patch /InstanceName=miInstancia o <nombre_paquete>.exe /qs /IAcceptSQLServerLicenseTerms /Action=Patch /InstanceID=\<identificador de instancia>.  
  
-   El programa de instalación puede integrar las últimas actualizaciones del producto con la instalación del producto principal, de modo que el producto principal y las actualizaciones aplicables se instalen al mismo tiempo. Puede preparar una instalación de una instancia del motor de base de datos para que incluya la actualización del producto: setup.exe /q /IAcceptSQLServerLicenseTerms /ACTION=PrepareImage /UpdateEnabled=True /UpdateEnabled=True /UpdateSource=\<ruta de acceso donde se descarga la actualización> /INSTANCEID=\<identificador de instancia> /FEATURES=SQLEngine.  
  
-   Actualizar solo los componentes compartidos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], como [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] y las Herramientas de administración: <nombreDePaquete>.exe /qs /IAcceptSQLServerLicenseTerms /Action=Patch  
  
-   Actualizar todas las instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] del equipo y todos los componentes compartidos, como [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] y las Herramientas de administración: <nombreDePaquete>.exe /qs /IAcceptSQLServerLicenseTerms /Action=Patch /AllInstances.  
  
 Quite una actualización de la línea de comandos y reemplace <nombreDePaquete> por el nombre del paquete de actualización:  
  
-   Quitar una actualización de una única instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y todos los componentes compartidos, como [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] y las herramientas de administración: <nombre_paquete>.exe /qs /Action=RemovePatch /InstanceName=MyInstance.  
  
-   Quitar una actualización únicamente de los componentes compartidos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], como [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] y las herramientas de administración: <nombre_paquete>.exe /qs /Action=RemovePatch  
  
    > [!NOTE]  
    >  El instalador de la actualización se asegura de que los componentes compartidos estén siempre en, o por encima de, la versión de la instancia en el nivel más alto.  
  
## <a name="supported-command-prompt-parameters"></a>Parámetros del símbolo del sistema compatibles  
  
> [!IMPORTANT]  
>  Cuando sea posible, proporcione credenciales de seguridad en tiempo de ejecución. Si debe almacenar credenciales en un archivo de script, proteja el archivo para evitar el acceso no autorizado.  
  
|Modificador|Descripción|  
|------------|-----------------|  
|**/?**|Muestra la ayuda del símbolo del sistema para la instalación desatendida|  
|**/action=Patch o /action=RemovePatch**|Especifica la acción de instalación: Patch o RemovePatch.|  
|**/allinstances**|Aplica la actualización de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a todas las instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y a todos los componentes compartidos que no reconocen instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|**/instancename=InstanceName** <sup>1</sup>|Aplica la actualización de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] denominada InstanceName y a todos los componentes compartidos que no reconocen instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|**/InstanceID=Inst1**|Aplica la actualización de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Inst1 y a todos los componentes compartidos que no reconocen instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|**/quiet**|Ejecuta el programa de instalación de la actualización de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en modo desatendido.|  
|**/qs**|Muestra únicamente el cuadro de diálogo de progreso de la interfaz de usuario.|  
|**/UpdateEnabled**|Especifica si el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe detectar e incluir actualizaciones del producto. Los valores válidos son True y False, o 1 y 0. De forma predeterminada, la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] incluirá las actualizaciones que encuentre.|  
|**/IAcceptSQLServerLicenseTerms**|Solo es obligatorio cuando se especifica el parámetro /Q o /QS para las instalaciones desatendidas.|  
  
 <sup>1</sup> no se puede especificar este parámetro para aplicar una actualización a una instancia preparada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Debe especificar el parámetro /instanceID en su lugar.  
  
## <a name="see-also"></a>Vea también  
 [Información general sobre la instalación de servicios de SQL Server](../../sql-server/install/overview-of-sql-server-servicing-installation.md)  
  
  
