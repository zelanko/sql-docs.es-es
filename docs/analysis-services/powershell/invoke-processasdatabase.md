---
title: ProcessASDatabase invocar | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 66d5d154-88ce-4c2e-b1ef-e2d2f6fb1c44
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f8e83493ed934a3f9bf32a1cef35969f04996223
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="invoke-processasdatabase"></a>Invoke-ProcessASDatabase

[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  Lleva a cabo la operación **Process** en un objeto **Database** especificado con un valor **ProcessType** o **RefreshType** determinado según el tipo subyacente de metadatos.  
  
 Use **ProcessType** para bases de datos con metadatos multidimensionales (esto incluye las bases de datos tabulares con nivel de compatibilidad 1050, 1100 o 1103).  
  
 Use **RefreshType** para bases de datos tabulares con el nivel de compatibilidad 1200 o superior.  

>[!NOTE] 
>En este artículo puede contener información no actualizada y ejemplos. Use el cmdlet Get-Help para la versión más reciente.
  
## <a name="syntax"></a>Sintaxis  
 `Invoke-ProcessASDatabase [-DatabaseName] <string> [-RefreshType] <RefreshType> {Full | ClearValues | Calculate |     DataOnly | Automatic | Add | Defragment} [-Server <string>] [-Credential <pscredential>] [-WhatIf] [-Confirm]     [<CommonParameters>]`  
  
 `Invoke-ProcessASDatabase [-DatabaseName] <string> [-ProcessType] <ProcessType> {ProcessFull | ProcessAdd |     ProcessUpdate | ProcessIndexes | ProcessData | ProcessDefault | ProcessClear | ProcessStructure |     ProcessClearStructureOnly | ProcessScriptCache | ProcessRecalc | ProcessDefrag} [-Server <string>] [-Credential     <pscredential>] [-WhatIf] [-Confirm]  [<CommonParameters>]`  
  
## <a name="description"></a>Description  
 El cmdlet **Invoke-ProcessASDatabase** procesa una base de datos al nivel especificado. Por ejemplo, en el caso de las bases de datos tabulares con el nivel de compatibilidad 1200, si establece **RefreshType** en **Full** se sobrescriben los datos existentes con todos los datos nuevos.  
  
 El tipo de procesamiento (multidimensional) o el tipo de actualización (tabular) es necesario y puede especificarse antes o después de los parámetros de base de datos y de servidor:  
  
-   Para más información sobre la opción multidimensional, vea [Configuración y opciones de procesamiento &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md).  
  
-   Para más información sobre la opción tabular, vea [Procesar base de datos, tabla o partición &#40;Analysis Services&#41;](../../analysis-services/tabular-models/process-database-table-or-partition-analysis-services.md).  
  
## <a name="parameters"></a>Parámetros  
  
### <a name="-databasename-string"></a>-DatabaseName \<cadena >  
 Especifica la base de datos tabular o multidimensional que se va a procesar.  
  
|||  
|-|-|  
|¿Requerido?|true|  
|¿Posición?|0|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-servermicrosoftanalysissevicesserver"></a>-Server\<Microsoft.AnalysisSevices.Server >  
 Opcionalmente, especifica la instancia del servidor al que se va a conectar si no usa el directorio del proveedor **SQLAS** para el contexto.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-refreshtype-microsoftanalysisservicesrefreshtype"></a>-RefreshType \<Microsoft.AnalysisServices.RefreshType >  
 Especifica el tipo de proceso para una base de datos Tabular.  Los valores válidos son Full, ClearValues, Calculate, DataOnly, Automatic, Add y Defragment. Vea [Procesar base de datos, tabla o partición &#40;Analysis Services&#41;](../../analysis-services/tabular-models/process-database-table-or-partition-analysis-services.md) para obtener descripciones e instrucciones.  
  
|||  
|-|-|  
|¿Requerido?|true|  
|¿Posición?|1|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-processtype-microsoftanalysisservicesprocesstype"></a>-ProcessType \<Microsoft.AnalysisServices.ProcessType >  
 Especifica el tipo de proceso para una base de datos multidimensional o tabular con los niveles de compatibilidad 1050-1103. Entre los valores válidos se incluyen ProcessFull, ProcessAdd, ProcessUpdate, ProcessIndexes, ProcessData, ProcessDefault, ProcessClear, ProcessStructure, ProcessCelarStructureOnly, ProcessScriptCache o ProcessRecalc. Vea [Configuración y opciones de procesamiento &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md) para obtener descripciones e instrucciones.  
  
|||  
|-|-|  
|¿Requerido?|true|  
|¿Posición?|1|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-credential"></a>-Credential  
 Si se especifica este parámetro, el nombre de usuario y la contraseña que se pasan se usarán para conectarse a la instancia de Analysis Services. Si no se especifica ninguna credencial, se dará por supuesto que es la cuenta predeterminada de Windows del usuario que ejecuta el script.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
## <a name="-whatif"></a>-Whatif  
 Incluya este parámetro para obtener información sobre las repercusiones de la operación antes de ejecutarla.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
## <a name="-confirm"></a>-Confirm  
 Incluya este parámetro para confirmar interactivamente la operación con una respuesta Sí o No antes de ejecutarla.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?||  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?||  
|¿Aceptar caracteres comodín?|false|  
  
## <a name="example-1-sqlas-provider"></a>Ejemplo 1 (proveedor SQLAS)  
 En este ejemplo se usa el proveedor **SQLAS** para establecer el contexto de la lista de bases de datos en una instancia predeterminada.  Si enumera el contenido del directorio de las bases de datos, verá todas las bases de datos junto con su estado de proceso y el modo de lectura y escritura.  
  
 Desde la carpeta de la base de datos, puede ejecutar **Invoke-ProcessASDatabase** especificando únicamente el nombre de la base de datos.  
  
```  
PS > import-module SQLPS -DisableNameChecking  
PS  SQL Server > cd sqlas\ssas-srv-01\default\databases  
PS SQLSERVER:\sqlas\ssas-srv-01\default\databases> dir  
. . . .  
PS SQLSERVER:\sqlas\ssas-srv-01\default\databases> Invoke-ProcessASDatabase "adventureworks"  
  
```  
  
 Según cuál sea tipo de base de datos, se le pedirá que especifique un **RefreshType** o un **ProcessType**.  
  
 Una prueba del procesamiento es la presencia de un objeto de impacto en la instrucción return: Microsoft.AnalysisServices.Tabular.ObjectImpact.  
  
 Tenga en cuenta que, a veces, se almacena en caché información de estado del objeto; así pues, si muestra en una lista el contenido de un directorio después de que el procesamiento se realice correctamente, el estado de la base de datos conservará su descriptor "sin procesar" original. Esto puede resultar confuso, puesto que la devolución del objeto Impact significa que la base de datos se ha procesado.  
  
 Para confirmar que el procesamiento se ha realizado correctamente, vea la página de propiedades de la base de datos en Management Studio, inicie una sesión nueva o devuelva el estado de procesamiento de un objeto de base de datos (a través de [Microsoft.AnalysisServices.ProcessableMajorObject.LastProcessed](https://msdn.microsoft.com/library/microsoft.analysisservices.processablemajorobject.lastprocessed.aspx)).  
  
## <a name="example-2"></a>Ejemplo 2  
 En este ejemplo se muestra la misma operación usando solo el cmdlet sin el proveedor. Se requieren parámetros adicionales para especificar el tipo de servidor y de proceso.  
  
```  
PS > import-module SQLPS -DisableNameChecking  
PS  SQL Server >  Invoke-ProcessASDatabase -databasename "AdventureWorks" -server '\\server-name\instancename' –ProcessType "ProcessFull"  
  
```  
  
  
  
