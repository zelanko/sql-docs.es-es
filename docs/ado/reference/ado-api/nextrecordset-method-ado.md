---
title: Método NextRecordset (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 03/20/2018
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- NextRecordset
- Recordset15::NextRecordset
- Recordset15::raw_NextRecordset
helpviewer_keywords:
- NextRecordset method [ADO]
ms.assetid: ab1fa449-a695-4987-b1ee-bc68f89418dd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3c7af4f5d217670ab23e71a3c53ccd5cf7944b0c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67932033"
---
# <a name="nextrecordset-method-ado"></a>Método NextRecordset (ADO)
Borra actual [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) de objetos y devuelve el siguiente **Recordset** al avanzar a través de una serie de comandos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Set recordset2 = recordset1.NextRecordset(RecordsAffected )  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve un **Recordset** objeto. En el modelo de sintaxis, *recordset1* y *recordset2* puede ser el mismo **Recordset** objeto, o bien puede usar objetos independientes. Cuando se usa independiente **Recordset** objetos, al restablecer el **ActiveConnection** propiedad en el original **Recordset** (*recordset1*) una vez **NextRecordset** se ha llamado a voluntad generará un error.  
  
#### <a name="parameters"></a>Parámetros  
 *RecordsAffected*  
 Opcional. Un **largo** variable a la que el proveedor devuelve el número de registros afectados por la operación actual.  
  
> [!NOTE]
>  Este parámetro solo devuelve el número de registros afectados por una operación; no devuelve un recuento de registros de una instrucción select utilizada para generar el **Recordset**.  
  
## <a name="remarks"></a>Comentarios  
 Use la **NextRecordset** método para devolver los resultados del comando siguiente en una instrucción compuesta o de un procedimiento almacenado que devuelve varios resultados. Si abre un **Recordset** objeto basado en una instrucción compuesta (por ejemplo, "seleccione \* FROM table1; Seleccione \* de table2 ") mediante el [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) método en un [comando](../../../ado/reference/ado-api/command-object-ado.md) o el [abierto](../../../ado/reference/ado-api/open-method-ado-recordset.md) método en un **Recordset**, ADO sólo el primer comando se ejecuta y devuelve los resultados a *recordset*. Para obtener acceso a los resultados de los comandos subsiguientes en la instrucción, llame a la **NextRecordset** método.  
  
 Siempre y cuando hay resultados adicionales y el **Recordset** que contiene las instrucciones compuestas se desconecte o calcular los límites del proceso, el **NextRecordset** seguirá (método) devolver **Recordset** objetos. Si un comando que devuelve filas se ejecuta correctamente pero no devuelve ningún registro, el valor devuelto **Recordset** objeto estará abierto pero vacío. Prueba para este caso, compruebe que la [BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) y [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) ambas propiedades están **True**. Si un comando no devuelve filas ejecuta correctamente, el valor devuelto **Recordset** objeto se cerrará, que puede comprobar probando la [estado](../../../ado/reference/ado-api/state-property-ado.md) propiedad en el **Recordset**. Cuando no hay ningún resultado más, *recordset* se establecerá en *nada*.  
  
 El **NextRecordset** método no está disponible en un desconectado **Recordset** objeto, donde [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) se ha establecido en **nada**(en Microsoft Visual Basic) o NULL (en otros lenguajes).  
  
 Si es una edición en curso en el modo de actualización inmediata, la llamada a la **NextRecordset** método genera un error; llame a la [actualizar](../../../ado/reference/ado-api/update-method.md) o [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) método primero.  
  
 Pasar parámetros para más de un comando en la instrucción compuesta rellenando la [parámetros](../../../ado/reference/ado-api/parameters-collection-ado.md) colección, o pasando una matriz con el original **abierto** o **Execute** llamada, los parámetros deben estar en el mismo orden en la colección o matriz que sus comandos respectivos en la serie de comandos. Debe terminar de leer todos los resultados antes de leer los valores de parámetro de salida.  
  
 El proveedor OLE DB determina cuándo se ejecuta cada comando en una instrucción compuesta. El [proveedor Microsoft OLE DB para SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md), por ejemplo, ejecuta todos los comandos en un lote al recibir la instrucción compuesta. Resultante **conjuntos de registros** simplemente se devuelven cuando se llama a **NextRecordset**.  
  
 Sin embargo, otros proveedores pueden ejecutar el comando siguiente en una instrucción solo después de llamar a NextRecordset. Para estos proveedores, si cierra explícitamente el **Recordset** objeto antes de la ejecución paso a paso a través de la instrucción de comando completo, ADO nunca ejecuta los comandos restantes.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo del método NextRecordset (VB)](../../../ado/reference/ado-api/nextrecordset-method-example-vb.md)   
 [Ejemplo del método NextRecordset (VC ++)](../../../ado/reference/ado-api/nextrecordset-method-example-vc.md)   
