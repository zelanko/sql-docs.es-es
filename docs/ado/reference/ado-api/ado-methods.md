---
title: "Métodos de ADO | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ADO, methods
- methods [ADO]
ms.assetid: a38c5670-ba28-44f3-bd5b-fcb46880e904
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e35be40ea3023338048bf729b9f4cea5b6048449
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="ado-methods"></a>Métodos de ADO
|||  
|-|-|  
|[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)|Crea un nuevo registro para un actualizables **Recordset** objeto.|  
|[Anexar](../../../ado/reference/ado-api/append-method-ado.md)|Anexa un objeto a una colección. Si la colección es **campos**, un nuevo **campo** objeto puede crearse antes de que se anexa a la colección.|  
|[AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md)|Anexa datos a un texto de gran tamaño o datos binarios **campo**, o a un **parámetro** objeto.|  
|[BeginTrans, CommitTrans y RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)|Administra el procesamiento de transacciones en un **conexión** objeto como sigue:<br /><br /> **BeginTrans** : inicia una transacción nueva.<br /><br /> **CommitTrans** : guarda los cambios y finaliza la transacción actual. También puede iniciar una nueva transacción.<br /><br /> **RollbackTrans** : cancela cualquier cambio y termina la transacción actual. También puede iniciar una nueva transacción.|  
|[Cancelar](../../../ado/reference/ado-api/cancel-method-ado.md)|Cancela la ejecución de una pendiente, llamada de método asincrónico.|  
|[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)|Cancela una actualización por lotes pendientes.|  
|[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)|Cancela los cambios realizados en la fila actual o nueva de un **Recordset** objeto, o el **campos** colección de un **registro** objeto antes de llamar a la  **Actualización** método.|  
|[Desactivar](../../../ado/reference/ado-api/clear-method-ado.md)|Quita todos los **Error** objetos desde la **errores** colección.|  
|[Clon](../../../ado/reference/ado-api/clone-method-ado.md)|Crea un duplicado **Recordset** objeto a partir de una existente **Recordset** objeto. Opcionalmente, especifica que la clonación sea de solo lectura.|  
|[Cerrar](../../../ado/reference/ado-api/close-method-ado.md)|Cierra un objeto abierto y los objetos dependientes.|  
|[CompareBookmarks](../../../ado/reference/ado-api/comparebookmarks-method-ado.md)|Compara dos marcadores y devuelve una indicación de sus valores relativos.|  
|[CopyRecord](../../../ado/reference/ado-api/copyrecord-method-ado.md)|Copia un archivo o directorio y su contenido a otra ubicación.|  
|[CopyTo](../../../ado/reference/ado-api/copyto-method-ado.md)|Copia el número especificado de caracteres o bytes (en función de **tipo**) en el **flujo** a otro **flujo** objeto.|  
|[CreateParameter](../../../ado/reference/ado-api/createparameter-method-ado.md)|Crea un nuevo **parámetro** objeto que tiene las propiedades especificadas.|  
|[Delete (colección Parameters de ADO)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)|Elimina un objeto de la **parámetros** colección.|  
|[Eliminar (colección de campos de ADO)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)|Elimina un objeto de la **campos** colección.|  
|[Delete (conjunto de registros ADO)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)|Elimina el registro actual o un grupo de registros.|  
|[DeleteRecord](../../../ado/reference/ado-api/deleterecord-method-ado.md)|Elimina un archivo o directorio y todos sus subdirectorios.|  
|[Execute (comando ADO)](../../../ado/reference/ado-api/execute-method-ado-command.md)|Ejecuta la consulta, la instrucción SQL o el procedimiento almacenado especificado en el **CommandText** propiedad.|  
|[Ejecutar (conexión de ADO)](../../../ado/reference/ado-api/execute-method-ado-connection.md)|Ejecuta la consulta especificada, la instrucción SQL, el procedimiento almacenado o la texto específico del proveedor.|  
|[Buscar](../../../ado/reference/ado-api/find-method-ado.md)|Busca un **conjunto de registros** para la fila que cumple los criterios especificados.|  
|[Flush](../../../ado/reference/ado-api/flush-method-ado.md)|Fuerza que el contenido de la **flujo** permanecen en el búfer de ADO en el objeto subyacente con el que el **flujo** está asociado.|  
|[get_OLEDBCommand (método)](../../../ado/reference/ado-api/get-oledbcommand-method.md)|Devuelve el comando de OLE DB subyacentes, primero propagar cualquier información de parámetros que se establece en el comando de ADO en el comando de OLE DB.|  
|[GetChildren](../../../ado/reference/ado-api/getchildren-method-ado.md)|Devuelve un **Recordset** cuyas filas representan los archivos y subdirectorios del directorio representado por este **registro**.|  
|[GetChunk](../../../ado/reference/ado-api/getchunk-method-ado.md)|Devuelve todo o una parte del contenido de un texto de gran tamaño o datos binarios **campo** objeto.|  
|[GetDataProviderDSO (método)](../../../ado/reference/ado-api/getdataproviderdso-method.md)|Recupera el objeto de origen de datos de OLEDB subyacente desde el proveedor de formas.|  
|[GetRows](../../../ado/reference/ado-api/getrows-method-ado.md)|Recupera varios registros de un **Recordset** objeto en una matriz.|  
|[GetString](../../../ado/reference/ado-api/getstring-method-ado.md)|Devuelve el **Recordset** como una cadena.|  
|[LoadFromFile](../../../ado/reference/ado-api/loadfromfile-method-ado.md)|Carga el contenido de un archivo existente en un **flujo**.|  
|[Mover](../../../ado/reference/ado-api/move-method-ado.md)|Mueve la posición del registro actual en un **Recordset** objeto.|  
|[MoveFirst, MoveLast, MoveNext y MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|Se mueve a la primera, última, siguiente o anterior registro en un determinado **Recordset** objeto y hace que el registro en el registro actual.|  
|[MoveRecord](../../../ado/reference/ado-api/moverecord-method-ado.md)|Mueve un archivo o directorio y su contenido a otra ubicación.|  
|[NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)|Borra actual **Recordset** de objetos y devuelve el siguiente **Recordset** al avanzar a través de una serie de comandos.|  
|[Abrir (conexión de ADO)](../../../ado/reference/ado-api/open-method-ado-connection.md)|Abre una conexión a un origen de datos.|  
|[Abrir (registro de ADO)](../../../ado/reference/ado-api/open-method-ado-record.md)|Se abre una existente **registro** de objeto o crea un nuevo archivo o directorio.|  
|[Abrir (conjunto de registros ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md)|Abre un cursor.|  
|[Abrir (Stream de ADO)](../../../ado/reference/ado-api/open-method-ado-stream.md)|Se abre un **flujo** objeto para manipular secuencias de datos binarios o de texto.|  
|[OpenSchema](../../../ado/reference/ado-api/openschema-method.md)|Obtiene información de esquema de base de datos del proveedor.|  
|[put_OLEDBCommand (método)](../../../ado/reference/ado-api/put-oledbcommand-method.md)|Este método no realiza ninguna operación - siempre devuelve S_OK.|  
|[Lectura](../../../ado/reference/ado-api/read-method.md)|Lee un número especificado de bytes a partir de un **flujo** objeto.|  
|[ReadText](../../../ado/reference/ado-api/readtext-method.md)|Lee un número especificado de caracteres de un texto **flujo** objeto.|  
|[Actualizar](../../../ado/reference/ado-api/refresh-method-ado.md)|Actualiza los objetos de una colección para reflejar los objetos disponibles y específicos del proveedor.|  
|[Requery](../../../ado/reference/ado-api/requery-method.md)|Actualiza los datos en un **Recordset** objeto volviendo a ejecutar la consulta en el que se basa el objeto.|  
|[Resincronización](../../../ado/reference/ado-api/resync-method.md)|Actualiza los datos en este **Recordset** objeto, o **campos** colección de un **registro** objeto de la base de datos subyacente.|  
|[Guardar](../../../ado/reference/ado-api/save-method.md)|Guarda el **Recordset** en un archivo o **flujo** objeto.|  
|[SaveToFile](../../../ado/reference/ado-api/savetofile-method.md)|Guarda el contenido binario de un **flujo** a un archivo.|  
|[Buscar](../../../ado/reference/ado-api/seek-method.md)|Busca el índice de un **Recordset** a encontrar rápidamente la fila que coincide con los valores especificados y cambia la posición de fila actual a dicha fila.|  
|[SetEOS](../../../ado/reference/ado-api/seteos-method.md)|Establece la posición que es el final de la secuencia.|  
|[SkipLine](../../../ado/reference/ado-api/skipline-method.md)|Omite una línea completa al leer una secuencia de texto.|  
|[Stat](../../../ado/reference/ado-api/stat-method.md)|Obtiene información estadística sobre una secuencia abierta.|  
|[Es compatible con](../../../ado/reference/ado-api/supports-method.md)|Determina si un determinado **Recordset** objeto admite un tipo determinado de funcionalidad.|  
|[Update](../../../ado/reference/ado-api/update-method.md)|Guarda los cambios realizados en la fila actual de un **Recordset** objeto, o el **campos** colección de un **registro** objeto.|  
|[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)|Escribe todas las actualizaciones por lotes pendientes en el disco.|  
|[Escribir](../../../ado/reference/ado-api/write-method.md)|Escribe datos binarios en un **flujo** objeto.|  
|[WriteText](../../../ado/reference/ado-api/writetext-method.md)|Escribe una cadena de texto especificado en un **flujo** objeto.|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ADO](../../../ado/reference/ado-api/ado-api-reference.md)   
 [Colecciones de ADO](../../../ado/reference/ado-api/ado-collections.md)   
 [Propiedades dinámicas de ADO](../../../ado/reference/ado-api/ado-dynamic-properties.md)   
 [Constantes enumeradas de ADO](../../../ado/reference/ado-api/ado-enumerated-constants.md)   
 [Apéndice B: errores de ADO](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [Eventos de ADO](../../../ado/reference/ado-api/ado-events.md)   
 [Modelo de objetos ADO](../../../ado/reference/ado-api/ado-object-model.md)   
 [Interfaces y los objetos ADO](../../../ado/reference/ado-api/ado-objects-and-interfaces.md)   
 [Propiedades de ADO](../../../ado/reference/ado-api/ado-properties.md)
