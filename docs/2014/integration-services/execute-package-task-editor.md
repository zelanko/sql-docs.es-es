---
title: Editor de la tarea ejecutar paquete | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.executepackagetask.parameter.F1
- sql12.dts.designer.executepackagetask.package.f1
- sql12.dts.designer.executepackagetask.general.f1
ms.assetid: c2c96b4f-eb10-4d8b-be34-88edfd0785fb
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 337b261c8c6b51125510ae463a673c746d7d6604
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2020
ms.locfileid: "85429292"
---
# <a name="execute-package-task-editor"></a>Editor de la tarea Ejecutar paquete
  Utilice el Editor de la tarea Ejecutar paquete para configurar la tarea Ejecutar paquete. La tarea Ejecutar paquete amplía las capacidades empresariales de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , ya que permite que los paquetes ejecuten otros paquetes como parte de un flujo de trabajo.  
  
 **¿Qué desea hacer?**  
  
-   [Abrir el Editor de la tarea Ejecutar paquete](#open)  
  
-   [Establecer las opciones de la página General](#general)  
  
-   [Establecer las opciones de la página Paquete](#package)  
  
-   [Establecer las opciones de la página Enlaces de parámetro](#parameter)  
  
##  <a name="open-the-execute-package-task-editor"></a><a name="open"></a>Abrir el editor de la tarea ejecutar paquete  
  
1.  Abra un proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] en [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] que contenga una tarea Ejecutar paquete.  
  
2.  Haga clic con el botón derecho en la tarea en el Diseñador SSIS y, después, haga clic en **Editar**.  
  
##  <a name="set-the-options-on-the-general-page"></a><a name="general"></a>Establecer las opciones de la página general  
 **Nombre**  
 Escriba un nombre único para la tarea Ejecutar paquete. Este nombre se utiliza como etiqueta en el icono de tarea.  
  
> [!NOTE]  
>  Los nombres de tarea deben ser únicos en un paquete.  
  
 **Descripción**  
 Escriba una descripción de la tarea Ejecutar paquete.  
  
##  <a name="set-the-options-on-the-package-page"></a><a name="package"></a>Establecer las opciones de la página paquete  
 **Volvió**  
 Seleccione **Referencia de proyecto** para los paquetes secundarios que están en el proyecto. Seleccione **Referencia externa** para los paquetes secundarios que se encuentran fuera del paquete  
  
> [!NOTE]  
>  La opción **ReferenceType** es de solo lectura y se establece en **Referencia externa** si el proyecto que contiene el paquete no se ha convertido al modelo de implementación de proyectos. Para más información sobre la conversión, vea [Implementación de paquetes en el servidor de Integration Services](../../2014/integration-services/deploy-projects-to-integration-services-server.md).  
  
 **Contraseña**  
 Si el paquete secundario está protegido con contraseña, tiene que proporcionar esta contraseña o hacer clic en el botón de puntos suspensivos (…) y crear una contraseña.  
  
 `ExecuteOutOfProcess`  
 Especifique si el paquete secundario se ejecuta en el proceso del paquete primario o en un proceso independiente. De forma predeterminada, la propiedad ExecuteOutOfProcess de la tarea ejecutar paquete se establece en `False` y el paquete secundario se ejecuta en el mismo proceso que el paquete primario. Si establece esta propiedad en `true`, el paquete secundario se ejecuta en un proceso independiente. Esto puede ralentizar el inicio del paquete secundario. Además, si se establece la propiedad en `true`, no se podrá depurar el paquete si realizó únicamente una instalación de herramientas; deberá instalar el producto [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. Para obtener más información, vea [instalar Integration Services](install-windows/install-integration-services.md).  
  
### <a name="referencetype-dynamic-options"></a>Opciones dinámicas de ReferenceType  
  
#### <a name="referencetype--external-reference"></a>ReferenceType = Referencia externa  
 **Ubicación**  
 Seleccione la ubicación del paquete secundario. Esta propiedad presenta las opciones indicadas en la siguiente tabla.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**SQL Server**|Establezca la ubicación de una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].|  
|**Sistema de archivos**|Permite establecer como ubicación el sistema de archivos.|  
  
 **Connection**  
 Seleccione el tipo de ubicación de almacenamiento para el paquete secundario.  
  
 **PackageNameReadOnly**  
 Muestra el nombre del paquete.  
  
#### <a name="referencetype--project-reference"></a>ReferenceType = Referencia de proyecto  
 **PackageNameFromProjectReference**  
 Seleccione un paquete incluido en el proyecto para que sea el paquete secundario.  
  
### <a name="location-dynamic-options"></a>Opciones dinámicas de ubicación  
  
#### <a name="location--sql-server"></a>Ubicación = SQL Server  
 **Connection**  
 Seleccione un administrador de conexiones de OLE DB de la lista o haga clic en \<**New connection...**> para crear un nuevo administrador de conexiones.  
  
 **Temas relacionados:** [Administrador de conexiones OLE DB](connection-manager/ole-db-connection-manager.md), [Configurar el administrador de conexiones OLE DB](../../2014/integration-services/configure-ole-db-connection-manager.md)  
  
 **Nombredepaquete**  
 Escriba el nombre del paquete secundario, o bien haga clic en los puntos suspensivos (…) y, después, busque el paquete.  
  
#### <a name="location--file-system"></a>Ubicación = Sistema de archivos  
 **Connection**  
 Seleccione un administrador de conexiones de archivos de la lista o haga clic en \<**New connection...**> para crear un nuevo administrador de conexiones.  
  
 **Temas relacionados:** [File Connection Manager](connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../2014/integration-services/file-connection-manager-editor.md)  
  
 **PackageNameReadOnly**  
 Muestra el nombre del paquete.  
  
##  <a name="set-the-options-on-the-parameter-bindings-page"></a><a name="parameter"></a>Establecer las opciones de la página enlaces de parámetros  
 Puede pasar valores del paquete primario o del proyecto al paquete secundario. El proyecto debe utilizar el modelo de implementación del proyecto y el paquete secundario debe estar incluido en el mismo proyecto que contiene el paquete primario.  
  
 Para obtener información sobre cómo convertir un proyecto al modelo de implementación de proyectos, vea [Implementación de paquetes en el servidor de Integration Services](../../2014/integration-services/deploy-projects-to-integration-services-server.md).  
  
 **Parámetro de paquete secundario**  
 Escriba o seleccione un nombre para el parámetro de paquete secundario.  
  
 **Enlazar un parámetro o variable**  
 Seleccione el parámetro o variable que contiene el valor que desea pasar al paquete secundario.  
  
 **Add (Agregar)**  
 Haga clic para asignar un parámetro o variable a un parámetro de paquete secundario.  
  
 **Quitar**  
 Haga clic para quitar una asignación entre un parámetro o variable y un parámetro de paquete secundario.  
  
  
