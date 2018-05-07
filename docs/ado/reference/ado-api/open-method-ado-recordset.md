---
title: Open (método) (conjunto de registros ADO) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::raw_Open
- Recordset15::Open
helpviewer_keywords:
- Open method [ADO]
ms.assetid: 3236749c-4b71-4235-89e2-ccdfaaa9319d
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e562f329f6f95a36777fc4db9131091003be37e0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="open-method-ado-recordset"></a>Open (método) (conjunto de registros ADO)
Abre un cursor en una [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
recordset.Open Source, ActiveConnection, CursorType, LockType, Options  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Source*  
 Opcional. A **Variant** que se evalúa como válido [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto, una instrucción SQL, un nombre de tabla, una llamada de procedimiento almacenado, una dirección URL o el nombre de un archivo o [flujo](../../../ado/reference/ado-api/stream-object-ado.md) objeto que contiene un almacenar de manera permanente [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
 *ActiveConnection*  
 Opcional. Ya sea un **Variant** que se evalúa como válido [conexión](../../../ado/reference/ado-api/connection-object-ado.md) nombre de variable de objeto, o un **cadena** que contiene [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) parámetros.  
  
 *CursorType*  
 Opcional. A [CursorTypeEnum](../../../ado/reference/ado-api/cursortypeenum.md) valor que determina el tipo de cursor que el proveedor debe usar al abrir el **conjunto de registros**. El valor predeterminado es **adOpenForwardOnly**.  
  
 *LockType*  
 Opcional. A [LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md) valor que determina qué tipo de bloqueo (concurrencia) que debe usar el proveedor al abrir el **conjunto de registros**. El valor predeterminado es **adLockReadOnly**.  
  
 *Opciones*  
 Opcional. A **largo** valor que indica cómo el proveedor debe evaluar el *origen* argumento si representa algo distinto de un **comando** objeto o que la **Recordset** debe restaurarse desde un archivo donde se guardó anteriormente. Puede ser uno o más [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) o [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md) valores, que se pueden combinar con un operador OR bit a bit.  
  
> [!NOTE]
>  Si abre un **Recordset** desde una **flujo** que contiene un persistente **conjunto de registros**, utilizando un [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md) valo **adAsyncFetchNonBlocking** no tiene ningún efecto; la búsqueda será sincrónica y de bloqueo.  
  
> [!NOTE]
>  El **ExecuteOpenEnum** valores de **adExecuteNoRecords** o **adExecuteStream** no debe usarse con **abiertos**.  
  
## <a name="remarks"></a>Comentarios  
 El cursor predeterminado para ADO **Recordset** es un cursor de solo avance y solo lectura ubicado en el servidor.  
  
 Mediante el **abiertos** método en un **Recordset** objeto abre un cursor que representa los registros de una tabla base, los resultados de una consulta o guardado anteriormente **conjunto de registros**.  
  
 Usar opcional *origen* argumento para especificar un origen de datos mediante uno de los siguientes: una **comando** variable de objeto, una instrucción SQL, un procedimiento almacenado, un nombre de tabla, una dirección URL o un nombre de ruta de acceso completa del archivo. Si *origen* es un nombre de ruta de acceso de archivo, puede ser una ruta de acceso completa ("c:\dir\file.rst"), una ruta de acceso relativa ("... \file.rst"), o una dirección URL ("http://files/file.rst").  
  
 No es una buena idea usar el *origen* argumento de la **abiertos** método para realizar una consulta de acción que no devuelve registros porque no hay ninguna manera fácil de determinar si la llamada se realizó correctamente. El **Recordset** devuelve como una consulta se cerrarán. Para realizar una consulta que no devuelve registros, como una instrucción INSERT de SQL, llame a la [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) método de un **comando** objeto o la [Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md) método de un [Conexión](../../../ado/reference/ado-api/connection-object-ado.md) objeto en su lugar.  
  
 El *ActiveConnection* argumento corresponde a la [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) propiedad y se especifica en qué conexión para abrir el **Recordset** objeto. Si se pasa una definición de conexión para este argumento, ADO abre una nueva conexión mediante los parámetros especificados. Después de abrir el **Recordset** con un cursor de cliente estableciendo el [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) propiedad **adUseClient**, puede cambiar el valor de esta propiedad para enviar actualizaciones a otro proveedor. O puede establecer esta propiedad en **nada** (en Microsoft Visual Basic) o NULL para desconectar el **Recordset** desde cualquier proveedor. Cambiar *ActiveConnection* para un cursor de servidor genera un error, sin embargo.  
  
 Para el resto de los argumentos que se corresponden directamente a las propiedades de un **Recordset** objeto (*origen*, *CursorType*, y *LockType*), la relación de los argumentos de las propiedades es como sigue:  
  
-   La propiedad es de lectura/escritura antes de la **Recordset** objeto está abierto.  
  
-   Se utilizan los valores de propiedad, a menos que se pasen los argumentos correspondientes cuando se ejecute la **abiertos** método. Si se pasa un argumento, reemplaza el valor de propiedad correspondiente y el valor de propiedad se actualiza con el valor del argumento.  
  
-   Después de abrir el **Recordset** objeto, estas propiedades son de sólo lectura.  
  
> [!NOTE]
>  El **ActiveConnection** propiedad es de solo lectura para **Recordset** objetos cuyo [origen](../../../ado/reference/ado-api/source-property-ado-recordset.md) propiedad está establecida en válido **comando** objeto, incluso si la **Recordset** objeto no está abierto.  
  
 Si se pasa un **comando** objeto en el *origen* argumento y también pase un *ActiveConnection* argumento, que se produce un error. El **ActiveConnection** propiedad de la **comando** objeto ya debe estar establecido en válido **conexión** objeto o cadena de conexión.  
  
 Si se pasa algo distinto de un **comando** objeto en el *origen* argumento, puede usar el *opciones* argumento para optimizar la evaluación de la *origen*  argumento. Si el *opciones* argumento no está definido, puede experimentar una disminución del rendimiento porque ADO debe realizar llamadas al proveedor para determinar si el argumento es una instrucción SQL, un procedimiento almacenado, una dirección URL o un nombre de tabla. Si sabe qué es *origen* tipo que está utilizando, establecer el *opciones* argumento indica a ADO que salte directamente al código pertinente. Si el *opciones* argumento no coincide con el *origen* escribe, se produce un error.  
  
 Si se pasa un **flujo** objeto en el *origen* argumento, no debes pasar información en el resto de argumentos. Si lo hace, se generará un error. El **ActiveConnection** información no está retenido cuando un **conjunto de registros** se abre desde un **flujo**.  
  
 El valor predeterminado para la *opciones* argumento es **adCmdFile** si no hay ninguna conexión está asociada a la **conjunto de registros**. Esto suele ser el caso para almacenar de manera permanente **Recordset** objetos.  
  
 Si el origen de datos no devuelve ningún registro, el proveedor establece tanto la [BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) y [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) propiedades a **True**, y la posición actual del registro es indefinida. Todavía puede agregar nuevos datos a este vacío **Recordset** objeto si el tipo de cursor lo permite.  
  
 Cuando haya finalizado las operaciones en un formato de archivo **Recordset** objeto, utilice la [cerrar](../../../ado/reference/ado-api/close-method-ado.md) método para liberarlos recursos del sistema asociados. Cerrar un objeto no se quita de la memoria; puede cambiar sus valores de propiedad y usar el **abrir** método para abrirla de nuevo más tarde. Para eliminar completamente un objeto de la memoria, establezca la variable de objeto *nada*.  
  
 Antes de la **ActiveConnection** propiedad está establecida, llame a **abiertos** sin operandos para crear una instancia de un **Recordset** creado anexando campos a la  **Conjunto de registros** [campos](../../../ado/reference/ado-api/fields-collection-ado.md) colección.  
  
 Si ha configurado la [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) propiedad **adUseClient**, es posible recuperar filas de forma asincrónica en uno de dos maneras. El método recomendado consiste en establecer *opciones* a **adAsyncFetch**. Como alternativa, puede utilizar la propiedad dinámica "Asynchronous Rowset Processing" en el [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) colección, pero eventos recuperados relacionados pueden perderse si no establece la *opciones* parámetro **adAsyncFetch**.  
  
> [!NOTE]
>  Recuperación en segundo plano en el proveedor MS Remote se admite solo mediante la **abiertos** del método *opciones* parámetro.  
  
> [!NOTE]
>  Direcciones URL que utilizan el esquema http, se invocarán automáticamente el [proveedor Microsoft OLE DB para Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obtener más información, consulte [absoluto y direcciones URL relativas](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
 Ciertas combinaciones de [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) y [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md) valores no son válidos. Para obtener información sobre los cuales no se pueden combinar opciones, vea los temas para la [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md), y [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md).  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de los métodos de apertura y cierre (VB)](../../../ado/reference/ado-api/open-and-close-methods-example-vb.md)   
 [Ejemplo de los métodos de apertura y cierre (VBScript)](../../../ado/reference/ado-api/open-and-close-methods-example-vbscript.md)   
 [Ejemplo de los métodos de apertura y cierre (VC ++)](../../../ado/reference/ado-api/open-and-close-methods-example-vc.md)   
 [Guardar y abrir un ejemplo de los métodos (VB)](../../../ado/reference/ado-api/save-and-open-methods-example-vb.md)   
 [Open (método) (conexión de ADO)](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Open (método) (registro de ADO)](../../../ado/reference/ado-api/open-method-ado-record.md)   
 [Open (método) (Stream de ADO)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [Método OpenSchema](../../../ado/reference/ado-api/openschema-method.md)   
 [Save (método)](../../../ado/reference/ado-api/save-method.md)
