---
title: Crear InfoCube para los datos de transacción | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 673cea01-a260-4fce-a1a0-f73839289805
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 43855c0c13052598de5e2c96ffc8cae5f289d249
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84916445"
---
# <a name="create-infocube-for-transaction-data"></a>Crear InfoCube para los datos de transacción
  Use el cuadro de diálogo **Crear InfoCube para los datos de transacción** para crear un InfoCube nuevo para los datos de transacciones en el sistema SAP Netweaver BW.  
  
 Puede abrir el cuadro de diálogo **Crear InfoCube para los datos de transacción** desde la página **Administrador de conexiones** del **Editor de destino de SAP BW**. Para más información acerca del destino de SAP BW, consulte [SAP BW Destination](sap-bw-destination.md).  
  
> [!IMPORTANT]  
>  La documentación de Microsoft Connector 1.1 for SAP BW da por supuesto que se está familiarizado con el entorno SAP Netweaver BW. Para obtener más información acerca de SAP Netweaver BW, o sobre cómo configurar los objetos y los procesos de SAP Netweaver BW, vea la documentación de SAP.  
  
 **Para abrir el cuadro de diálogo Crear InfoCube para los datos de transacción**  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contiene el destino SAP BW.  
  
2.  En la pestaña **Flujo de datos** , haga doble clic en el destino de SAP BW.  
  
3.  En **Editor de destino SAP BW**, haga clic en **Administrador de conexiones** para abrir la página **Administrador de conexiones** del editor.  
  
4.  En la página **Administrador de conexiones** , en el cuadro del grupo **Crear objetos de SAP BW** , seleccione **InfoCube**y, a continuación, haga clic en **Crear**.  
  
## <a name="general-options"></a>Opciones generales  
 **Nombre de InfoCube**  
 Permite escribir un nombre para el nuevo InfoCube.  
  
 **Descripción larga**  
 Permite escribir una descripción para el nuevo InfoCube.  
  
 **Guardar y activar**  
 Permite guardar y activar el nuevo InfoCube.  
  
## <a name="infocube-transfer-structure-options"></a>Opciones de la estructura de transferencia de InfoCube  
 La sección sobre la estructura de transferencia de InfoCube permite asociar columnas del flujo de datos a InfoObjects.  
  
 **PipelineElement**  
 Permite mostrar la columna en la salida del flujo de datos que está conectada al destino de SAP BW.  
  
 **PipelineDataType**  
 Permite mostrar el tipo de datos de la columna del flujo de datos.  
  
 **InfoObject**  
 Permite mostrar el nombre del InfoObject que está asociado a la columna del flujo datos.  
  
 **Tipo**  
 Permite mostrar el tipo del InfoObject que está asociado a la columna del flujo datos. En la siguiente tabla se muestran los posibles valores para el tipo.  
  
|Value|Descripción|  
|-----------|-----------------|  
|CHA|Características|  
|UNI|Unidades|  
|KYF|Cifras clave|  
|TIM|Características de tiempo|  
  
 **IObject - Buscar**  
 Permite asociar un InfoObject existente a la columna de flujo de datos de la fila actual. Para efectuar este tipo de asociación, haga clic en **Buscar** y, a continuación use el cuadro de diálogo **Buscar InfoObject** para seleccionar el InfoObject existente. Para obtener más información sobre este cuadro de diálogo, vea [Look Up InfoObject](look-up-infoobject.md).  
  
 Después de seleccionar un InfoObject existente, el componente rellena las columnas **InfoObject** y **Tipo** con los valores seleccionados.  
  
 **IObject - Nuevo**  
 Permite crear un InfoObject nuevo y asociarlo a la columna de flujo de datos de la fila actual. Para crear el InfoObject nuevo, haga clic en **Nuevo**y, a continuación, use el cuadro de diálogo **Crear nuevo InfoObject** para crear el InfoObject. Para obtener más información sobre este cuadro de diálogo, vea [Create New InfoObject](create-new-infoobject.md).  
  
 Después haber creado un InfoObject nuevo, el componente rellena las columnas **InfoObject** y **Tipo** con los valores nuevos.  
  
 **IObject - Quitar**  
 Permite quitar la asociación entre el InfoObject y la columna de flujo de datos de la fila actual. Para quitar esta asociación, haga clic en **Quitar**.  
  
## <a name="see-also"></a>Consulte también  
 [Ayuda F1 de Microsoft Connector 1.1 for SAP BW](../microsoft-connector-for-sap-bw-f1-help.md)  
  
  
