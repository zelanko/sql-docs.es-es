---
title: Analysis Services el editor de la tarea ejecutar DDL (página DDL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.asexecuteddltask.ddl.f1
helpviewer_keywords:
- Analysis Services Execute DDL Task Editor
ms.assetid: f21bf8d0-ec5f-4c18-9de0-8875addb927b
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 7cb1c84cccf4123f6ca1894baba5676937d80a15
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84925646"
---
# <a name="analysis-services-execute-ddl-task-editor-ddl-page"></a>Editor de la tarea Ejecutar DDL de Analysis Services (página DDL)
  Use la página **DDL** del cuadro de diálogo **Editor de la tarea Ejecutar DDL de Analysis Services** para especificar una conexión a un proyecto de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] o una base de datos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] y proporcionar información sobre el origen de las instrucciones del lenguaje de definición de datos (DDL).  
  
 Para obtener información acerca de esta tarea, vea [Analysis Services Execute DDL Task](control-flow/analysis-services-execute-ddl-task.md).  
  
## <a name="static-options"></a>Opciones estáticas  
 **Connection**  
 Seleccione un [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] proyecto o un [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Administrador de conexiones de la lista, o bien haga clic en \<**New connection...**> y use el cuadro de diálogo **Agregar administrador de conexiones de Analysis Services** para crear una nueva conexión.  
  
 **Temas relacionados:** [Referencia de la interfaz de usuario del cuadro de diálogo Agregar administrador de conexiones con Analysis Services](connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md), [Administrador de conexiones de Analysis Services](connection-manager/analysis-services-connection-manager.md)  
  
 **Tipo de origen**  
 Especifique el tipo de origen de las instrucciones de DDL. Esta propiedad presenta las opciones indicadas en la siguiente tabla:  
  
|Value|Descripción|  
|-----------|-----------------|  
|**Entrada directa**|Establezca en el cuadro de texto **SourceDirect** el origen de la instrucción DDL almacenada. Al seleccionar este valor se muestran las opciones dinámicas de la siguiente sección.|  
|**Conexión de archivos**|Establezca el origen de un archivo que contenga la instrucción DDL. Al seleccionar este valor se muestran las opciones dinámicas de la siguiente sección.|  
|**Variable**|Establezca el origen en una variable. Al seleccionar este valor se muestran las opciones dinámicas de la siguiente sección.|  
  
## <a name="dynamic-options"></a>Opciones dinámicas  
  
### <a name="sourcetype--direct-input"></a>SourceType = Entrada directa  
 **Origen**  
 Escriba las instrucciones de DDL o haga clic en los puntos suspensivos **(...)** y, a continuación, escriba las instrucciones en el cuadro de diálogo **instrucciones de DDL** .  
  
### <a name="sourcetype--file-connection"></a>SourceType = Conexión de archivos  
 **Origen**  
 Seleccione una conexión de archivo de la lista o haga clic en \<**New connection...**> y use el cuadro de diálogo **Administrador de conexiones de archivos** para crear una nueva conexión.  
  
 **Temas relacionados:** [Administrador de conexiones de archivos](connection-manager/file-connection-manager.md)  
  
### <a name="sourcetype--variable"></a>SourceType = Variable  
 **Origen**  
 Seleccione una variable de la lista o haga clic en \<**New variable...**> y use el cuadro de diálogo **Agregar variable** para crear una nueva variable.  
  
 **Temas relacionados:** [Variables de Integration Services &#40;SSIS&#41;](integration-services-ssis-variables.md)  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de errores y mensajes de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Analysis Services &#40;página general del editor de la tarea ejecutar DDL&#41;](general-page-of-integration-services-designers-options.md)   
 [Página expresiones](expressions/expressions-page.md)   
 [Flujo de control](control-flow/control-flow.md)   
 [Referencia de ASSL&#41; &#40;de lenguaje de scripting Analysis Services](https://docs.microsoft.com/bi-reference/assl/analysis-services-scripting-language-assl-for-xmla)   
 [Referencia XML for Analysis &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-for-analysis-xmla-reference)  
  
  
