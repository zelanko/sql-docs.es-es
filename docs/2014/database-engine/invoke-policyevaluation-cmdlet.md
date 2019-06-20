---
title: Cmdlet Invoke-PolicyEvaluation | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, Invoke-PolicyEvaluation
- Policy-Based Management, PowerShell
- Invoke-PolicyEvaluation cmdlet
- Cmdlets [SQL Server], Invoke-PolicyEvaluation
- PowerShell [SQL Server], Invoke-PolicyEvaluation
ms.assetid: 3e6d4f5a-59b7-4203-b95a-f7e692c0f131
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c1239d2dea1a4f73b54f78345f769c9550c262b9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66064692"
---
# <a name="invoke-policyevaluation-cmdlet"></a>cmdlet Invoke-PolicyEvaluation
  **Invoke-PolicyEvaluation** es un cmdlet de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que notifica si un conjunto de destino de objetos de SQL Server cumple las condiciones especificadas en una o más directivas de administración basada en directivas.  
  
## <a name="using-invoke-policyevaluation"></a>Uso de Invoke-PolicyEvaluation  
 **Invoke-PolicyEvaluation** evalúa una o mas directivas comparándolas con un conjunto de objetos de SQL Server que se conoce como el conjunto de destino. Los objetos del conjunto de destino provienen de un servidor de destino. Cada directiva define condiciones, que son los estados permitidos de los objetos de destino. Por ejemplo, la directiva **Trustworthy Database** indica que la propiedad de base de datos TRUSTWORTHY se debe establecer como OFF.  
  
 El parámetro **-AdHocPolicyEvaluationMode** especifica las acciones realizadas:  
  
 Comprobación  
 Informa del estado de cumplimiento de los objetos de destino mediante las credenciales del inicio de sesión actual. No configure ningún objeto. Esta es la configuración predeterminada.  
  
 CheckSqlScriptAsProxy  
 Informa del estado de cumplimiento de los objetos de destino mediante las credenciales del inicio de sesión de proxy **##MS_PolicyTSQLExecutionLogin##** . No configure ningún objeto.  
  
 Configurar  
 Informa del estado de cumplimiento de los objetos de destino mediante las credenciales del inicio de sesión actual. Vuelva a configurar cualquier opción que se pueda establecer y que sea determinista que no cumpla las directivas.  
  
## <a name="specifying-polices"></a>Especificar directivas  
 La forma en la que se especifica una directiva depende de su ubicación de almacenamiento. Las directivas se pueden almacenar en dos formatos:  
  
-   Pueden ser objetos almacenados en un almacén de directivas, como una instancia del motor de base de datos. Puede usar la carpeta SQLSERVER:\SQLPolicy para especificar la ubicación de las directivas en un almacén de directivas. Puede usar los cmdlets de Windows PowerShell para filtrar las directivas de entrada basándose en sus propiedades, como el uso de Where-Object para filtrar por categoría de directiva o Get-Item para hacerlo por nombre de directiva.  
  
-   Se pueden exportar como archivos XML. Puede utilizar una unidad de disco del sistema de archivos, como D:, para especificar la ubicación de los archivos XML. Puede usar los cmdlets de Windows PowerShell como Where-Object para filtrar las directivas por sus propiedades de archivo, como nombre de archivo.  
  
 Si las directivas se almacenan en un almacén de directivas, debe pasar un conjunto de PSObjects que señalen a las directivas que se van a evaluar. Esto se suele realizar mediante la canalización de la salida de un cmdlet como Get-Item a **Invoke-PolicyEvaluation**y no requiere que se especifique el parámetro **-Policy** . Por ejemplo, si ha importado las directivas de las prácticas recomendadas de Microsoft a la instancia del motor de base de datos, este comando evalúa la directiva **Database Status** :  
  
```  
sl "SQLSERVER:\SQLPolicy\MyComputer\DEFAULT\Policies"  
Get-Item "Database Status" | Invoke-PolicyEvaluation -TargetServerName "MYCOMPUTER"  
```  
  
 En este ejemplo se muestra el uso de Where-Object para filtrar varias directivas de un almacén de directivas en función de su propiedad **PolicyCategory** . **Invoke-PolicyEvaluation** usa los objetos de la salida canalizada de **Where-Object**.  
  
```  
sl "SQLSERVER:\SQLPolicy\MyComputer\DEFAULT\Policies"  
gci | Where-Object {$_.PolicyCategory -eq "Microsoft Best Practices: Maintenance"} | Invoke-PolicyEvaluation -TargetServer "MYCOMPUTER"  
```  
  
 Si las directivas se almacenan como archivos XML, debe usar el parámetro **-Policy** para proporcionar tanto la ruta de acceso como el nombre de cada directiva. Si no especifica una ruta de acceso en el parámetro **-Policy** , **Invoke-PolicyEvaulation** usa el valor actual de la ruta de acceso **sqlps** . Por ejemplo, este comando evalúa una de las directivas de las prácticas recomendadas de Microsoft instalada con SQL Server comparándola con la base de datos predeterminada para el inicio de sesión:  
  
```  
Invoke-PolicyEvaluation -Policy "C:\Program Files\Microsoft SQL Server\120\Tools\Policies\DatabaseEngine\1033\Database Status.xml" -TargetServerName "MYCOMPUTER"  
```  
  
 Este comando realiza la misma acción, pero usa la ruta de acceso de **sqlps** actual para establecer la ubicación del archivo XML de directivas:  
  
```  
sl "C:\Program Files\Microsoft SQL Server\120\Tools\Policies\DatabaseEngine\1033"  
Invoke-PolicyEvaluation -Policy "Database Status.xml" -TargetServerName "MYCOMPUTER"  
```  
  
 En este ejemplo se muestra el empleo del cmdlet **Get-ChildItem** para recuperar varios archivos XML de directivas y canalizar los objetos a **Invoke-PolicyEvaluation**:  
  
```  
sl "C:\Program Files\Microsoft SQL Server\120\Tools\Policies\DatabaseEngine\1033"  
gci "Database Status.xml", "Trustworthy Database.xml" | Invoke-PolicyEvaluation -TargetServer "MYCOMPUTER"  
```  
  
## <a name="specifying-the-target-set"></a>Especificar el conjunto de destino  
 Use tres parámetros para especificar el conjunto de objetos de destino:  
  
-   **-TargetServerName** especifica la instancia de SQL Server que contiene los objetos de destino. Puede especificar la información en una cadena con el formato definido para la propiedad ConnectionString de la clase <xref:System.Data.SqlClient.SqlConnection> . Puede usar la clase <xref:System.Data.SqlClient.SqlConnectionStringBuilder> para generar una cadena de conexión con el formato correcto. También puede crear un objeto <xref:Microsoft.SqlServer.Management.Sdk.Sfc.SqlStoreConnection> y pasarlo a **-TargetServer**. Si proporciona una cadena que solo contiene el nombre del servidor, **Invoke-PolicyEvaluation** usa autenticación de Windows para conectar con el servidor.  
  
-   **-TargetObjects** toma un objeto o una matriz de objetos que representa a los objetos de SQL Server del conjunto de destino. Por ejemplo, podría crear una matriz de objetos de la clase <xref:Microsoft.SqlServer.Management.Smo.Database> para pasarlos a **-TargetObjects**.  
  
-   **-TargetExpressions** toma una cadena que contiene una expresión de consulta que especifica los objetos del conjunto de destino. La expresión de consulta tiene el formato de los nodos separados por el carácter '/'. Cada nodo tiene el formato ObjectType[Filter]. El tipo de objeto es uno de los objetos de una jerarquía de objetos de los Objetos de administración de SQL Server (SMO). Filter es una expresión que filtra los objetos de ese nodo. Para más información, consulte [Query Expressions and Uniform Resource Names](../powershell/query-expressions-and-uniform-resource-names.md).  
  
 Especifique **-TargetObjects** o **-TargetExpression**, no ambos.  
  
 En este ejemplo se usa un objeto Sfc.SqlStoreConnection para especificar el servidor de destino:  
  
```  
sl "C:\Program Files\Microsoft SQL Server\120\Tools\Policies\DatabaseEngine\1033"  
$conn = New-Object Microsoft.SqlServer.Management.Sdk.Sfc.SqlStoreConnection("server='MYCOMPUTER';Trusted_Connection=True")  
Invoke-PolicyEvaluation -Policy "Database Status.xml" -TargetServerName $conn  
```  
  
 En este ejemplo se usa **-TargetExpression** para identificar la base de datos concreta que se va a evaluar:  
  
```  
sl "C:\Program Files\Microsoft SQL Server\120\Tools\Policies\DatabaseEngine\1033"  
Invoke-PolicyEvaluation -Policy "Database Status.xml" -TargetServerName "MyComputer" -TargetExpression "Server[@Name='MYCOMPUTER']/Database[@Name='AdventureWorks2012']"  
```  
  
## <a name="evaluating-analysis-services-policies"></a>Evaluar las directivas de Analysis Services  
 Para evaluar las directivas comparándolas con una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], debe cargar y registrar un ensamblado en PowerShell, crear una variable con un objeto de conexión de Analysis Services y pasársela al parámetro **-TargetObject** . En este ejemplo se muestra cómo evaluar la directiva de configuración de área expuesta de las prácticas recomendadas de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]:  
  
```  
sl "C:\Program Files\Microsoft SQL Server\120\Tools\Policies\AnalysisServices\1033"  
[System.Reflection.Assembly]::LoadWithPartialName("Microsoft.AnalysisServices")  
$SSASsvr = new-object Microsoft.AnalysisServices.Server  
$SSASsvr.Connect("Data Source=Localhost")  
Invoke-PolicyEvaluation -Policy "Surface Area Configuration for Analysis Services Features.xml" -TargetObject $SSASsvr  
```  
  
## <a name="evaluating-reporting-services-policies"></a>Evaluar las directivas de Reporting Services  
 Para evaluar las directivas de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] , debe cargar y registrar un ensamblado en PowerShell, crear una variable con un objeto de conexión de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] y pasársela al parámetro **-TargetObject** . En este ejemplo se muestra cómo evaluar la directiva de configuración de área expuesta de las prácticas recomendadas de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]:  
  
```  
sl "C:\Program Files\Microsoft SQL Server\120\Tools\Policies\ReportingServices\1033"  
[System.Reflection.Assembly]::LoadWithPartialName("Microsoft.SqlServer.Dmf.Adapters")  
$SSRSsvr = new-object Microsoft.SqlServer.Management.Adapters.RSContainer('MyComputer')  
Invoke-PolicyEvaluation -Policy "Surface Area Configuration for Reporting Services 2008 Features.xml" -TargetObject $SSRSsvr  
```  
  
## <a name="formatting-output"></a>Dar formato a los resultados  
 De forma predeterminada, la salida de **Invoke-PolicyEvaluation** se muestra en la ventana del símbolo del sistema como informe conciso en formato legible. Puede usar el parámetro **-OutputXML** para especificar que el cmdlet genere un informe detallado como archivo XML. **Invoke-PolicyEvaluation** usa el esquema SML-IF (Systems Modeling Language Interchange Format) para que los lectores SML-IF puedan leer el archivo.  
  
```  
sl "SQLSERVER:\SQLPolicy\MyComputer\DEFAULT\Policies"  
Invoke-PolicyEvaluation -Policy "Datbase Status" -TargetServer "MYCOMPUTER" -OutputXML > C:\MyReports\DatabaseStatusReport.xml  
```  
  
## <a name="see-also"></a>Vea también  
 [Utilizar los cmdlets del motor de base de datos](../../2014/database-engine/use-the-database-engine-cmdlets.md)  
  
  
