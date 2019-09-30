---
title: Editor de destino de SAP BW (página Asignaciones) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.sapbwdestination.columns.f1
ms.assetid: dfa1f1d6-6b64-4331-bdc5-eaa8b7aa41a1
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 31c6ab812081d66980002ed0138f5b1ad63f62b5
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/26/2019
ms.locfileid: "71298100"
---
# <a name="sap-bw-destination-editor-mappings-page"></a>Editor de destino de SAP BW (página Asignaciones)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Use la página **Asignaciones** del cuadro de diálogo **Editor de destino de SAP BW** para asignar columnas de entrada a columnas de destino.  
  
 Para obtener más información sobre el destino SAP BW de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW, vea [Destino de SAP BW](../../integration-services/data-flow/sap-bw-destination.md).  
  
> [!IMPORTANT]  
>  La documentación de Microsoft Connector 1.1 for SAP BW da por supuesto que se está familiarizado con el entorno SAP Netweaver BW. Para obtener más información acerca de SAP Netweaver BW, o sobre cómo configurar los objetos y los procesos de SAP Netweaver BW, vea la documentación de SAP.  
  
 **Para abrir la página Asignaciones**  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contiene el destino SAP BW.  
  
2.  En la pestaña **Flujo de datos** , haga doble clic en el destino de SAP BW.  
  
3.  En **Editor de destino de SAP BW**, haga clic en **Asignaciones** para abrir la página **Asignaciones** del editor.  
  
## <a name="options"></a>Opciones  
  
> [!NOTE]  
>  Si no conoce todos los valores necesarios para configurar el destino, puede que tenga que ponerse en contacto con el administrador de SAP.  
  
 La página **Asignaciones** del **Editor de destino de SAP BW** consta de dos secciones:  
  
-   En la sección superior aparecen las columnas de entrada y de destino disponibles y permite crear asignaciones entre estos dos tipos de columnas.  
  
-   En la sección inferior hay una tabla que indica las columnas de entrada que se han asignado y a qué columnas de salida.  
  
### <a name="upper-section-options"></a>Opciones de la sección superior  
 La sección superior presenta las opciones siguientes:  
  
 **Columnas de entrada disponibles**  
 Muestra la lista de columnas de entrada disponibles.  
  
 Para asignar una columna de entrada a una columna de destino, arrastre una columna desde la lista **Columnas de entrada disponibles** y colóquela en la lista **Columnas de destino disponibles** .  
  
 **Columnas de destino disponibles**  
 Muestra la lista de columnas de destino disponibles.  
  
 Para asignar una columna de entrada a una columna de destino, arrastre una columna desde la lista **Columnas de entrada disponibles** y colóquela en la lista **Columnas de destino disponibles** .  
  
 La sección superior dispone también de un menú contextual que se abre si hace clic con el botón secundario en el fondo. Este menú contextual contiene las siguientes opciones:  
  
-   **Seleccionar todas las asignaciones**  
  
-   **Eliminar asignaciones seleccionadas**  
  
-   **Asignar elementos por coincidencia de nombres**  
  
### <a name="lower-section-columns"></a>Columnas de la sección inferior  
 La sección inferior presenta una tabla con las asignaciones y tiene las columnas siguientes:  
  
 **Columna de entrada**  
 Permite ver las columnas de entrada que ha seleccionado.  
  
 Para asignar una columna de entrada a la misma columna de destino, seleccione una columna de entrada diferente de la lista. Para quitar una asignación, seleccione **\<omitir>** con el fin de excluir la columna de entrada de los resultados.  
  
 **Columna de destino**  
 Permite ver todas las columnas de destino disponibles, tanto si las columnas están asignadas como si no lo están.  
  
## <a name="see-also"></a>Consulte también  
 [Editor de destino de SAP BW &#40;página Administrador de conexiones&#41;](../../integration-services/data-flow/sap-bw-destination-editor-connection-manager-page.md)   
 [Editor de destino de SAP BW &#40;página Salida de error&#41;](../../integration-services/data-flow/sap-bw-destination-editor-error-output-page.md)   
 [Editor de destino de SAP BW &#40;página Avanzadas&#41;](../../integration-services/data-flow/sap-bw-destination-editor-advanced-page.md)   
 [Ayuda F1 de Microsoft Connector for SAP BW](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  
