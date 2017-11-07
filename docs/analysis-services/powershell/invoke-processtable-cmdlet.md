---
title: Cmdlet Invoke-ProcessTable | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 865e6d06-b99a-41f3-9d6f-c3c97b529b23
caps.latest.revision: 9
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d2298c9e882f3f754b16ce33bf6bc72dfc6d80ff
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="invoke-processtable-cmdlet"></a>Cmdlet Invoke-ProcessTable

[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  Lleva a cabo la operación **Process** en una **Table** con un valor concreto **RefreshType**.  

>[!NOTE] 
>En este artículo puede contener información no actualizada y ejemplos. Use el cmdlet Get-Help para la versión más reciente.
  
## <a name="syntax"></a>Sintaxis  
 `Invoke-ProcessTable [-DatabaseName] <string> [-TableName] <string> [-RefreshType] <RefreshType> {Full |     ClearValues | Calculate | DataOnly | Automatic | Add | Defragment} [-Server <string>] [-Credential <pscredential>     [-WhatIf] [-Confirm]  [<CommonParameters>]`  
  
 `Invoke-ProcessTable -RefreshType <RefreshType> {Full | ClearValues | Calculate | DataOnly | Automatic | Add |     Defragment} -Table <Table> [-Server <string>] [-Credential <pscredential>] [-WhatIf] [-Confirm]     [<CommonParameters>]`  
  
## <a name="parameters"></a>Parámetros  
  
### <a name="-tablename-string"></a>-TableName \<cadena >  
 Nombre de la tabla a la que pertenece la partición que debe procesarse.  
  
|||  
|-|-|  
|¿Requerido?|true|  
|¿Posición?|0|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-databasename-string"></a>-DatabaseName \<cadena >  
 Especifica la base de datos a la que la tabla pertenece.  
  
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
  
### <a name="-credential"></a>-Credential  
 Si se especifica este parámetro, el nombre de usuario y la contraseña que se pasan se usarán para conectarse a la instancia de Analysis Services. Si no se especifica ninguna credencial, se dará por supuesto que es la cuenta predeterminada de Windows del usuario que ejecuta el script.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-whatif"></a>-Whatif  
 Incluya este parámetro para obtener información sobre las repercusiones de la operación antes de ejecutarla.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-confirm"></a>-Confirm  
 Incluya este parámetro para confirmar interactivamente la operación con una respuesta Sí o No antes de ejecutarla.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?||  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?||  
|¿Aceptar caracteres comodín?|false|  
  
## <a name="example-1"></a>Ejemplo 1  
 `PS SQLSERVER:\SQLAS\MachineName\Instance\Databases\DB1\> Invoke-ProcessTable -TableName "myTable" -Database "DB1"  -RefreshType "Full"`  
  
 Este comando canaliza la identidad de la tabla que se va a procesar.  
  
## <a name="example-2"></a>Ejemplo 2  
 `PS SQLSERVER:\SQLAS\MachineName\Instance\Databases\DB1\> Invoke-ProcessTable -TableName "myTable" -Database "DB1"  -RefreshType [Microsoft.AnalysisServices.Tabular.RefreshType]::Full`  
  
 Este comando procesa una tabla de metadatos tabulares mediante un tipo de actualización **enum** .  
  
  

