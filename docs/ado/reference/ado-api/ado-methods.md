---
title: Métodos de ADO | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, methods
- methods [ADO]
ms.assetid: a38c5670-ba28-44f3-bd5b-fcb46880e904
author: rothja
ms.author: jroth
ms.openlocfilehash: 65145ce8f77c352fb24a2a206d99828298b6a60c
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82747256"
---
# <a name="ado-methods"></a>Métodos de ADO

|||  
|-|-|  
|[AgregarNuevo](../../../ado/reference/ado-api/addnew-method-ado.md)|Crea un nuevo registro para un objeto de **conjunto de registros** actualizable.|  
|[Append](../../../ado/reference/ado-api/append-method-ado.md)|Anexa un objeto a una colección. Si la colección es **campos**, puede crearse un nuevo objeto de **campo** antes de que se anexe a la colección.|  
|[AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md)|Anexa datos a un **campo**de datos binario o de texto grande, o a un objeto de **parámetro** .|  
|[BeginTrans, CommitTrans y RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)|Administra el procesamiento de transacciones dentro de un objeto de **conexión** de la manera siguiente:<br /><br /> **BeginTrans** : inicia una nueva transacción.<br /><br /> **CommitTrans** : guarda los cambios y finaliza la transacción actual. También puede iniciar una nueva transacción.<br /><br /> **RollbackTrans** : cancela cualquier cambio y finaliza la transacción actual. También puede iniciar una nueva transacción.|  
|[Cancelar](../../../ado/reference/ado-api/cancel-method-ado.md)|Cancela la ejecución de una llamada de método pendiente y asincrónica.|  
|[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)|Cancela una actualización por lotes pendiente.|  
|[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)|Cancela los cambios realizados en la fila actual o nueva de un objeto de **conjunto de registros** , o la colección de **campos** de un objeto de **registro** , antes de llamar al método **Update** .|  
|[Borrar](../../../ado/reference/ado-api/clear-method-ado.md)|Quita todos los objetos de **error** de la colección de **errores** .|  
|[Clonar](../../../ado/reference/ado-api/clone-method-ado.md)|Crea un objeto de **conjunto de registros** duplicado a partir de un objeto de conjunto de **registros** existente. Opcionalmente, especifica que el clon es de solo lectura.|  
|[Close](../../../ado/reference/ado-api/close-method-ado.md)|Cierra un objeto abierto y los objetos dependientes.|  
|[CompareBookmarks](../../../ado/reference/ado-api/comparebookmarks-method-ado.md)|Compara dos marcadores y devuelve una indicación de sus valores relativos.|  
|[CopyRecord](../../../ado/reference/ado-api/copyrecord-method-ado.md)|Copia un archivo o un directorio, y su contenido, en otra ubicación.|  
|[CopyTo](../../../ado/reference/ado-api/copyto-method-ado.md)|Copia el número especificado de caracteres o bytes (dependiendo del **tipo**) de la **secuencia** en otro objeto de **flujo** .|  
|[CreateParameter](../../../ado/reference/ado-api/createparameter-method-ado.md)|Crea un nuevo objeto de **parámetro** que tiene las propiedades especificadas.|  
|[Delete (colección de parámetros de ADO)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)|Elimina un objeto de la colección de **parámetros** .|  
|[Delete (colección Fields de ADO)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)|Elimina un objeto de la colección **Fields** .|  
|[Delete (conjunto de registros ADO)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)|Elimina el registro actual o un grupo de registros.|  
|[DeleteRecord](../../../ado/reference/ado-api/deleterecord-method-ado.md)|Elimina un archivo o un directorio y todos sus subdirectorios.|  
|[Execute (comando de ADO)](../../../ado/reference/ado-api/execute-method-ado-command.md)|Ejecuta la consulta, la instrucción SQL o el procedimiento almacenado especificado en la propiedad **CommandText** .|  
|[Execute (conexión ADO)](../../../ado/reference/ado-api/execute-method-ado-connection.md)|Ejecuta la consulta, la instrucción SQL, el procedimiento almacenado o el texto específico del proveedor especificados.|  
|[Buscar](../../../ado/reference/ado-api/find-method-ado.md)|Busca en un **conjunto de registros** la fila que cumple los criterios especificados.|  
|[Consumir](../../../ado/reference/ado-api/flush-method-ado.md)|Fuerza el contenido de la **secuencia** que queda en el búfer de ADO al objeto subyacente al que está asociada la **secuencia** .|  
|[get_OLEDBCommand (método)](../../../ado/reference/ado-api/get-oledbcommand-method.md)|Devuelve el comando OLEDB subyacente, propagando primero cualquier información de parámetros establecida en el comando de ADO al comando OLEDB.|  
|[GetChildren](../../../ado/reference/ado-api/getchildren-method-ado.md)|Devuelve un **conjunto de registros** cuyas filas representan los archivos y subdirectorios del directorio representado por este **registro**.|  
|[GetChunk](../../../ado/reference/ado-api/getchunk-method-ado.md)|Devuelve todo, o una parte de, el contenido de un objeto de **campo** de datos binarios o de texto grande.|  
|[GetDataProviderDSO (método)](../../../ado/reference/ado-api/getdataproviderdso-method.md)|Recupera el objeto de origen de datos OLEDB subyacente del proveedor de formas.|  
|[GetRows](../../../ado/reference/ado-api/getrows-method-ado.md)|Recupera varios registros de un objeto de **conjunto de registros** en una matriz.|  
|[GetString](../../../ado/reference/ado-api/getstring-method-ado.md)|Devuelve el **conjunto de registros** como una cadena.|  
|[LoadFromFile (](../../../ado/reference/ado-api/loadfromfile-method-ado.md)|Carga el contenido de un archivo existente en una **secuencia**.|  
|[Mover](../../../ado/reference/ado-api/move-method-ado.md)|Mueve la posición del registro actual en un objeto de **conjunto de registros** .|  
|[MoveFirst, MoveLast, MoveNext y MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|Se desplaza al registro primero, último, siguiente o anterior de un objeto de **conjunto de registros** especificado y hace que registre el registro actual.|  
|[MoveRecord](../../../ado/reference/ado-api/moverecord-method-ado.md)|Mueve un archivo, o un directorio y su contenido, a otra ubicación.|  
|[NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)|Borra el objeto de **conjunto de registros** actual y devuelve el siguiente **conjunto de registros** avanzando por una serie de comandos.|  
|[Open (conexión ADO)](../../../ado/reference/ado-api/open-method-ado-connection.md)|Abre una conexión a un origen de datos.|  
|[Open (registro de ADO)](../../../ado/reference/ado-api/open-method-ado-record.md)|Abre un objeto **Record** existente o crea un nuevo archivo o directorio.|  
|[Open (conjunto de registros ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md)|Abre un cursor.|  
|[Open (secuencia de ADO)](../../../ado/reference/ado-api/open-method-ado-stream.md)|Abre un objeto de **flujo** para manipular flujos de datos binarios o de texto.|  
|[OpenSchema](../../../ado/reference/ado-api/openschema-method.md)|Obtiene la información del esquema de la base de datos del proveedor.|  
|[put_OLEDBCommand (método)](../../../ado/reference/ado-api/put-oledbcommand-method.md)|Este método no realiza ninguna operación; siempre Devuelve S_OK.|  
|[Lectura](../../../ado/reference/ado-api/read-method.md)|Lee un número especificado de bytes de un objeto de **secuencia** .|  
|[ReadText](../../../ado/reference/ado-api/readtext-method.md)|Lee un número especificado de caracteres de un objeto de **flujo** de texto.|  
|[Actualizar](../../../ado/reference/ado-api/refresh-method-ado.md)|Actualiza los objetos de una colección para reflejar los objetos disponibles en el proveedor y específicos de este.|  
|[Requery](../../../ado/reference/ado-api/requery-method.md)|Actualiza los datos de un objeto de **conjunto de registros** volviendo a ejecutar la consulta en la que se basa el objeto.|  
|[Resincronizar](../../../ado/reference/ado-api/resync-method.md)|Actualiza los datos del objeto de conjunto de **registros** actual, o la colección de **campos** de un objeto de **registro** , de la base de datos subyacente.|  
|[Guardar](../../../ado/reference/ado-api/save-method.md)|Guarda el **conjunto de registros** en un archivo o en un objeto de **secuencia** .|  
|[SaveToFile](../../../ado/reference/ado-api/savetofile-method.md)|Guarda el contenido binario de una **secuencia** en un archivo.|  
|[Seek](../../../ado/reference/ado-api/seek-method.md)|Busca el índice de un **conjunto de registros** para localizar rápidamente la fila que coincide con los valores especificados y cambia la posición de la fila actual a esa fila.|  
|[Seteos](../../../ado/reference/ado-api/seteos-method.md)|Establece la posición que es el final de la secuencia.|  
|[SkipLine](../../../ado/reference/ado-api/skipline-method.md)|Omite una línea completa cuando se lee una secuencia de texto.|  
|[Necesidad](../../../ado/reference/ado-api/stat-method.md)|Obtiene información estadística sobre un flujo abierto.|  
|[Admite](../../../ado/reference/ado-api/supports-method.md)|Determina si un objeto de **conjunto de registros** especificado admite un tipo determinado de funcionalidad.|  
|[Actualizar](../../../ado/reference/ado-api/update-method.md)|Guarda los cambios realizados en la fila actual de un objeto de **conjunto de registros** o la colección de **campos** de un objeto de **registro** .|  
|[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)|Escribe todas las actualizaciones de Batch pendientes en el disco.|  
|[Escritura](../../../ado/reference/ado-api/write-method.md)|Escribe datos binarios en un objeto de **secuencia** .|  
|[WriteText](../../../ado/reference/ado-api/writetext-method.md)|Escribe una cadena de texto especificada en un objeto de **secuencia** .|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de la API de ADO](../../../ado/reference/ado-api/ado-api-reference.md)   
 [Colecciones de ADO](../../../ado/reference/ado-api/ado-collections.md)   
 [Propiedades dinámicas de ADO](../../../ado/reference/ado-api/ado-dynamic-properties.md)   
 [Constantes enumeradas de ADO](../../../ado/reference/ado-api/ado-enumerated-constants.md)   
 [Apéndice B: errores de ADO](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [Eventos de ADO](../../../ado/reference/ado-api/ado-events.md)   
 [Modelo de objetos ADO](../../../ado/reference/ado-api/ado-object-model.md)   
 [Objetos e interfaces de ADO](../../../ado/reference/ado-api/ado-objects-and-interfaces.md)   
 [Propiedades de ADO](../../../ado/reference/ado-api/ado-properties.md)
