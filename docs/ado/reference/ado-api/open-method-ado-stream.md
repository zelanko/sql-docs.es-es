---
title: Abrir (método) (Stream de ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_Open
- _Stream::Open
helpviewer_keywords:
- Open method [ADO]
ms.assetid: d26f48fb-904e-4932-a245-3b4332ca1600
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0df165514a10bc667c8bd2cc6d2a8569faa79d11
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47611423"
---
# <a name="open-method-ado-stream"></a>Open (método) (Stream de ADO)
Se abre un [Stream](../../../ado/reference/ado-api/stream-object-ado.md) objeto para manipular secuencias de datos binarios o texto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Stream.Open Source, Mode , OpenOptions, UserName, Password  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Source*  
 Opcional. Un **Variant** valor que especifica el origen de datos para el **Stream**. *Origen* puede contener una cadena de dirección URL absoluta que apunta a un nodo existente en una estructura de árbol conocida, como un sistema de correo electrónico o archivo. Se debe especificar una dirección URL mediante la palabra clave de dirección URL ("URL =*esquema*://*server*/*carpeta*"). Como alternativa, *origen* puede contener una referencia a una ya está abierta [registro](../../../ado/reference/ado-api/record-object-ado.md) objeto, que se abre la secuencia predeterminada asociada con el **registro**. Si *origen* no se especifica un **Stream** se crea una instancia y abierto, asociada a ningún origen subyacente de forma predeterminada. Para obtener más información sobre los esquemas de dirección URL y sus proveedores asociados, consulte [absoluto y las direcciones URL relativas](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
 *Modo*  
 Opcional. Un [ConnectModeEnum](../../../ado/reference/ado-api/connectmodeenum.md) valor que especifica el modo de acceso para el resultado **Stream** (por ejemplo, lectura/escritura o de solo lectura). Valor predeterminado es **adModeUnknown**. Consulte la [modo](../../../ado/reference/ado-api/mode-property-ado.md) propiedad para obtener más información acerca de los modos de acceso. Si *modo* no se especifica, se ha heredado por el objeto de origen. Por ejemplo, si el origen **registro** se abre en modo de solo lectura, el **Stream** también se puede abrir en modo de solo lectura de forma predeterminada.  
  
 *OpenOptions*  
 Opcional. Un [StreamOpenOptionsEnum](../../../ado/reference/ado-api/streamopenoptionsenum.md) valor. Valor predeterminado es **adOpenStreamUnspecified**.  
  
 *UserName*  
 Opcional. Un **cadena** valor que contiene la identificación de usuario que, si es necesario, obtenga acceso a la **Stream** objeto.  
  
 *Contraseña*  
 Opcional. Un **cadena** valor que contiene la contraseña que, si es necesario, obtenga acceso a la **Stream** objeto.  
  
## <a name="remarks"></a>Comentarios  
 Cuando un **registro** objeto se pasa como parámetro de origen, el *UserID* y *contraseña* no se utilizan parámetros porque el acceso a la **registro** objeto ya está disponible. De forma similar, el [modo](../../../ado/reference/ado-api/mode-property-ado.md) de la **registro** objeto se transfiere a la **Stream** objeto. Cuando *origen* no se especifica, el **Stream** abierto no contiene datos y tiene un [tamaño](../../../ado/reference/ado-api/size-property-ado-stream.md) de cero (0). Para evitar la pérdida de datos que se escriben en esta **Stream** cuando el **Stream** está cerrada, guarde el **Stream** con el [CopyTo](../../../ado/reference/ado-api/copyto-method-ado.md) o [ SaveToFile](../../../ado/reference/ado-api/savetofile-method.md) métodos, o guardarla en otra ubicación de memoria.  
  
 Un *adOpenStreamFromRecord* valor de **OpenOptions** identifica el contenido de la *origen* parámetro sea ya estaba abierto **registro**objeto. El comportamiento predeterminado consiste en tratar *origen* como una dirección URL que apunte directamente a un nodo en una estructura de árbol, como un archivo. Se abre la secuencia predeterminada asociada con ese nodo.  
  
 Mientras el **Stream** es no está abierto, es posible leer todas las propiedades de solo lectura de la **Stream**. Si un **Stream** se abre de forma asincrónica, todas las operaciones siguientes (distinto comprobando el [estado](../../../ado/reference/ado-api/state-property-ado.md) y otras propiedades de solo lectura) se bloquean hasta que el **abierto** se ha completado la operación.  
  
 Además de las opciones que se trataron anteriormente, al no especificar *origen*, puede crear una instancia de un **Stream** objeto en la memoria sin asociarla a un origen subyacente. Puede agregar dinámicamente datos en la secuencia de escribir datos binarios o de texto en el **Stream** con [escribir](../../../ado/reference/ado-api/write-method.md) o [WriteText](../../../ado/reference/ado-api/writetext-method.md), o cargando datos desde un archivo con [ LoadFromFile](../../../ado/reference/ado-api/loadfromfile-method-ado.md).  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de secuencia (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Método Open (conexión de ADO)](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Método Open (Record ADO)](../../../ado/reference/ado-api/open-method-ado-record.md)   
 [Método Open (ADO Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Método OpenSchema](../../../ado/reference/ado-api/openschema-method.md)   
 [Método SaveToFile](../../../ado/reference/ado-api/savetofile-method.md)
