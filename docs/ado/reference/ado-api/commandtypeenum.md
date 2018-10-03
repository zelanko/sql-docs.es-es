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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5ff7b6ecf919ab83340e49e4395f8c2d1701261d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47742883"
---
# <a name="commandtypeenum"></a>CommandTypeEnum
Especifica cómo se debe interpretar un argumento de comando.  
  
 Es importante validar proporcionado por el usuario *CommandString* valores para no dar a los usuarios de la aplicación la posibilidad de insertar comandos potencialmente peligrosos de ADO ejecutar.  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adCmdUnspecified**|-1|No se especifica el argumento de tipo de comando.|  
|**adCmdText**|1|Se evalúa como [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) como una definición textual de un comando o procedimiento almacenado llamar.|  
|**adCmdTable**|2|Se evalúa como **CommandText** como un nombre de tabla cuyas columnas se devuelven mediante una consulta SQL generada internamente.|  
|**adCmdStoredProc**|4|Se evalúa como **CommandText** como un nombre de procedimiento almacenado.|  
|**adCmdUnknown**|8|Predeterminado: Indica que el tipo de comando en el **CommandText** propiedad no se conoce.<br /><br /> Cuando se desconoce el tipo de comando, ADO realiza varios intentos para interpretar el **CommandText**.<br /><br /> -   **CommandText** se interpreta como una definición textual de una llamada de comando o procedimiento almacenado. Este es el mismo comportamiento que **adCmdText**.<br />-   **CommandText** es el nombre de un procedimiento almacenado. Este es el mismo comportamiento que **adCmdStoredProc**.<br />-   **CommandText** se interpreta como el nombre de una tabla. Todas las columnas se devuelven mediante una consulta SQL generada internamente. Este es el mismo comportamiento que **adCmdTable**.|  
|**adCmdFile**|256|Se evalúa como **CommandText** como el nombre de archivo de una forma persistente almacenado [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md). Puede usar con **Recordset.** [Abierto](../../../ado/reference/ado-api/open-method-ado-recordset.md) o [Requery](../../../ado/reference/ado-api/requery-method.md) solo.|  
|**adCmdTableDirect**|512|Se evalúa como **CommandText** como un nombre de tabla cuyas columnas se devuelven. Puede usar con **Recordset.Open** o **Requery** solo. Para usar el [Seek](../../../ado/reference/ado-api/seek-method.md) método, el **Recordset** debe abrirse con **adCmdTableDirect**.<br /><br /> Este valor no puede combinarse con el [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md) valor **adAsyncExecute**.|  
  
## <a name="adowfc-equivalent"></a>Equivalente de ADO y WFC  
 Paquete: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.CommandType.UNSPECIFIED|  
|AdoEnums.CommandType.TEXT|  
|AdoEnums.CommandType.TABLE|  
|AdoEnums.CommandType.STOREDPROC|  
|AdoEnums.CommandType.UNKNOWN|  
|AdoEnums.CommandType.FILE|  
|AdoEnums.CommandType.TABLEDIRECT|  
  
## <a name="applies-to"></a>Se aplica a  
  
|||  
|-|-|  
|[Propiedad CommandType (ADO)](../../../ado/reference/ado-api/commandtype-property-ado.md)|[Método Execute (Command ADO)](../../../ado/reference/ado-api/execute-method-ado-command.md)|  
|[Execute (método) (conexión de ADO)](../../../ado/reference/ado-api/execute-method-ado-connection.md)|[Open (método) (conjunto de registros ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md)|  
|[Requery (método)](../../../ado/reference/ado-api/requery-method.md)||
