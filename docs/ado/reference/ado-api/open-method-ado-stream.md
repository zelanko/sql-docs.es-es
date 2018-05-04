---
title: Open (método) (Stream de ADO) | Documentos de Microsoft
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
- _Stream::raw_Open
- _Stream::Open
helpviewer_keywords:
- Open method [ADO]
ms.assetid: d26f48fb-904e-4932-a245-3b4332ca1600
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 44493854720564e241817c1b482339f9c5cbbd32
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="open-method-ado-stream"></a>Open (método) (Stream de ADO)
Se abre un [flujo](../../../ado/reference/ado-api/stream-object-ado.md) objeto para manipular secuencias de datos binarios o de texto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Stream.Open Source, Mode , OpenOptions, UserName, Password  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Source*  
 Opcional. A **Variant** valor que especifica el origen de datos para la **flujo**. *Origen* puede contener una cadena de dirección URL absoluta que apunta a un nodo existente en una estructura de árbol conocida, como un sistema de archivos o correo electrónico. Debe especificarse una dirección URL mediante la palabra clave de dirección URL ("URL =*esquema*://*server*/*carpeta*"). O bien, *origen* puede contener una referencia a una ya está abierto [registro](../../../ado/reference/ado-api/record-object-ado.md) objeto, que se abre la secuencia predeterminada asociada con el **registro**. Si *origen* no se especifica un **flujo** se crea una instancia y abierto, asociada a ningún origen subyacente de forma predeterminada. Para obtener más información sobre los esquemas de dirección URL y sus proveedores asociados, vea [absoluto y direcciones URL relativas](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
 *Modo*  
 Opcional. A [ConnectModeEnum](../../../ado/reference/ado-api/connectmodeenum.md) valor que especifica el modo de acceso para los resultantes **flujo** (por ejemplo, lectura/escritura o de solo lectura). Valor predeterminado es **adModeUnknown**. Consulte la [modo](../../../ado/reference/ado-api/mode-property-ado.md) propiedad para obtener más información acerca de los modos de acceso. Si *modo* no se especifica, se ha heredado por el objeto de origen. Por ejemplo, si el origen de **registro** se abre en modo de solo lectura, el **flujo** también se abrirá en modo de solo lectura de forma predeterminada.  
  
 *OpenOptions*  
 Opcional. A [StreamOpenOptionsEnum](../../../ado/reference/ado-api/streamopenoptionsenum.md) valor. Valor predeterminado es **adOpenStreamUnspecified**.  
  
 *UserName*  
 Opcional. A **cadena** valor que contiene la identificación del usuario que, si es necesario, obtenga acceso a la **flujo** objeto.  
  
 *Contraseña*  
 Opcional. A **cadena** valor que contiene la contraseña que, si es necesario, obtenga acceso a la **flujo** objeto.  
  
## <a name="remarks"></a>Comentarios  
 Cuando un **registro** objeto se pasa como el parámetro de origen, el *UserID* y *contraseña* no se utilizan parámetros porque el acceso a la **registro** objeto ya está disponible. De forma similar, el [modo](../../../ado/reference/ado-api/mode-property-ado.md) de la **registro** objeto se transfiere a la **flujo** objeto. Cuando *origen* no se especifica, el **flujo** abierto no contiene datos y tiene un [tamaño](../../../ado/reference/ado-api/size-property-ado-stream.md) de cero (0). Para evitar la pérdida de datos que se escriben en este **flujo** cuando el **flujo** es cerrado, guardar la **flujo** con el [CopyTo](../../../ado/reference/ado-api/copyto-method-ado.md) o [ SaveToFile](../../../ado/reference/ado-api/savetofile-method.md) métodos, o guardarlo en otra ubicación de memoria.  
  
 Un *adOpenStreamFromRecord* valo **OpenOptions** identifica el contenido de la *origen* parámetro que ya estaba abierto **registro**objeto. El comportamiento predeterminado consiste en tratar *origen* como una dirección URL que apunta directamente a un nodo en una estructura de árbol, como un archivo. Se abre la secuencia predeterminada asociada a ese nodo.  
  
 Mientras el **flujo** es no está abierto, es posible leer todas las propiedades de solo lectura de la **flujo**. Si un **flujo** se abrió de forma asincrónica, todas las operaciones subsiguientes (distinto de la comprobación de la [estado](../../../ado/reference/ado-api/state-property-ado.md) y otras propiedades de solo lectura) se bloquean hasta que el **abrir** se ha completado la operación.  
  
 Además de las opciones que se han expuesto anteriormente, si no especifica *origen*, puede crear una instancia de un **flujo** objeto en la memoria sin asociarla a un origen subyacente. Puede agregar datos dinámicamente a la secuencia escribiendo datos binarios o de texto a la **flujo** con [escribir](../../../ado/reference/ado-api/write-method.md) o [WriteText](../../../ado/reference/ado-api/writetext-method.md), o mediante la carga de datos desde un archivo con [ LoadFromFile](../../../ado/reference/ado-api/loadfromfile-method-ado.md).  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de secuencia (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Open (método) (conexión de ADO)](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Open (método) (registro de ADO)](../../../ado/reference/ado-api/open-method-ado-record.md)   
 [Open (método) (conjunto de registros ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Método OpenSchema](../../../ado/reference/ado-api/openschema-method.md)   
 [Método SaveToFile](../../../ado/reference/ado-api/savetofile-method.md)
