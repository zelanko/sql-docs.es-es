---
title: "Método NextRecordset (ADO) | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- NextRecordset
- Recordset15::NextRecordset
- Recordset15::raw_NextRecordset
helpviewer_keywords:
- NextRecordset method [ADO]
ms.assetid: ab1fa449-a695-4987-b1ee-bc68f89418dd
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e7650cb3516311f3eb93e93304ba9d20ec874466
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="nextrecordset-method-ado"></a>Método NextRecordset (ADO)
Borra actual [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) de objetos y devuelve el siguiente **Recordset** al avanzar a través de una serie de comandos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Set recordset2 = recordset1.NextRecordset(RecordsAffected )  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve un **Recordset** objeto. En el modelo de sintaxis, *recordset1* y *recordset2* puede ser el mismo **Recordset** objeto, o bien puede ser objetos independientes. Cuando se usa independiente **Recordset** objetos, restablecer el **ActiveConnection** propiedad en el original **Recordset** (*recordset1*) una vez **NextRecordset** se ha llamado will generará un error.  
  
#### <a name="parameters"></a>Parámetros  
 *RecordsAffected*  
 Opcional. A **largo** variable a la que el proveedor devuelve el número de registros que se ven afectados por la operación actual.  
  
> [!NOTE]
>  Este parámetro sólo devuelve el número de registros afectados por una operación; no devuelve un recuento de registros de una instrucción select utilizada para generar el **conjunto de registros**.  
  
## <a name="remarks"></a>Comentarios  
 Use la **NextRecordset** método para devolver los resultados del siguiente comando en una instrucción de comando compuesta o de un procedimiento almacenado que devuelve varios resultados. Si abre un **Recordset** objeto basado en una instrucción de comando compuesta (por ejemplo, "seleccione \* FROM Tabla1; Seleccione \* de table2 ") mediante el [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) método en un [comando](../../../ado/reference/ado-api/command-object-ado.md) o la [abiertos](../../../ado/reference/ado-api/open-method-ado-recordset.md) método en un **conjunto de registros**, ADO ejecuta sólo el primer comando y devuelve los resultados a *conjunto de registros*. Para obtener acceso a los resultados de los comandos subsiguientes de la instrucción, llame a la **NextRecordset** método.  
  
 Siempre que hay resultados adicionales y el **Recordset** que contiene las instrucciones compuestas se desconecte o calcular las referencias en los límites de proceso, no el **NextRecordset** continuará (método) devolver **Recordset** objetos. Si un comando que devuelve filas se ejecuta correctamente pero no devuelve ningún registro, el valor devuelto **Recordset** objeto estará abierto pero vacío. Prueba en este caso, compruebe que la [BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) y [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) ambas propiedades están **True**. Si una aplicación no??? comando ejecuta correctamente, el valor devuelto devuelve filas **Recordset** objeto estará cerrado, lo que puede comprobarse mediante la [estado](../../../ado/reference/ado-api/state-property-ado.md) propiedad en el **conjunto de registros**. Cuando ya no queden más resultados, *recordset* se establecerá en *nada*.  
  
 El **NextRecordset** método no está disponible en un desconectada **Recordset** objeto, donde [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) se ha establecido en **nada**(en Microsoft Visual Basic) o NULL (en otros lenguajes).  
  
 Si es una operación de edición en curso mientras esté en modo de actualización inmediata, la llamada a la **NextRecordset** método genera un error; llamar a la [actualizar](../../../ado/reference/ado-api/update-method.md) o [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) método primero.  
  
 Para pasar parámetros para más de un comando en la instrucción compuesta rellenando la [parámetros](../../../ado/reference/ado-api/parameters-collection-ado.md) colección, o pasando una matriz con el original **abiertos** o **Execute** llamada, los parámetros deben estar en el mismo orden en la colección o matriz que sus respectivos comandos en la serie de comandos. Debe finalizar leer todos los resultados antes de leer los valores de parámetro de salida.  
  
 El proveedor OLE DB determina cuándo se ejecuta cada comando de una instrucción compuesta. El [proveedor Microsoft OLE DB para SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md), por ejemplo, ejecuta todos los comandos en un lote al recibir la instrucción compuesta. Resultante **conjuntos de registros** simplemente se devuelven cuando se llama a **NextRecordset**.  
  
 Sin embargo, otros proveedores pueden ejecutar el comando siguiente en una instrucción solo después de llama a NextRecordset. Para estos proveedores, si cierra explícitamente el **Recordset** objeto antes de la ejecución paso a paso a través de la instrucción de comando completo, ADO no ejecutará nunca los comandos restantes.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo del método NextRecordset (VB)](../../../ado/reference/ado-api/nextrecordset-method-example-vb.md)   
 [Ejemplo del método NextRecordset (VC ++)](../../../ado/reference/ado-api/nextrecordset-method-example-vc.md)   

