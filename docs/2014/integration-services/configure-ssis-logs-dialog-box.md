---
title: Cuadro de diálogo configurar registros de SSIS | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.configuredtslogs.loggingdetails.f1
- sql12.dts.designer.configuredtslogs.providersandlogs.f1
- sql12.dts.designer.configuredtslogs.containers.f1
helpviewer_keywords:
- Configure SSIS Logs dialog box
ms.assetid: 4b980275-cd9a-4943-8c36-727d51f9a484
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 6fab2f2e8fad2cd77e5bc27a78e66940fc40544b
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84921676"
---
# <a name="configure-ssis-logs-dialog-box"></a>Configurar registros de SSIS, cuadro de diálogo
  Use el cuadro de diálogo **Configurar registros de SSIS** para definir las opciones de registro de un paquete.  
  
 **¿Qué desea hacer?**  
  
1.  [Abrir el cuadro de diálogo Configurar registros de SSIS](#open_dialog)  
  
2.  [Configurar las opciones en el panel Contenedores](#container)  
  
3.  [Configurar las opciones en la pestaña Proveedores y registros](#provider)  
  
4.  [Configurar las opciones en la pestaña Detalles](#detail)  
  
##  <a name="open-the-configure-ssis-logs-dialog-box"></a><a name="open_dialog"></a>Abrir el cuadro de diálogo configurar registros de SSIS  
 **Para abrir el cuadro de diálogo Configurar registros de SSIS**  
  
-   En el Diseñador [!INCLUDE[ssIS](../includes/ssis-md.md)] , haga clic en **Registro** en el menú **SSIS** .  
  
##  <a name="configure-the-options-in-the-containers-pane"></a><a name="container"></a>Configurar las opciones en el panel contenedores  
 Utilice el panel **Contenedores** del cuadro de diálogo **Configurar registros de SSIS** para habilitar el paquete y sus contenedores para registro.  
  
### <a name="options"></a>Opciones  
 **Contenedores**  
 Active las casillas en la vista jerárquica para habilitar el paquete y sus contenedores para registro:  
  
-   Si no se activan, el contenedor no está habilitado para el registro. Seleccione esta opción para habilitar el registro.  
  
-   Si esta casilla aparece atenuada, el contenedor utiliza las opciones de registro de su elemento primario. Esta opción no está disponible para el paquete.  
  
-   Si se activa, el contenedor define sus propias opciones de registro.  
  
 Si un contenedor aparece atenuado y desea establecer opciones de registro en el contenedor, haga clic dos veces en la casilla. El primer clic desactiva la casilla y el segundo la activa para permitirle que elija los proveedores de registro que desea utilizar y para seleccionar la información que desea registrar.  
  
##  <a name="configure-the-options-on-the-providers-and-logs-tab"></a><a name="provider"></a>Configurar las opciones de la pestaña proveedores y registros  
 Use la pestaña **Proveedores y registros** del cuadro de diálogo **Configurar registros de SSIS** con el fin de crear y configurar registros para la captura de eventos en tiempo de ejecución.  
  
### <a name="options"></a>Opciones  
 **Tipo de proveedor**  
 Seleccione un tipo de proveedor de registro de la lista.  
  
 **Add (Agregar)**  
 Agregue un registro del tipo especificado a la colección de proveedores de registro del paquete.  
  
 **Nombre**  
 Use las casillas para habilitar o deshabilitar registros para contenedores o tareas que se han seleccionado en el panel **Contenedores** del cuadro de diálogo **Configurar registros de SSIS** . El campo del nombre se puede modificar. Utilice el nombre predeterminado para el proveedor o escriba un nombre descriptivo único.  
  
 **Descripción**  
 El campo de la descripción se puede modificar. Haga clic en la descripción predeterminada del registro y, a continuación, modifíquela.  
  
 **Configuración**  
 Seleccione un administrador de conexiones existente de la lista o haga clic en \<**New connection...**> para crear un nuevo administrador de conexiones. En función del tipo de proveedor de registro, puede configurar un administrador de conexiones OLE DB o un administrador de conexiones de archivos. El proveedor de registro para Registro de eventos de [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows no requiere conexión.  
  
 Temas relacionados: [OLE DB Connection Manager](connection-manager/ole-db-connection-manager.md) , [File Connection Manager](connection-manager/file-connection-manager.md)  
  
 **Eliminar**  
 Seleccione un proveedor de registro y haga clic en **Eliminar**.  
  
##  <a name="configure-the-options-on-the-details-tab"></a><a name="detail"></a>Configurar las opciones de la pestaña detalles  
 Utilice la pestaña **Detalles** del cuadro de diálogo **Configurar registros de SSIS** para especificar los eventos que se van a habilitar para el registro y los detalles de información que se van a registrar. La información que selecciona se aplica a todos los proveedores de registro del paquete. Por ejemplo, no puede escribir cierta información en la instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e información diferente en un archivo de texto.  
  
### <a name="options"></a>Opciones  
 **Eventos**  
 Habilite o deshabilite eventos para el registro.  
  
 **Descripción**  
 Vea una descripción del evento.  
  
 **Avanzadas**  
 Seleccione o borre eventos para el registro, y seleccione o borre información que se va a registrar para cada evento. Haga clic en **Básicas** para ocultar todos los detalles de registro a excepción de la lista de eventos. La información siguiente está disponible para el registro:  
  
|Value|Descripción|  
|-----------|-----------------|  
|**Equipo**|Nombre del equipo en el que ha tenido lugar el evento registrado.|  
|**Operador**|El nombre de usuario de la persona que ha iniciado el paquete.|  
|**SourceName**|El nombre del paquete, contenedor o tarea en la que ha tenido lugar el evento registrado.|  
|**SourceID**|El nombre del identificador único global (GUID) del paquete, la tarea o el contenedor en el que ha tenido lugar el evento registrado.|  
|**ExecutionID**|El identificador único global de la instancia de ejecución del paquete.|  
|**MessageText**|Mensaje asociado a la entrada del registro.|  
|**DataBytes**|Reservado para uso futuro.|  
  
 **Basic**  
 Seleccione o borre los eventos de registro. Esta opción oculta los detalles de registro a excepción de la lista de eventos. Si selecciona un evento, se seleccionan todos los detalles de registro para el evento de forma predeterminada. Haga clic en **Avanzadas** para mostrar los detalles de registro.  
  
 **Cargar**  
 Especifique un archivo XML existente para utilizarlo como una plantilla para establecer las opciones de registro.  
  
 **Guardar**  
 Guarde los detalles de configuración como una plantilla para un archivo XML.  
  
  
