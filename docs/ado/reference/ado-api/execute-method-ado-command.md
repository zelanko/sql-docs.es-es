---
title: Método Execute (Command ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::Execute
- Command15::raw_Execute
helpviewer_keywords:
- Execute method [ADO]
ms.assetid: f84a5ff3-0528-4ad7-9bea-9a15103378dd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4ef42c04944f39e0b2d1930cc6520df2b6c5fa5d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67918855"
---
# <a name="execute-method-ado-command"></a>Método Execute (Command ADO)
Ejecuta la consulta, la instrucción SQL o el procedimiento almacenado especificado en el [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) o [CommandStream](../../../ado/reference/ado-api/commandstream-property-ado.md) propiedad de la [objeto Command](../../../ado/reference/ado-api/command-object-ado.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Set recordset = command.Execute( RecordsAffected, Parameters, Options )  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) referencia de objeto, una secuencia, o **nada**.  
  
#### <a name="parameters"></a>Parámetros  
 *RecordsAffected*  
 Opcional. Un **largo** variable a la que el proveedor devuelve el número de registros que se ven afectados por la operación. El *RecordsAffected* parámetro solo se aplica a las consultas de acción o los procedimientos almacenados. *RecordsAffected* no devuelve el número de registros devueltos por un procedimiento almacenado o una consulta que devuelve resultados. Para obtener esta información, use la [RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md) propiedad. El **Execute** método no devolverá la información correcta cuando se usa con **adAsyncExecute**, simplemente porque cuando se ejecuta de forma asincrónica un comando, el número de registros afectados es posible que no conozca en el momento en que el método devuelve.  
  
 *Parámetros*  
 Opcional. Un **Variant** matriz de valores de parámetro que se usa junto con la cadena de entrada o la secuencia especificada en **CommandText** o **CommandStream**. (Los parámetros de salida no devolverá valores correctos cuando se pasa este argumento.)  
  
 *Opciones*  
 Opcional. Un **largo** valor que indica cómo el proveedor debe evaluar el [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) o el [CommandStream](../../../ado/reference/ado-api/commandstream-property-ado.md) propiedad de la [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto. Puede ser un valor de máscara de bits que se realiza mediante [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) o [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md) valores. Por ejemplo, podría usar **adCmdText** y **adExecuteNoRecords** en combinación, si desea que ADO evalúe el valor de la **CommandText** propiedad como texto, y indicar que el comando debe descartar y no devolver ningún registro que puede generarse cuando se ejecuta el texto del comando.  
  
> [!NOTE]
>  Use la **ExecuteOptionEnum** valor **adExecuteNoRecords** para mejorar el rendimiento, ya que minimiza el procesamiento interno. Si **adExecuteStream** se especifica, las opciones **adAsyncFetch** y **adAsynchFetchNonBlocking** se omiten. No utilice el **CommandTypeEnum** valores de **adCmdFile** o **adCmdTableDirect** con **Execute**. Solo se pueden usar estos valores como opciones con la [abierto](../../../ado/reference/ado-api/open-method-ado-recordset.md) y [Requery](../../../ado/reference/ado-api/requery-method.md) métodos de un **Recordset**.  
  
## <a name="remarks"></a>Comentarios  
 Mediante el **Execute** método en un **comando** objeto ejecuta la consulta especificada en el **CommandText** propiedad o **CommandStream** propiedad del objeto.  
  
 Los resultados se devuelven en un **Recordset** (de forma predeterminada) o como un flujo de información binaria. Para obtener un flujo binario, especifique **adExecuteStream** en *opciones*, a continuación, proporcione un flujo estableciendo **Command.Properties ("salida Stream")** . ADO **Stream** objeto puede especificarse para recibir los resultados o se puede especificar otro objeto stream, como el objeto de respuesta de IIS. Si se ha especificado ninguna secuencia antes de llamar a **Execute** con **adExecuteStream**, se produce un error. La posición de la secuencia en la devolución de **Execute** es proveedor específico.  
  
 Si el comando no está diseñado para devolver resultados (por ejemplo, una consulta UPDATE de SQL) el proveedor devuelve **nada** siempre que la opción **adExecuteNoRecords** especificado; en caso contrario, Execute devuelve un cerrado **Recordset**. Algunos lenguajes de aplicación permiten omitir este valor devuelto si no hay ningún **Recordset** es el deseado.  
  
 **Ejecutar** genera un error si el usuario especifica un valor para **CommandStream** cuando el **CommandType** es **adCmdStoredProc**,  **adCmdTable**, o **adCmdTableDirect**.  
  
 Si la consulta tiene parámetros, valores actual para el **comando** se usan los parámetros del objeto a menos que reemplace estos elementos con los valores de parámetro pasados con la **Execute** llamar. Puede invalidar un subconjunto de los parámetros omitiendo valores nuevos para algunos de los parámetros cuando se llama a la **Execute** método. El orden en el que se especifican los parámetros es el mismo orden en que los pasa al método. Por ejemplo, si hay cuatro (o más) parámetros y desea pasar valores nuevos para los parámetros primeros y cuarto, pasaría `Array(var1,,,var4)` como el *parámetros* argumento.  
  
> [!NOTE]
>  Los parámetros de salida no devolverán valores correctos cuando se pasa en el *parámetros* argumento.  
  
 Un [ExecuteComplete](../../../ado/reference/ado-api/executecomplete-event-ado.md) evento se emitirá cuando finalice esta operación.  
  
> [!NOTE]
>  Al emitir comandos que contiene las direcciones URL, los usuarios que usen el esquema http invocará automáticamente el [proveedor Microsoft OLE DB para la publicación en Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obtener más información, consulte [absoluto y las direcciones URL relativas](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Execute, Requery y Clear métodos ejemplo (VB)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vb.md)   
 [Execute, Requery y Clear métodos ejemplo (VBScript)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vbscript.md)   
 [Execute, Requery y Clear métodos ejemplo (VC ++)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vc.md)   
 [Propiedad CommandStream (ADO)](../../../ado/reference/ado-api/commandstream-property-ado.md)   
 [Propiedad CommandText (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md)   
 [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)   
 [Ejecutar el método (conexión de ADO)](../../../ado/reference/ado-api/execute-method-ado-connection.md)   
 [Evento ExecuteComplete (ADO)](../../../ado/reference/ado-api/executecomplete-event-ado.md)
