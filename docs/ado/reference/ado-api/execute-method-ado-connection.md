---
title: "Execute (método) (conexión de ADO) | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Connection15::Execute
- Connection15::raw_Execute
helpviewer_keywords: Execute method [ADO]
ms.assetid: 03c69320-96b2-4d85-8d49-a13b13e31578
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: b6f8e6c980d8263a5a7076603f447ecc8aa33e00
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="execute-method-ado-connection"></a>Execute (método) (conexión de ADO)
Ejecuta la consulta especificada, la instrucción SQL, el procedimiento almacenado o la texto específico del proveedor.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Set recordset = connection.Execute (CommandText, RecordsAffected, Options)  
Set recordset = connection.Execute (CommandText, RecordsAffected, Options)  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve un [conjunto de registros ADO (objetos)](../../../ado/reference/ado-api/recordset-object-ado.md) referencia de objeto.  
  
#### <a name="parameters"></a>Parámetros  
 *CommandText*  
 A **cadena** valor que contiene la instrucción SQL, el procedimiento almacenado, una dirección URL o el texto específico del proveedor para ejecutar. **Opcionalmente,**, nombres de tabla se pueden usar pero solo si el proveedor es compatible con SQL. Por ejemplo, si un nombre de tabla "Clientes" se utiliza, ADO antepondrá automáticamente la sintaxis estándar Select de SQL para formar y pasar "SELECT * FROM Customers" como un [!INCLUDE[tsql](../../../includes/tsql_md.md)] instrucción al proveedor.  
  
 *RecordsAffected*  
 Opcional. A **largo** variable a la que el proveedor devuelve el número de registros que se ven afectados por la operación.  
  
 *Opciones*  
 Opcional. A **largo** valor que indica cómo el proveedor debe evaluar el argumento CommandText. Puede ser una máscara de bits de uno o varios [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) o [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md) valores.  
  
 **Tenga en cuenta** Use la **ExecuteOptionEnum** valor **adExecuteNoRecords** para mejorar el rendimiento al minimizar el procesamiento interno y para las aplicaciones que se va a trasladar desde Visual Basic 6.0.  
  
 No utilice **adExecuteStream** con el **Execute** método de un **conexión** objeto.  
  
 No utilice los valores adCmdFile ni adCmdTableDirect con Execute. Estos valores sólo pueden utilizarse como opciones con el [Open (método) (conjunto de registros ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md) y [método Requery](../../../ado/reference/ado-api/requery-method.md) métodos de un **conjunto de registros**.  
  
## <a name="remarks"></a>Comentarios  
 Mediante el **Execute** método en un [conexión ADO (objetos)](../../../ado/reference/ado-api/connection-object-ado.md) objeto ejecuta cualquier consulta que se pasan al método en el argumento CommandText en la conexión especificada. Si el argumento CommandText especifica una consulta que devuelva filas, los resultados que genera la ejecución se almacenan en un nuevo **Recordset** objeto. Si el comando no está diseñado para devolver resultados (por ejemplo, una consulta UPDATE de SQL) el proveedor devuelve **nada** siempre que la opción **adExecuteNoRecords** especificado; en caso contrario, Execute devuelve un cerrado **conjunto de registros**.  
  
 El valor devuelto **Recordset** objeto siempre es un cursor de solo lectura, solo hacia delante. Si necesita un **conjunto de registros** objetos con mayor funcionalidad, cree primero un **Recordset** objeto con la configuración de la propiedad deseada, utilice el **Recordset** delobjeto[ Open (método) (conjunto de registros ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md) método para ejecutar la consulta y devolver el tipo de cursor deseado.  
  
 El contenido de la *CommandText* argumento son específico del proveedor y puede ser una sintaxis SQL estándar o cualquier formato de comando especial que admita el proveedor.  
  
 Se emitirá un evento ExecuteComplete cuando finalice esta operación.  
  
> [!NOTE]
>  Direcciones URL que utilizan el esquema http, se invocarán automáticamente el [proveedor Microsoft OLE DB para Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obtener más información, consulte [absoluto y direcciones URL relativas](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conexión (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
