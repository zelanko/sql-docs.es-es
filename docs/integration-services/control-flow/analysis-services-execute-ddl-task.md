---
title: Tarea Ejecutar DDL de Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.asexecuteddltask.f1
- sql13.dts.designer.asexecuteddltask.general.f1
- sql13.dts.designer.asexecuteddltask.ddl.f1
helpviewer_keywords:
- Analysis Services Execute DDL task
- DDL
ms.assetid: 7f25c8c6-b601-41f2-9553-be0a2ee0751a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: cce0b8606b398d1c72b70c161bb8ccdf0d779167
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/16/2019
ms.locfileid: "65728060"
---
# <a name="analysis-services-execute-ddl-task"></a>Tarea Ejecutar DDL de Analysis Services

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  La tarea Ejecutar DDL de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ejecuta instrucciones del lenguaje de definición de datos (DDL) que pueden crear, quitar o modificar modelos de minería de datos y objetos multidimensionales, como cubos y dimensiones. Por ejemplo, una instrucción DDL puede crear una partición en el cubo de **Adventure Works** o eliminar una dimensión de [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)], la base de datos de ejemplo de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] incluida en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 La tarea Ejecutar DDL de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] utiliza un administrador de conexiones de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para conectar con una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Para más información, consulte [Analysis Services Connection Manager](../../integration-services/connection-manager/analysis-services-connection-manager.md).  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] incluye diversas tareas que realizan operaciones de Business Intelligence, como procesamiento de objetos de análisis y la ejecución de consultas de predicción de minería de datos.  
  
 Para obtener más información sobre tareas de Business Intelligence relacionadas, haga clic en uno de los temas siguientes:  
  
-   [Tarea de procesamiento de Analysis Services](../../integration-services/control-flow/analysis-services-processing-task.md)  
  
-   [Tarea Consulta de minería de datos](../../integration-services/control-flow/data-mining-query-task.md)  
  
## <a name="ddl-statements"></a>Instrucciones DDL  
 Las instrucciones de DDL se representan como instrucciones del Lenguaje de scripting de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] (ASSL) y se generan como comandos de XML for Analysis (XMLA).  
  
-   ASSL se usa para definir y describir una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , así como las bases de datos y los objetos de base de datos que contiene. Para más información, vea [Referencia de Analysis Services Scripting Language &#40;ASSL&#41;](../../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md).  
  
-   XMLA es un lenguaje de comandos que se usa para enviar comandos de acción, como Create, Alter o Process, a una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Para más información, vea [Referencia XML for Analysis &#40;XMLA&#41;](../../analysis-services/xmla/xml-for-analysis-xmla-reference.md).  
  
 Si se almacena el código de DDL en un archivo independiente, la tarea Ejecutar DDL de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] utiliza un administrador de conexiones de archivos para especificar la ruta del archivo. Para más información, consulte [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md).  
  
 Como las instrucciones de DDL pueden contener contraseñas y otra información confidencial, un paquete que contenga una o varias tareas Ejecutar DDL de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] debe usar el nivel de protección de paquetes **EncryptAllWithUserKey** o **EncryptAllWithPassword**. Para obtener más información, vea [Paquetes de Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-packages.md).  
  
### <a name="ddl-examples"></a>Ejemplos de DDL  
 Las tres instrucciones DDL siguientes se generaron mediante objetos de scripting de [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)], la base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] incluida en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 La siguiente instrucción DDL elimina la dimensión **Promotion** .  
  
```  
<Delete xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
    <Object>  
        <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
        <DimensionID>Dim Promotion</DimensionID>  
    </Object>  
</Delete>  
  
```  
  
 La siguiente instrucción DDL procesa el cubo de [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] .  
  
```  
<Batch xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
  <Parallel>  
    <Process xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
      <Object>  
        <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
      </Object>  
      <Type>ProcessFull</Type>  
      <WriteBackTableCreation>UseExisting</WriteBackTableCreation>  
    </Process>  
  </Parallel>  
</Batch>  
  
```  
  
 La siguiente instrucción DDL crea el modelo de minería **Forecasting** .  
  
```  
<Create xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
    <ParentObject>  
        <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
        <MiningStructureID>Forecasting</MiningStructureID>  
    </ParentObject>  
    <ObjectDefinition>  
        <MiningModel xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
            <ID>Forecasting</ID>  
            <Name>Forecasting</Name>  
            <Algorithm>Microsoft_Time_Series</Algorithm>  
            <AlgorithmParameters>  
                <AlgorithmParameter>  
                    <Name>PERIODICITY_HINT</Name>  
                    <Value xsi:type="xsd:string">{12}</Value>  
                </AlgorithmParameter>  
            </AlgorithmParameters>  
            <Columns>  
                <Column>  
                    <ID>Amount</ID>  
                    <Name>Amount</Name>  
                    <SourceColumnID>Amount</SourceColumnID>  
                    <Usage>Predict</Usage>  
                </Column>  
                <Column>  
                    <ID>Model Region</ID>  
                    <Name>Model Region</Name>  
                    <SourceColumnID>Model Region</SourceColumnID>  
                    <Usage>Key</Usage>  
                </Column>  
                <Column>  
                    <ID>Quantity</ID>  
                    <Name>Quantity</Name>  
                    <SourceColumnID>Quantity</SourceColumnID>  
                    <Usage>Predict</Usage>  
                </Column>  
                <Column>  
                    <ID>Time Index</ID>  
                    <Name>Time Index</Name>  
                    <SourceColumnID>Time Index</SourceColumnID>  
                    <Usage>Key</Usage>  
                </Column>  
            </Columns>  
            <Collation>Latin1_General_CS_AS_KS</Collation>  
        </MiningModel>  
    </ObjectDefinition>  
</Create>  
  
```  
  
 Las tres instrucciones DDL siguientes se generaron mediante objetos de scripting de [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)], la base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] incluida en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 La siguiente instrucción DDL elimina la dimensión **Promotion** .  
  
```  
<Delete xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
    <Object>  
        <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
        <DimensionID>Dim Promotion</DimensionID>  
    </Object>  
</Delete>  
  
```  
  
 La siguiente instrucción DDL procesa el cubo de [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] .  
  
```  
<Batch xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
  <Parallel>  
    <Process xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
      <Object>  
        <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
      </Object>  
      <Type>ProcessFull</Type>  
      <WriteBackTableCreation>UseExisting</WriteBackTableCreation>  
    </Process>  
  </Parallel>  
</Batch>  
  
```  
  
 La siguiente instrucción DDL crea el modelo de minería **Forecasting** .  
  
```  
<Create xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
    <ParentObject>  
        <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
        <MiningStructureID>Forecasting</MiningStructureID>  
    </ParentObject>  
    <ObjectDefinition>  
        <MiningModel xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
            <ID>Forecasting</ID>  
            <Name>Forecasting</Name>  
            <Algorithm>Microsoft_Time_Series</Algorithm>  
            <AlgorithmParameters>  
                <AlgorithmParameter>  
                    <Name>PERIODICITY_HINT</Name>  
                    <Value xsi:type="xsd:string">{12}</Value>  
                </AlgorithmParameter>  
            </AlgorithmParameters>  
            <Columns>  
                <Column>  
                    <ID>Amount</ID>  
                    <Name>Amount</Name>  
                    <SourceColumnID>Amount</SourceColumnID>  
                    <Usage>Predict</Usage>  
                </Column>  
                <Column>  
                    <ID>Model Region</ID>  
                    <Name>Model Region</Name>  
                    <SourceColumnID>Model Region</SourceColumnID>  
                    <Usage>Key</Usage>  
                </Column>  
                <Column>  
                    <ID>Quantity</ID>  
                    <Name>Quantity</Name>  
                    <SourceColumnID>Quantity</SourceColumnID>  
                    <Usage>Predict</Usage>  
                </Column>  
                <Column>  
                    <ID>Time Index</ID>  
                    <Name>Time Index</Name>  
                    <SourceColumnID>Time Index</SourceColumnID>  
                    <Usage>Key</Usage>  
                </Column>  
            </Columns>  
            <Collation>Latin1_General_CS_AS_KS</Collation>  
        </MiningModel>  
    </ObjectDefinition>  
</Create>  
  
```  
  
## <a name="configuration-of-the-analysis-services-execute-ddl-task"></a>Configuración de la tarea Ejecutar DDL de Analysis Services  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información acerca de las propiedades que puede establecer en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en el tema siguiente:  
  
-   [Página Expresiones](../../integration-services/expressions/expressions-page.md)  
  
 Para obtener más información sobre cómo configurar estas propiedades en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en el siguiente tema:  
  
-   [Establecer las propiedades de tareas o contenedores](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="programmatic-configuration-of-the-analysis-services-execute-ddl-task"></a>Configuración mediante programación de la tarea Ejecutar DDL de Analysis Services  
 Para obtener más información sobre cómo establecer estas propiedades mediante programación, haga clic en el tema siguiente:  
  
-   <xref:Microsoft.DataTransformationServices.Tasks.DTSProcessingTask.ASExecuteDDLTask>  
  
## <a name="analysis-services-execute-ddl-task-editor-general-page"></a>Editor de la tarea Ejecutar DDL de Analysis Services (página General)
  Use la página **General** del cuadro de diálogo **Editor de la tarea Ejecutar DDL de Analysis Services** para nombrar y describir la tarea Ejecutar DDL de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
### <a name="options"></a>Opciones  
 **Nombre**  
 Proporcione un nombre único para la tarea Ejecutar DDL de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Este nombre se utiliza como etiqueta en el icono de tarea.  
  
> [!NOTE]  
>  Los nombres de tarea deben ser únicos en un paquete.  
  
 **Descripción**  
 Escriba una descripción de la tarea Ejecutar DDL de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
## <a name="analysis-services-execute-ddl-task-editor-ddl-page"></a>Editor de la tarea Ejecutar DDL de Analysis Services (página DDL)
  Use la página **DDL** del cuadro de diálogo **Editor de la tarea Ejecutar DDL de Analysis Services** para especificar una conexión a un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y proporcionar información sobre el origen de las instrucciones del lenguaje de definición de datos (DDL).  
  
### <a name="static-options"></a>Opciones estáticas  
 **Conexión**  
 Seleccione un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o un administrador de conexiones de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en la lista, o bien haga clic en \<**Nueva conexión…**> y use el cuadro de diálogo **Agregar administrador de conexiones de Analysis Services** para crear una conexión.  
  
 **Temas relacionados:** [Referencia de la interfaz de usuario del cuadro de diálogo Agregar administrador de conexiones con Analysis Services](../../integration-services/connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md), [Administrador de conexiones de Analysis Services](../../integration-services/connection-manager/analysis-services-connection-manager.md)  
  
 **Tipo de origen**  
 Especifique el tipo de origen de las instrucciones de DDL. Esta propiedad presenta las opciones indicadas en la siguiente tabla:  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**Entrada directa**|Establezca en el cuadro de texto **SourceDirect** el origen de la instrucción DDL almacenada. Al seleccionar este valor se muestran las opciones dinámicas de la siguiente sección.|  
|**Conexión de archivos**|Establezca el origen de un archivo que contenga la instrucción DDL. Al seleccionar este valor se muestran las opciones dinámicas de la siguiente sección.|  
|**Variable**|Establezca el origen en una variable. Al seleccionar este valor se muestran las opciones dinámicas de la siguiente sección.|  
  
### <a name="dynamic-options"></a>Opciones dinámicas  
  
#### <a name="sourcetype--direct-input"></a>SourceType = Entrada directa  
 **Source**  
 Escriba las instrucciones de DDL, o bien haga clic en el botón de puntos suspensivos **(…)** y, después, escriba las instrucciones en el cuadro de diálogo **Instrucciones DDL**.  
  
#### <a name="sourcetype--file-connection"></a>SourceType = Conexión de archivos  
 **Source**  
 Seleccione una conexión de archivos de la lista, o bien haga clic en \<**Nueva conexión…**> y use el cuadro de diálogo **Administrador de conexiones de archivos** para crear una conexión.  
  
 **Temas relacionados:** [Administrador de conexiones de archivos](../../integration-services/connection-manager/file-connection-manager.md)  
  
#### <a name="sourcetype--variable"></a>SourceType = Variable  
 **Source**  
 Seleccione una variable de la lista, o bien haga clic en \<**Nueva variable…**> y use el cuadro de diálogo **Agregar variable** para crear una variable.  
  
 **Temas relacionados:** [Variables de Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md)  
  
