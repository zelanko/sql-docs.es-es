---
title: Ejecutar el método (conexión de ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::Execute
- Connection15::raw_Execute
helpviewer_keywords:
- Execute method [ADO]
ms.assetid: 03c69320-96b2-4d85-8d49-a13b13e31578
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 0489bb43ee3b41ebf4334da0d6b8045e117acc39
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66695377"
---
# <a name="execute-method-ado-connection"></a>Execute (método) (conexión de ADO)
Ejecuta la consulta especificada, instrucción SQL, procedimiento almacenado o texto específico del proveedor.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Set recordset = connection.Execute (CommandText, RecordsAffected, Options)  
Set recordset = connection.Execute (CommandText, RecordsAffected, Options)  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve un [conjunto de registros ADO (objetos)](../../../ado/reference/ado-api/recordset-object-ado.md) referencia de objeto.  
  
#### <a name="parameters"></a>Parámetros  
 *CommandText*  
 Un **cadena** valor que contiene la instrucción SQL, el procedimiento almacenado, una dirección URL o el texto específico del proveedor para ejecutar. **Opcionalmente,** , se pueden usar los nombres de tabla, pero solo si el proveedor es compatible con SQL. Por ejemplo si un nombre de tabla de "Clientes" se utiliza, ADO antepondrá automáticamente la sintaxis estándar Select de SQL para formar y pasar "SELECT * FROM Customers" como un [!INCLUDE[tsql](../../../includes/tsql-md.md)] instrucción al proveedor.  
  
 *RecordsAffected*  
 Opcional. Un **largo** variable a la que el proveedor devuelve el número de registros que se ven afectados por la operación.  
  
 *Opciones*  
 Opcional. Un **largo** valor que indica cómo el proveedor debe evaluar el argumento CommandText. Puede ser una máscara de bits de uno o varios [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) o [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md) valores.  
  
 **Tenga en cuenta** uso el **ExecuteOptionEnum** valor **adExecuteNoRecords** para mejorar el rendimiento, ya que minimiza el procesamiento interno y para las aplicaciones que se va a trasladar desde Visual Basic 6.0.  
  
 No use **adExecuteStream** con el **Execute** método de un **conexión** objeto.  
  
 No utilice los valores adCmdFile ni adCmdTableDirect con Execute. Solo se pueden usar estos valores como opciones con la [método Open (ADO Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md) y [método Requery](../../../ado/reference/ado-api/requery-method.md) métodos de un **Recordset**.  
  
## <a name="remarks"></a>Comentarios  
 Mediante el **Execute** método en un [conexión ADO (objetos)](../../../ado/reference/ado-api/connection-object-ado.md) objeto ejecuta cualquier consulta que se pase al método en el argumento CommandText en la conexión especificada. Si el argumento CommandText especifica una consulta que devuelva filas, los resultados que genera la ejecución se almacenan en un nuevo **Recordset** objeto. Si el comando no está diseñado para devolver resultados (por ejemplo, una consulta UPDATE de SQL) el proveedor devuelve **nada** siempre que la opción **adExecuteNoRecords** especificado; en caso contrario, Execute devuelve un cerrado **Recordset**.  
  
 El valor devuelto **Recordset** objeto siempre es un cursor de solo lectura, solo hacia delante. Si necesita un **Recordset** con más funcionalidad, cree primero un **Recordset** objeto con la configuración de la propiedad deseada y, después, usar el **Recordset** objeto [ Método Open (ADO Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md) método para ejecutar la consulta y devolver el tipo de cursor deseados.  
  
 El contenido de la *CommandText* argumento son específico del proveedor y puede ser una sintaxis SQL estándar o cualquier formato de comando especial que admite el proveedor.  
  
 Se emitirá un evento ExecuteComplete cuando finalice esta operación.  
  
> [!NOTE]
>  Las direcciones URL con el esquema http, se invocarán automáticamente el [proveedor Microsoft OLE DB para la publicación en Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obtener más información, consulte [absoluto y las direcciones URL relativas](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conexión (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
