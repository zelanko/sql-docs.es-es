---
title: CommandTypeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CommandTypeEnum
helpviewer_keywords:
- CommandTypeEnum enumeration [ADO]
ms.assetid: 4b1feb9c-a855-40fe-a906-efe688687e9f
author: rothja
ms.author: jroth
ms.openlocfilehash: 68572a642333e4e9c2c334cd7680b96b0cacced3
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82760381"
---
# <a name="commandtypeenum"></a>CommandTypeEnum
Especifica cómo debe interpretarse un argumento de comando.  
  
 Es importante validar los valores de *CommandString* proporcionados por el usuario para evitar que los usuarios de la aplicación tengan la oportunidad de insertar comandos potencialmente peligrosos para que ADO los ejecute.  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adCmdUnspecified**|-1|No especifica el argumento de tipo de comando.|  
|**adCmdText**|1|Evalúa [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) como una definición textual de un comando o una llamada a un procedimiento almacenado.|  
|**adCmdTable**|2|Evalúa **CommandText** como un nombre de tabla cuyas columnas son devueltas por una consulta SQL generada internamente.|  
|**adCmdStoredProc**|4|Evalúa **CommandText** como un nombre de procedimiento almacenado.|  
|**adCmdUnknown**|8|Predeterminada. Indica que no se conoce el tipo de comando en la propiedad **CommandText** .<br /><br /> Cuando no se conoce el tipo de comando, ADO realizará varios intentos de interpretar **CommandText**.<br /><br /> -   **CommandText** se interpreta como una definición textual de un comando o una llamada a un procedimiento almacenado. Este es el mismo comportamiento que **adCmdText**.<br />-   **CommandText** es el nombre de un procedimiento almacenado. Este comportamiento es el mismo que el de **adCmdStoredProc**.<br />-   **CommandText** se interpreta como el nombre de una tabla. Todas las columnas se devuelven mediante una consulta SQL generada internamente. Este comportamiento es el mismo que el de **adCmdTable**.|  
|**adCmdFile**|256|Evalúa **CommandText** como el nombre de archivo de un [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md)almacenado de forma persistente. Se usa con el **conjunto de registros.** Solo [abrir o volver](../../../ado/reference/ado-api/open-method-ado-recordset.md) a [consultar](../../../ado/reference/ado-api/requery-method.md) .|  
|**adCmdTableDirect**|512|Evalúa **CommandText** como un nombre de tabla cuyas columnas se devuelven todos. Se usa con **Recordset. Open** o solo **Requery** . Para utilizar el método [Seek](../../../ado/reference/ado-api/seek-method.md) , el **conjunto de registros** debe abrirse con **adCmdTableDirect**.<br /><br /> Este valor no se puede combinar con el valor **adAsyncExecute**de [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md) .|  
  
## <a name="adowfc-equivalent"></a>Equivalente de ADO/WFC  
 Paquete: **com. ms. wfc. Data**  
  
|Constante|  
|--------------|  
|AdoEnums. CommandType. no especificado|  
|AdoEnums. CommandType. TEXT|  
|AdoEnums. CommandType. TABLE|  
|AdoEnums. CommandType. STOREDPROC|  
|AdoEnums. CommandType. UNKNOWN|  
|AdoEnums. CommandType. FILE|  
|AdoEnums. CommandType. TABLEDIRECT|  
  
## <a name="applies-to"></a>Se aplica a  
  
|||  
|-|-|  
|[Propiedad CommandType (ADO)](../../../ado/reference/ado-api/commandtype-property-ado.md)|[Método Execute (Command ADO)](../../../ado/reference/ado-api/execute-method-ado-command.md)|  
|[Execute (método) (conexión de ADO)](../../../ado/reference/ado-api/execute-method-ado-connection.md)|[Open (método) (conjunto de registros ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md)|  
|[Requery (método)](../../../ado/reference/ado-api/requery-method.md)||
