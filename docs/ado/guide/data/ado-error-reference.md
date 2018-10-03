---
title: Errores de ADO | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- errors [ADO], number reference
- errors [ADO], ErrorValueEnum
- ErrorValueEnum enumeration [ADO]
ms.assetid: f653393e-d4b0-4c34-ad5f-2bdf56bc1305
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d61e3ab4bd3fb7afda858dd7e2b14fd2bddbd599
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47752393"
---
# <a name="ado-errors"></a>Errores de tiempo de ejecución de ADO
El **ErrorValueEnum** constante describe los valores de error de ADO. Para obtener una lista completa de estas constantes enumeradas, incluidos los valores, vea [Apéndice B: errores de ADO](../../../ado/guide/appendixes/appendix-b-ado-errors.md). En esta sección examinaremos algunos de los errores más interesantes y explicar algunas situaciones específicas que pueden generar, o soluciones para corregir el problema. Tanto el **ErrorValueEnum** aparecen constante y el número decimal positivo corto.

|Number|Constante ErrorValueEnum|Descripción/causas posibles|
|------------|-----------------------------|----------------------------------|
|**3000**|**adErrProviderFailed**|Proveedor no pudo realizar la operación solicitada.|
|**3001**|**adErrInvalidArgument**|Los argumentos son del tipo incorrecto, están fuera del intervalo aceptable o están en conflicto entre sí. Este error se produjo a menudo por un error tipográfico en una instrucción SELECT de SQL. Por ejemplo, un nombre de tabla o campo mal escrita puede generar este error. Este error también puede producirse cuando un campo o una tabla con el nombre de una instrucción SELECT no existe en el almacén de datos.|
|**3002**|**adErrOpeningFile**|No se pudo abrir el archivo. Se especificó un nombre de archivo mal escrito o movido, cambiado de nombre o eliminar un archivo. A través de una red, la unidad podría no estar disponible temporalmente o tráfico de red podría impedir una conexión.|
|**3003**|**adErrReadFile**|No se pudo leer el archivo. Se especifica incorrectamente el nombre del archivo, es posible que se han movido o eliminado el archivo o el archivo puede estar dañado.|
|**3004**|**adErrWriteFile**|Escritura en un archivo error. Es posible que se ha cerrado un archivo y, a continuación, intentó escribir en él, o el archivo podría estar dañado. Si el archivo se encuentra en una unidad de red, las condiciones de red transitorio pueden impedir que la escritura en una unidad de red.|
|**3021**|**adErrNoCurrentRecord**|Cualquier **BOF** o **EOF** es True, o se ha eliminado el registro actual. La operación solicitada requiere un registro actual.<br /><br /> Se intentó actualizar registros mediante **buscar** o **Seek** para mover el puntero de registro para el registro deseado. Si no se encuentra el registro, **EOF** será True. Este error también puede producirse después de un error **AddNew** o **eliminar** porque no hay ningún registro actual cuando estos métodos generan errores.|
|**3219**|**adErrIllegalOperation**|Operación no se permite en este contexto.|
|**3220**|**adErrCantChangeProvider**|El proveedor suministrado es diferente de aquel ya está en uso.|
|**3246**|**adErrInTransaction**|**Conexión** objeto no se puede cerrar explícitamente en una transacción. Un **Recordset** o **conexión** no se puede cerrar el objeto que está participando en una transacción. Llamar a **RollbackTrans** o **CommitTrans** antes de cerrar el objeto.|
|**3251**|**adErrFeatureNotAvailable**|El objeto o el proveedor no es capaz de realizar la operación solicitada. Algunas operaciones dependen de una versión de proveedor determinado.|
|**3265**|**adErrItemNotFound**|No se encuentra el elemento de la colección correspondiente para el nombre u ordinal. Se ha especificado un nombre de campo o de tabla incorrecto.|
|**3367**|**adErrObjectInCollection**|Objeto ya está en la colección. No se puede anexar. No se puede agregar un objeto a la misma colección dos veces.|
|**3420**|**adErrObjectNotSet**|Objeto ya no es válido.|
|**3421**|**adErrDataConversion**|Aplicación utiliza un valor de un tipo incorrecto para la operación actual. Es posible que ha proporcionado una cadena a una operación que espera una secuencia, por ejemplo.|
|**3704**|**adErrObjectClosed**|No se permite la operación cuando el objeto está cerrado. El **conexión** o **Recordset** se ha cerrado. Por ejemplo, es posible que algunas otras rutinas podrían cerrar un objeto global. Puede evitar este error comprobando el **estado** propiedad antes de intentar una operación.|
|**3705**|**adErrObjectOpen**|No se permite la operación cuando el objeto está abierto. No se puede abrir un objeto que está abierto. Los campos no se puede anexar una apertura **Recordset**.|
|**3706**|**adErrProviderNotFound**|No se encuentra el proveedor. Se pueden no instalarse correctamente.<br /><br /> Se podría especificar el nombre del proveedor de forma incorrecta, el proveedor especificado no puede instalarse en el equipo donde se ejecuta el código o la instalación es posible que se han dañado.|
|**3707**|**adErrBoundToCommand**|El **ActiveConnection** propiedad de un **Recordset** objeto, que tiene un **comando** como su origen de objeto, no se puede cambiar. La aplicación intentó asignar un nuevo **conexión** objeto a un **Recordset** que tiene un **comando** objeto como su origen.|
|**3708**|**adErrInvalidParamInfo**|**Parámetro** objeto no está definido correctamente. Se proporcionó información incoherente o incompleta.|
|**3709**|**adErrInvalidConnection**|La conexión no se puede usar para realizar esta operación. Es cerrado o no válido en este contexto.|
|**3710**|**adErrNotReentrant**|No se puede realizar la operación al evento de procesamiento. No se puede realizar una operación dentro de un controlador de eventos que provoca el evento se vuelva a activar. Por ejemplo, métodos de navegación no deben llamarse desde dentro un **WillMove** controlador de eventos.|
|**3711**|**adErrStillExecuting**|No se puede realizar la operación mientras se ejecuta de forma asincrónica.|
|**3712**|**adErrOperationCancelled**|Operación cancelada por el usuario. La aplicación ha llamado el **CancelUpdate** o **CancelBatch** método y la operación actual se ha cancelado.|
|**3713**|**adErrStillConnecting**|No se puede realizar la operación mientras se conecta de forma asincrónica.|
|**3714**|**adErrInvalidTransaction**|Coordinación de transacciones no es válido o no se ha iniciado.|
|**3715**|**adErrNotExecuting**|No se puede realizar la operación mientras no se ejecute.|
|**3716**|**adErrUnsafeOperation**|Configuración de seguridad de este equipo prohíbe tener acceso a un origen de datos en otro dominio.|
|**3717**|**adWrnSecurityDialog**|Exclusivamente para uso interno. No use. (El valor de entrada se incluyó por motivos de integridad. Este error no debería aparecer en el código.)|
|**3718**|**adWrnSecurityDialogHeader**|Exclusivamente para uso interno. No use. (Entrada incluida por razones de integridad. Este error no debería aparecer en el código.)|
|**3719**|**adErrIntegrityViolation**|Valor de datos está en conflicto con las restricciones de integridad del campo. Un nuevo valor para un **campo** provocaría una clave duplicada. Un valor que conforma un lado de una relación entre dos registros podría no ser actualizable.|
|**3720**|**adErrPermissionDenied**|Permisos insuficientes impide escribir en el campo. El usuario mencionado en la cadena de conexión no tiene los permisos adecuados para escribir en un **campo**.|
|**3721**|**adErrDataOverflow**|Valor de datos es demasiado grande para representarlo mediante el tipo de datos. Se asignó un valor numérico que es demasiado grande para el campo correspondiente. Por ejemplo, un valor entero largo se asignó a un campo de entero corto.|
|**3722**|**adErrSchemaViolation**|Valor de datos está en conflicto con el tipo de datos o las restricciones del campo. El almacén de datos tiene restricciones de validación que difieren de los **campo** valor.|
|**3723**|**adErrSignMismatch**|Error de conversión porque el valor de datos tenía signo y el tipo de datos utilizado por el proveedor no tenía signo.|
|**3724**|**adErrCantConvertvalue**|No se puede convertir el valor de datos por razones distintas del desbordamiento de datos o la falta de coincidencia de inicio de sesión. Por ejemplo, conversión habría truncado los datos.|
|**3725**|**adErrCantCreate**|Valor de datos no se puede establecer o recuperar porque se desconoce el tipo de datos de campo o el proveedor tuvo recursos insuficientes para realizar la operación.|
|**3726**|**adErrColumnNotOnThisRow**|Registro no contiene este campo. Se especificó un nombre de campo incorrecto o un campo no está en el **campos** se hace referencia a la colección del registro actual.|
|**3727**|**adErrURLDoesNotExist**|La dirección URL de origen o el elemento primario de la dirección URL de destino no existe. Hay un error tipográfico en la dirección URL de origen o destino. Es posible que tenga `http://mysite/photo/myphoto.jpg` cuando realmente debería tener `http://mysite/photos/myphoto.jpg` en su lugar. El error tipográfico en la dirección URL principal (en este caso, *photo* en lugar de *fotos*) ha provocado el error.|
|**3728**|**adErrTreePermissionDenied**|Los permisos son insuficientes para acceder a árbol o subárbol. El usuario mencionado en la cadena de conexión no tiene los permisos adecuados.|
|**3729**|**adErrInvalidURL**|Dirección URL contiene caracteres no válidos. Asegúrese de que la dirección URL se ha escrito correctamente. La dirección URL sigue el esquema registrado para el proveedor actual (por ejemplo, el proveedor de publicación en Internet se registra para http).|
|**3730**|**adErrResourceLocked**|Objeto que representa la dirección URL especificada está bloqueado por uno o varios procesos. Espere a que finalice el proceso e intente la operación de nuevo. Se ha bloqueado el objeto que está intentando obtener acceso a otro usuario o por otro proceso en la aplicación. Esto es más probable que surgen en un entorno multiusuario.|
|**3731**|**adErrResourceExists**|No se puede realizar la operación de copia. Objeto con nombre mediante la dirección URL de destino ya existe. Especificar **adCopyOverwrite** para reemplazar el objeto. Si no especifica **adCopyOverwrite** al copiar los archivos en un directorio, la copia se produce un error al intentar copiar un elemento que ya existe en la ubicación de destino.|
|**3732**|**adErrCannotComplete**|El servidor no puede completar la operación. Esto podría ser porque el servidor está ocupado con otras operaciones o es posible que esté bajo de recursos.|
|**3733**|**adErrVolumeNotFound**|El proveedor no puede encontrar el dispositivo de almacenamiento indicado por la dirección URL. Asegúrese de que la dirección URL se ha escrito correctamente. La dirección URL del dispositivo de almacenamiento puede ser incorrecta, pero este error puede producirse por otras razones. El dispositivo podría estar sin conexión o un gran volumen de tráfico de red podría impedir que la conexión que se realicen.|
|**3734**|**adErrOutOfSpace**|No se puede realizar la operación. Proveedor no puede obtener suficiente espacio de almacenamiento. Es posible que no haya suficiente memoria RAM o espacio en disco para archivos temporales en el servidor.|
|**3735**|**adErrResourceOutOfScope**|Dirección URL de origen o destino está fuera del ámbito del registro actual.|
|**3736**|**adErrUnavailable**|No se pudo completar la operación y el estado no está disponible. El campo no esté disponible o no se intentó realizar la operación. Otro usuario podría ha cambiado o eliminado el campo que está intentando acceder.|
|**3737**|**adErrURLNamedRowDoesNotExist**|Esta dirección URL con el nombre de registro no existe. Al intentar abrir un archivo mediante un **registro** de objeto, el nombre de archivo o la ruta de acceso al archivo está mal escrito.|
|**3738**|**adErrDelResOutOfScope**|La dirección URL del objeto que va a eliminar está fuera del ámbito del registro actual.|
|**3747**|**adErrCatalogNotSet**|Operación requiere válido **ParentCatalog**.|
|**3748**|**adErrCantChangeConnection**|Se denegó la conexión. La nueva conexión que ha solicitado tiene características diferentes de lo que ya está en uso.|
|**3749**|**adErrFieldsUpdateFailed**|Error al actualizar los campos. Para obtener más información, examine el **estado** propiedad de cada objeto de campo. Este error puede producirse en dos situaciones: al cambiar un **campo** valor del objeto en el proceso de cambiar o agregar un registro a la base de datos; y al cambiar las propiedades de la **campo** propio objeto.<br /><br /> El **registro** o **Recordset** no se pudo actualizar debido a un problema con uno de los campos del registro actual. Enumerar el **campos** colección y compruebe el **estado** propiedad de cada campo para determinar la causa del problema.|
|**3750**|**adErrDenyNotSupported**|Proveedor no admite restricciones de uso compartido. Se ha intentado para restringir el uso compartido de archivos y el proveedor no admite el concepto.|
|**3751**|**adErrDenyTypeNotSupported**|Proveedor no admite el tipo solicitado de restricción de uso compartido. Se intentó establecer un tipo concreto de uso compartido de archivos restricción que no es compatible con su proveedor. Consulte la documentación del proveedor para determinar qué restricciones de uso compartido de archivos son compatibles.|
