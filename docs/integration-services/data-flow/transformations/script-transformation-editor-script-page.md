---
title: "Editor de transformación script (página Script) | Documentos de Microsoft"
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
- sql13.dts.designer.scriptcomponent.script.f1
helpviewer_keywords:
- Script Transformation Editor
ms.assetid: 4c6d1901-ef21-4aa7-9d0a-6bbeb7fadf1c
caps.latest.revision: 38
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ce227c91ad8109f3f8f7686e01a219392146602e
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="script-transformation-editor-script-page"></a>Editor de transformación Script (página Script)
  Use la pestaña **Script** del cuadro de diálogo **Editor de transformación Script** para especificar un script y las propiedades relacionadas.  
  
 Para obtener más información acerca del componente de script, vea [Script Component](../../../integration-services/data-flow/transformations/script-component.md) y [Configuring the Script Component in the Script Component Editor](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md). Para obtener información acerca de cómo programar el componente de script, vea [Extending the Data Flow with the Script Component](../../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md).  
  
## <a name="options"></a>Opciones  
 **Propiedades**  
 Vea y modifique las propiedades de la transformación de script. Muchas de las propiedades mostradas son de solo lectura. Puede modificar las siguientes propiedades:  
  
|Value|Description|  
|-----------|-----------------|  
|**Description**|Describe la transformación del script según su propósito.|  
|**LocaleID**|Especifica la configuración regional para proporcionar información específica de la región para ordenar y para la conversión de fecha y hora.|  
|**Nombre**|Escriba un nombre descriptivo para el componente.|  
|**ValidateExternalMetadata**|Indica si la transformación del script valida metadatos de columna con orígenes de datos externos en tiempo de diseño. El valor **false** retrasa la validación hasta el momento de la ejecución.|  
|**Variables de solo lectura**|Escriba una lista de variables separadas por comas (sin espacios) a la que la transformación del script tenga acceso de solo lectura.<br /><br /> Nota: Los nombres de variables distinguen entre mayúsculas y minúsculas.|  
|**Variables de lectura/escritura**|Escriba una lista de variables separadas por comas (sin espacios) a la que la transformación del script tenga acceso de lectura y escritura.<br /><br /> Nota: Los nombres de variables distinguen entre mayúsculas y minúsculas.|  
|**Lenguaje de script**|Seleccione el lenguaje de script que va a usar el componente de script.<br /><br /> Para establecer el lenguaje de script predeterminado para los componentes Script y las tareas de script, utilice la opción **Lenguaje de scripting** en la página **General** del cuadro de diálogo **Opciones** .|  
|**UserComponentTypeName**|Especifica la clase <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponentHost> y el ensamblado **Microsoft.SqlServer.TxScript** compatibles con la infraestructura de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
  
 **Editar script**  
 Use [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools for Applications (VSTA) para crear o modificar un script.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de mensajes y Error de Integration Services](../../../integration-services/integration-services-error-and-message-reference.md)   
 [Seleccionar tipo de componente de Script](../../../integration-services/data-flow/transformations/select-script-component-type.md)   
 [Editor de transformación script &#40; página columnas de entrada &#41;](../../../integration-services/data-flow/transformations/script-transformation-editor-input-columns-page.md)   
 [Editor de transformación script &#40; entradas y salidas página &#41;](../../../integration-services/data-flow/transformations/script-transformation-editor-inputs-and-outputs-page.md)   
 [Editor de transformación script &#40; Página Administradores de conexión &#41;](../../../integration-services/data-flow/transformations/script-transformation-editor-connection-managers-page.md)   
 [Ejemplos de componente de Script adicionales](../../../integration-services/extending-packages-scripting-data-flow-script-component-examples/additional-script-component-examples.md)  
  
  
