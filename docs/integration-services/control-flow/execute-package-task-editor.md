---
title: Ejecutar el Editor de la tarea de paquete | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.executepackagetask.package.f1
- sql13.dts.designer.executepackagetask.parameter.F1
- sql13.dts.designer.executepackagetask.general.f1
ms.assetid: c2c96b4f-eb10-4d8b-be34-88edfd0785fb
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: a2e3655bedbb24f2174a62c8792cd168e7642592
ms.openlocfilehash: 6f03d1bb15f1513a7683c6719c42e9cd7f440a71
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="execute-package-task-editor"></a>Editor de la tarea Ejecutar paquete
  Utilice el Editor de la tarea Ejecutar paquete para configurar la tarea Ejecutar paquete. La tarea Ejecutar paquete amplía las capacidades empresariales de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , ya que permite que los paquetes ejecuten otros paquetes como parte de un flujo de trabajo.  
  
 **¿Qué desea hacer?**  
  
-   [Abrir el Editor de la tarea Ejecutar paquete](#open)  
  
-   [Establecer las opciones de la página General](#general)  
  
-   [Establecer las opciones de la página Paquete](#package)  
  
-   [Establecer las opciones de la página Enlaces de parámetro](#parameter)  
  
##  <a name="open"></a> Abrir el Editor de la tarea Ejecutar paquete  
  
1.  Abra un proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] que contenga una tarea Ejecutar paquete.  
  
2.  Haga clic con el botón derecho en la tarea en el Diseñador SSIS y, después, haga clic en **Editar**.  
  
##  <a name="general"></a> Establecer las opciones de la página General  
 **Nombre**  
 Escriba un nombre único para la tarea Ejecutar paquete. Este nombre se utiliza como etiqueta en el icono de tarea.  
  
> [!NOTE]  
>  Los nombres de tarea deben ser únicos en un paquete.  
  
 **Description**  
 Escriba una descripción de la tarea Ejecutar paquete.  
  
##  <a name="package"></a> Establecer las opciones de la página Paquete  
 **ReferenceType**  
 Seleccione **Referencia de proyecto** para los paquetes secundarios que están en el proyecto. Seleccione **Referencia externa** para los paquetes secundarios que se encuentran fuera del paquete  
  
> [!NOTE]  
>  La opción **ReferenceType** es de solo lectura y se establece en **Referencia externa** si el proyecto que contiene el paquete no se ha convertido al modelo de implementación de proyectos. [Implementación de Integration Services (SSIS) proyectos y paquetes](../../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md).  
  
 **Contraseña**  
 Si el paquete secundario está protegido con contraseña, debe proporcionar esta contraseña o hacer clic en el botón de puntos suspensivos (...) y crear una nueva contraseña.  
  
 **ExecuteOutOfProcess**  
 Especifique si el paquete secundario se ejecuta en el proceso del paquete primario o en un proceso independiente. De forma predeterminada, la propiedad ExecuteOutOfProcess de la tarea Ejecutar paquete se establece en **False**y el paquete secundario se ejecuta en el mismo proceso que el paquete primario. Si establece esta propiedad en **true**, el paquete secundario se ejecuta en un proceso independiente. Esto puede ralentizar el inicio del paquete secundario. Además, si establece la propiedad en **true**, no podrá depurar el paquete si ha realizado una instalación de solo herramientas (tendrá que instalar el producto [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ). Para más información, vea [Instalar Integration Services](../../integration-services/install-windows/install-integration-services.md).  
  
### <a name="referencetype-dynamic-options"></a>Opciones dinámicas de ReferenceType  
  
#### <a name="referencetype--external-reference"></a>ReferenceType = Referencia externa  
 **Ubicación**  
 Seleccione la ubicación del paquete secundario. Esta propiedad presenta las opciones indicadas en la siguiente tabla.  
  
|Value|Description|  
|-----------|-----------------|  
|**SQL Server**|Establezca la ubicación de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**Sistema de archivos**|Permite establecer como ubicación el sistema de archivos.|  
  
 **Conexión**  
 Seleccione el tipo de ubicación de almacenamiento para el paquete secundario.  
  
 **PackageNameReadOnly**  
 Muestra el nombre del paquete.  
  
#### <a name="referencetype--project-reference"></a>ReferenceType = Referencia de proyecto  
 **PackageNameFromProjectReference**  
 Seleccione un paquete incluido en el proyecto para que sea el paquete secundario.  
  
### <a name="location-dynamic-options"></a>Opciones dinámicas de ubicación  
  
#### <a name="location--sql-server"></a>Ubicación = SQL Server  
 **Conexión**  
 Seleccione un administrador de conexiones de OLE DB en la lista o haga clic en \< **nueva conexión...** > para crear una nueva conexión de administrador.  
  
 **Temas relacionados:** [Administrador de conexiones OLE DB](../../integration-services/connection-manager/ole-db-connection-manager.md), [Configurar el administrador de conexiones OLE DB](../../integration-services/connection-manager/configure-ole-db-connection-manager.md)  
  
 **PackageName**  
 Escriba el nombre del paquete secundario o haga clic en los puntos suspensivos (...) y después busque el paquete.  
  
#### <a name="location--file-system"></a>Ubicación = Sistema de archivos  
 **Conexión**  
 Seleccione un administrador de conexión de archivos en la lista o haga clic en \< **nueva conexión...** > para crear una nueva conexión de administrador.  
  
 **Temas relacionados:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 **PackageNameReadOnly**  
 Muestra el nombre del paquete.  
  
##  <a name="parameter"></a> Establecer las opciones de la página Enlaces de parámetro  
 Puede pasar valores del paquete primario o del proyecto al paquete secundario. El proyecto debe utilizar el modelo de implementación del proyecto y el paquete secundario debe estar incluido en el mismo proyecto que contiene el paquete primario.  
  
 Para obtener información sobre cómo convertir proyectos en el modelo de implementación de proyecto, vea [implementar Integration Services (SSIS) proyectos y paquetes](../../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md).  
  
 **Parámetro de paquete secundario**  
 Escriba o seleccione un nombre para el parámetro de paquete secundario.  
  
 **Enlazar un parámetro o variable**  
 Seleccione el parámetro o variable que contiene el valor que desea pasar al paquete secundario.  
  
 **Agregar**  
 Haga clic para asignar un parámetro o variable a un parámetro de paquete secundario.  
  
 **Quitar**  
 Haga clic para quitar una asignación entre un parámetro o variable y un parámetro de paquete secundario.  
  
  
