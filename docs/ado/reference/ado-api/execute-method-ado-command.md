---
title: "Método Execute (Command ADO) | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Command15::Execute
- Command15::raw_Execute
helpviewer_keywords:
- Execute method [ADO]
ms.assetid: f84a5ff3-0528-4ad7-9bea-9a15103378dd
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 651123d3112ca58c028412bd025325f303f0d637
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="execute-method-ado-command"></a>Método Execute (Command ADO)
Ejecuta la consulta, la instrucción SQL o el procedimiento almacenado especificado en el [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) o [CommandStream](../../../ado/reference/ado-api/commandstream-property-ado.md) propiedad de la [objeto de comando](../../../ado/reference/ado-api/command-object-ado.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Set recordset = command.Execute( RecordsAffected, Parameters, Options )  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) referencia de objeto, una secuencia, o **nada**.  
  
#### <a name="parameters"></a>Parámetros  
 *RecordsAffected*  
 Opcional. A **largo** variable a la que el proveedor devuelve el número de registros que se ven afectados por la operación. El *RecordsAffected* parámetro solo se aplica a las consultas de acción o los procedimientos almacenados. *RecordsAffected* no devuelve el número de registros devueltos por un procedimiento almacenado o una consulta que devuelve resultados. Para obtener esta información, use la [RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md) propiedad. El **Execute** método no devolverá la información correcta cuando se usa con **adAsyncExecute**, simplemente porque cuando se ejecuta de forma asincrónica un comando, el número de registros afectados puede todavía no se conoce en el momento en que el método devuelve.  
  
 *Parámetros*  
 Opcional. A **Variant** matriz de valores de parámetro que se usa junto con la cadena de entrada o la secuencia especificados en **CommandText** o **CommandStream**. (Los parámetros de salida no devuelve valores correctos cuando se pasa este argumento.)  
  
 *Opciones*  
 Opcional. A **largo** valor que indica cómo debe evaluar el proveedor el [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) o [CommandStream](../../../ado/reference/ado-api/commandstream-property-ado.md) propiedad de la [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto. Puede ser un valor de máscara de bits formado con [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) o [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md) valores. Por ejemplo, podría utilizar **adCmdText** y **adExecuteNoRecords** en combinación si desea que ADO evalúe el valor de la **CommandText** propiedad como texto, y indicar que el comando debe descartar y no devolver ningún registro que pueda generarse cuando se ejecuta el texto del comando.  
  
> [!NOTE]
>  Use la **ExecuteOptionEnum** valor **adExecuteNoRecords** para mejorar el rendimiento al minimizar el procesamiento interno. Si **adExecuteStream** se especifica, las opciones de **adAsyncFetch** y **adAsynchFetchNonBlocking** se omiten. No utilice la **CommandTypeEnum** valores de **adCmdFile** o **adCmdTableDirect** con **Execute**. Estos valores sólo pueden utilizarse como opciones con el [abiertos](../../../ado/reference/ado-api/open-method-ado-recordset.md) y [Requery](../../../ado/reference/ado-api/requery-method.md) métodos de un **conjunto de registros**.  
  
## <a name="remarks"></a>Comentarios  
 Mediante el **Execute** método en un **comando** objeto ejecuta la consulta especificada en el **CommandText** propiedad o **CommandStream** propiedad del objeto.  
  
 Se devuelven resultados en un **Recordset** (de forma predeterminada) o como una secuencia de información binaria. Para obtener una secuencia binaria, especifique **adExecuteStream** en *opciones*, a continuación, proporcionar un flujo estableciendo **Command.Properties ("flujo de salida")**. ADO **flujo** objeto puede especificarse para recibir los resultados, o se puede especificar otro objeto de secuencia, como el objeto de respuesta de IIS. Si no hay ninguna secuencia se ha especificado antes de llamar a **Execute** con **adExecuteStream**, se produce un error. La posición de la secuencia en la devolución de **Execute** es proveedor específico.  
  
 Si el comando no está diseñado para devolver resultados (por ejemplo, una consulta UPDATE de SQL) el proveedor devuelve **nada** siempre que la opción **adExecuteNoRecords** especificado; en caso contrario, Execute devuelve un cerrado **conjunto de registros**. Algunos lenguajes de aplicación permiten omitir este valor devuelto si no hay ningún **Recordset** se desea.  
  
 **Ejecutar** genera un error si el usuario especifica un valor para **CommandStream** cuando el **CommandType** es **adCmdStoredProc**, ** adCmdTable**, o **adCmdTableDirect**.  
  
 Si la consulta tiene parámetros, valores actual para la **comando** se usan los parámetros del objeto a menos que se reemplacen éstos con los valores de parámetro pasados con la **Execute** llamar. Puede reemplazar un subconjunto de los parámetros omitiendo valores nuevos para algunos de los parámetros cuando se llama a la **Execute** método. El orden en que se especifican los parámetros es el mismo orden en que los pasa al método. Por ejemplo, si hay cuatro (o más) parámetros y desea pasar valores nuevos para los parámetros primeros y cuarto, pasaría `Array(var1,,,var4)` como el *parámetros* argumento.  
  
> [!NOTE]
>  Parámetros de salida no devolverán valores correctos cuando se pasa en el *parámetros* argumento.  
  
 Un [ExecuteComplete](../../../ado/reference/ado-api/executecomplete-event-ado.md) se emitirán los eventos cuando finaliza esta operación.  
  
> [!NOTE]
>  Cuando se emite comandos que contiene las direcciones URL, los usuarios que utilicen el esquema http, se invocarán automáticamente el [proveedor Microsoft OLE DB para Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obtener más información, consulte [absoluto y direcciones URL relativas](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de comando (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Execute, Requery y Clear ejemplo de los métodos (VB)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vb.md)   
 [Execute, Requery y Clear métodos ejemplo (VBScript)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vbscript.md)   
 [Execute, Requery y Clear ejemplo de los métodos (VC ++)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vc.md)   
 [Propiedad CommandStream (ADO)](../../../ado/reference/ado-api/commandstream-property-ado.md)   
 [Propiedad CommandText (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md)   
 [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)   
 [Execute (método) (conexión de ADO)](../../../ado/reference/ado-api/execute-method-ado-connection.md)   
 [Evento ExecuteComplete (ADO)](../../../ado/reference/ado-api/executecomplete-event-ado.md)

