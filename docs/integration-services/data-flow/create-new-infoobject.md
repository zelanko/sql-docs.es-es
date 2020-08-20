---
description: Crear nuevo InfoObject
title: Crear nuevo InfoObject | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 3587a633-1c0b-4d63-a22a-6b2b93923c3a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9cb9336b7999373b1f6af5bb5327a35f77fdbe7e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88495891"
---
# <a name="create-new-infoobject"></a>Crear nuevo InfoObject

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Use el cuadro de diálogo **Crear nuevo InfoObject** para crear un nuevo InfoObject en el sistema SAP Netweaver BW.  
  
 Puede abrir el cuadro de diálogo **Crear InfoObject** desde la página **Administrador de conexiones** del **Editor de destino de SAP BW**. Para más información acerca del destino de SAP BW, consulte [SAP BW Destination](../../integration-services/data-flow/sap-bw-destination.md).  
  
> [!IMPORTANT]  
>  La documentación de Microsoft Connector 1.1 for SAP BW da por supuesto que se está familiarizado con el entorno SAP Netweaver BW. Para obtener más información acerca de SAP Netweaver BW, o sobre cómo configurar los objetos y los procesos de SAP Netweaver BW, vea la documentación de SAP.  
  
 **Para abrir el cuadro de diálogo Crear nuevo InfoObject**  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contiene el destino SAP BW.  
  
2.  En la pestaña **Flujo de datos** , haga doble clic en el destino de SAP BW.  
  
3.  En **Editor de destino SAP BW**, haga clic en **Administrador de conexiones** para abrir la página **Administrador de conexiones** del editor.  
  
4.  En la página **Administrador de conexiones** , en el cuadro del grupo **Crear objetos de SAP BW** , lleve a cabo uno de los siguientes pasos para crear un InfoObject:  
  
    1.  Para crear un InfoObject directamente, seleccione **InfoObject**y haga clic en **Crear** para abrir el cuadro de diálogo **Crear nuevo InfoObject** .  
  
    2.  Para crear un InfoObject mientras crea un InfoCube, seleccione **InfoCube**y, a continuación, haga clic en **Crear**. En el cuadro de diálogo **Crear InfoCube para los datos de transacción** , en la columna **IObject** para una de las filas en la lista, seleccione **Crear** para abrir el cuadro de diálogo **Crear nuevo InfoObject** .  
  
        > [!NOTE]  
        >  Cada fila de la tabla representa una columna en el flujo de datos del paquete.  
  
    3.  Para crear un InfoObject mientras crea un InfoSource para los datos de transacción, seleccione **InfoSource**y, a continuación, haga clic en **Crear**. En el cuadro de diálogo **Crear InfoSource** , seleccione **Datos transaccionales**y, a continuación, haga clic en **Aceptar**. En el cuadro de diálogo **Crear InfoSource para los datos de transacción** , en la columna **IObject** para una de las filas en la lista, seleccione **Crear** para abrir el cuadro de diálogo **Crear nuevo InfoObject** .  
  
        > [!NOTE]  
        >  Cada fila de la tabla representa una columna en el flujo de datos del paquete.  
  
    4.  Para crear un InfoObject mientras crea un InfoSource para los datos maestros, seleccione **InfoSource**y, a continuación, haga clic en **Crear**. En el cuadro de diálogo **Crear InfoSource** , seleccione **Datos maestros**y, a continuación, haga clic en **Aceptar**. En el cuadro de diálogo **Crear InfoSource para datos maestros** , haga clic en **Nuevo** para abrir el cuadro de diálogo **Crear nuevo InfoObject** .  
  
 También puede abrir el cuadro de diálogo **Crear nuevo InfoObject** si hace clic en **Nuevo** en la sección **Atributos** del cuadro de diálogo **Crear nuevo InfoObject** .  
  
## <a name="general-options"></a>Opciones generales  
 **Característica**  
 Cree un InfoObject que represente datos de dimensión.  
  
 **Cifra clave**  
 Permite crear un InfoObject que represente datos de hechos.  
  
 **Nombre de InfoObject**  
 Permite escribir un nombre para el InfoObject.  
  
 **Descripción breve**  
 Permite escribir una descripción breve para el InfoObject.  
  
 **Descripción larga**  
 Permite escribir una descripción larga para el InfoObject.  
  
 **Tiene datos maestros**  
 Permite indicar que el InfoObject contiene datos maestros en forma de atributos, texto o jerarquías.  
  
> [!NOTE]  
>   Seleccione esta opción si el InfoObject representa datos dimensionales y ha seleccionado la opción **Característica** .  
  
 **Permitir caracteres en minúscula**  
 Permite aceptar caracteres en minúsculas en los datos del InfoObject.  
  
 **Guardar y activar**  
 Permite guardar y activar el nuevo InfoObject.  
  
## <a name="data-type-options"></a>Opciones de tipo de datos  
 **CHAR - Cadena de caracteres**  
 Permite indicar que el InfoObject no contiene datos de caracteres.  
  
 **NUMC - Cadena numérica**  
 Permite indicar que el InfoObject no contiene datos numéricos.  
  
 **DATS - Fecha (AAAAMMDD)**  
 Permite indicar que el InfoObject no contiene datos de fecha.  
  
 **TIMS - Hora (HHMMSS)**  
 Permite indicar que InfoObject no contiene datos de hora.  
  
 **Longitud**  
 Permite escribir la longitud de los datos.  
  
## <a name="text-options"></a>Opciones de texto  
 **Con textos**  
 Permite indicar que el InfoObject no contiene datos de texto.  
  
 **Texto breve**  
 Permite indicar que el InfoObject no contiene textos breves.  
  
 **Texto intermedio**  
 Permite indicar que el InfoObject no contiene textos intermedios.  
  
 **Texto largo**  
 permite indicar que el InfoObject no contiene textos largos.  
  
 **Dependiente del idioma del texto**  
 Permite indicar que los textos dependen del idioma.  
  
 **Dependiente de la hora del texto**  
 Permite indicar que los textos dependen de la hora.  
  
## <a name="attributes-section"></a>Sección Atributos  
 La sección **Atributos** consta de una lista de atributos para InfoObject y de las opciones que permiten agregar y quitar atributos de la lista.  
  
### <a name="attributes-list"></a>Lista de atributos  
 La lista **Atributos** muestra los atributos del InfoObject que está creando. La lista **Atributos** tiene los siguientes encabezados de columna:  
  
 **InfoObject**  
 Permite ver el nombre del InfoObject.  
  
 **Descripción**  
 Permite ver la descripción del InfoObject.  
  
 **Tipo de InfoObject**  
 Permite ver el tipo de InfoObject. En la siguiente tabla se muestran los posibles valores para el tipo.  
  
|Value|Descripción|  
|-----------|-----------------|  
|CHA|Características|  
|KYF|Cifras clave|  
|UNI|Unidades|  
|TIM|Características de tiempo|  
  
### <a name="attributes-options"></a>Opciones de Atributos  
 Use las opciones siguientes para agregar y quitar los atributos para el InfoObject que está creando:  
  
 **Add (Agregar)**  
 Permite agregar un InfoObject existente como atributo.  
  
 Para agregar un InfoObject existente, haga clic en Agregar y, a continuación, use el cuadro de diálogo **Buscar InfoObject** para buscar el InfoObject. Para obtener más información sobre este cuadro de diálogo, vea [Look Up InfoObject](../../integration-services/data-flow/look-up-infoobject.md).  
  
 **Nuevo**  
 Permite agregar un InfoObject nuevo como atributo.  
  
 Para crear y agregar un InfoObject nuevo, haga clic en Nuevo y, a continuación, use una nueva instancia del cuadro de diálogo crear **Crear nuevo InfoObject** para crear el InfoObject nuevo.  
  
 **Remove**  
 Quita el InfoObject seleccionado de la lista **Atributos** .  
  
## <a name="see-also"></a>Consulte también  
 [Crear InfoCube para datos de transacción](../../integration-services/data-flow/create-infocube-for-transaction-data.md)   
 [Crear InfoSource](../../integration-services/data-flow/create-infosource.md)   
 [Crear InfoSource para datos de transacción](../../integration-services/data-flow/create-infosource-for-transaction-data.md)   
 [Crear InfoSource para datos maestros](../../integration-services/data-flow/create-infosource-for-master-data.md)   
 [Ayuda F1 de Microsoft Connector for SAP BW](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  
