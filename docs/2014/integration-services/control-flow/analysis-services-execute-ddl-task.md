---
title: Tarea Ejecutar DDL de Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.asexecuteddltask.f1
helpviewer_keywords:
- Analysis Services Execute DDL task
- DDL
ms.assetid: 7f25c8c6-b601-41f2-9553-be0a2ee0751a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: a74ab896e974410e8357a22546cb63ed7365a149
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62833160"
---
# <a name="analysis-services-execute-ddl-task"></a>Tarea Ejecutar DDL de Analysis Services
  La tarea Ejecutar DDL de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ejecuta instrucciones del lenguaje de definición de datos (DDL) que pueden crear, quitar o modificar modelos de minería de datos y objetos multidimensionales, como cubos y dimensiones. Por ejemplo, una instrucción DDL puede crear una partición en el cubo de **Adventure Works** o eliminar una dimensión de [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)], la base de datos de ejemplo de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] incluida en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 La tarea Ejecutar DDL de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] utiliza un administrador de conexiones de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para conectar con una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Para más información, consulte [Analysis Services Connection Manager](../connection-manager/analysis-services-connection-manager.md).  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] incluye diversas tareas que realizan operaciones de Business Intelligence, como procesamiento de objetos de análisis y la ejecución de consultas de predicción de minería de datos.  
  
 Para obtener más información sobre tareas de Business Intelligence relacionadas, haga clic en uno de los temas siguientes:  
  
-   [Tarea de procesamiento de Analysis Services](analysis-services-processing-task.md)  
  
-   [Tarea Consulta de minería de datos](data-mining-query-task.md)  
  
## <a name="ddl-statements"></a>Instrucciones DDL  
 Las instrucciones de DDL se representan como instrucciones del Lenguaje de scripting de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] (ASSL) y se generan como comandos de XML for Analysis (XMLA).  
  
-   ASSL se usa para definir y describir una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , así como las bases de datos y los objetos de base de datos que contiene. Para obtener más información, vea [Analysis Services scripting Language &#40;ASSL&#41; Reference](https://docs.microsoft.com/bi-reference/assl/analysis-services-scripting-language-assl-for-xmla).  
  
-   XMLA es un lenguaje de comandos que se usa para enviar comandos de acción, como Create, Alter o Process, a una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Para más información, vea [Referencia XML for Analysis &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-for-analysis-xmla-reference).  
  
 Si se almacena el código de DDL en un archivo independiente, la tarea Ejecutar DDL de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] utiliza un administrador de conexiones de archivos para especificar la ruta del archivo. Para obtener más información, consulte [File Connection Manager](../connection-manager/file-connection-manager.md).  
  
 Como las instrucciones de DDL pueden contener contraseñas y otros datos confidenciales, un paquete que contenga una o varias tareas Ejecutar DDL de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] debe usar el nivel de protección de paquetes `EncryptAllWithUserKey` o `EncryptAllWithPassword`. Para obtener más información, vea [Paquetes de Integration Services &#40;SSIS&#41;](../integration-services-ssis-packages.md).  
  
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
  
 Para obtener más información acerca de las propiedades que puede establecer en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en uno de los temas siguientes:  
  
-   [Analysis Services &#40;página general del editor de la tarea ejecutar DDL&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [Analysis Services ejecutar el editor de la tarea DDL &#40;página DDL&#41;](../analysis-services-execute-ddl-task-editor-ddl-page.md)  
  
-   [Página Expresiones](../expressions/expressions-page.md)  
  
 Para obtener más información sobre cómo configurar estas propiedades en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en el siguiente tema:  
  
-   [Establecer las propiedades de tareas o contenedores](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="programmatic-configuration-of-the-analysis-services-execute-ddl-task"></a>Configuración mediante programación de la tarea Ejecutar DDL de Analysis Services  
 Para obtener más información sobre cómo establecer estas propiedades mediante programación, haga clic en el tema siguiente:  
  
-   <xref:Microsoft.DataTransformationServices.Tasks.DTSProcessingTask.ASExecuteDDLTask>  
  
  
