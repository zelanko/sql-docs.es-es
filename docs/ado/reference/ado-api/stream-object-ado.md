---
title: Stream (objeto) (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Stream
helpviewer_keywords:
- Stream object [ADO]
ms.assetid: 0514531f-009d-4519-abc3-d727014a39f1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 976e822482efc530e3b055f61c242ee03a30e012
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47613863"
---
# <a name="stream-object-ado"></a>Objeto de secuencia (ADO)
Representa un flujo de datos binarios o texto.  
  
 En las jerarquías de estructura de árbol como un sistema de archivos o un sistema de correo electrónico, un [registro](../../../ado/reference/ado-api/record-object-ado.md) puede tener una secuencia binaria predeterminada de bits asociados que contiene el contenido del archivo o el correo electrónico. Un **Stream** objeto puede utilizarse para manipular campos o registros que contienen estas secuencias de datos. Un **Stream** puede obtenerse un objeto de las siguientes maneras:  
  
-   Desde una dirección URL que apunta a un objeto (normalmente un archivo) que contiene datos binarios o texto. Este objeto puede ser un documento simple, un **registro** objeto que representa un documento estructurado, o una carpeta.  
  
-   Abriendo el valor predeterminado **Stream** objeto asociado con un **registro** objeto. Puede obtener la secuencia predeterminada asociada con un **registro** objeto cuando la **registro** se abre, para eliminar una vuelta sólo para abrir la secuencia.  
  
-   Creando un **Stream** objeto. Estos **Stream** objetos pueden utilizarse para almacenar los datos para los fines de la aplicación. A diferencia de un **Stream** asociado con una dirección URL o el valor predeterminado **Stream** de un **registro**, con instancias **Stream** no tiene asociación con una origen subyacente de forma predeterminada.  
  
 Con los métodos y propiedades de un **Stream** objeto, puede hacer lo siguiente:  
  
-   Abra un **Stream** objeto desde un **registro** o la dirección URL con el [abierto](../../../ado/reference/ado-api/open-method-ado-stream.md) método.  
  
-   Cerrar un **Stream** con el [cerrar](../../../ado/reference/ado-api/close-method-ado.md) método.  
  
-   Entrada de bytes o texto en un **Stream** con el [escribir](../../../ado/reference/ado-api/write-method.md) y [WriteText](../../../ado/reference/ado-api/writetext-method.md) métodos.  
  
-   Leer los bytes desde el **Stream** con el [lectura](../../../ado/reference/ado-api/read-method.md) y [ReadText](../../../ado/reference/ado-api/readtext-method.md) métodos.  
  
-   Las escriba **Stream** del búfer de datos en la propiedad ADO al objeto subyacente con el [vaciar](../../../ado/reference/ado-api/flush-method-ado.md) método.  
  
-   Copie el contenido de un **Stream** a otro **Stream** con el [CopyTo](../../../ado/reference/ado-api/copyto-method-ado.md) método.  
  
-   Controlar cómo se leen las líneas del archivo de origen con la [SkipLine](../../../ado/reference/ado-api/skipline-method.md)método y el [LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md) propiedad.  
  
-   Determinar el final de la secuencia con el [EOS](../../../ado/reference/ado-api/eos-property.md)propiedad y [SetEOS](../../../ado/reference/ado-api/seteos-method.md) método.  
  
-   Guardar y restaurar datos en archivos con la [SaveToFile](../../../ado/reference/ado-api/savetofile-method.md)y [LoadFromFile](../../../ado/reference/ado-api/loadfromfile-method-ado.md) métodos.  
  
-   Especificar el juego de caracteres utilizado para almacenar el **Stream** con el [Charset](../../../ado/reference/ado-api/charset-property-ado.md) propiedad.  
  
-   Detener asincrónico **Stream** operación con el [cancelar](../../../ado/reference/ado-api/cancel-method-ado.md) método.  
  
-   Determinar el número de bytes en un **Stream** con el [tamaño](../../../ado/reference/ado-api/size-property-ado-stream.md) propiedad.  
  
-   Controlar la posición actual dentro de un **Stream** con el [posición](../../../ado/reference/ado-api/position-property-ado.md) propiedad.  
  
-   Determinar el tipo de datos en un **Stream** con el [tipo](../../../ado/reference/ado-api/type-property-ado-stream.md) propiedad.  
  
-   Determinar el estado actual de la **Stream** (cerrar, abrir o ejecutar) con el [estado](../../../ado/reference/ado-api/state-property-ado.md) propiedad.  
  
-   Especificar el modo de acceso para el **Stream** con el [modo](../../../ado/reference/ado-api/mode-property-ado.md) propiedad.  
  
> [!NOTE]
>  Las direcciones URL con el esquema http, se invocarán automáticamente el [proveedor Microsoft OLE DB para la publicación en Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obtener más información, consulte [absoluto y las direcciones URL relativas](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
 El **Stream** objeto es seguro para scripting.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Los eventos, métodos y propiedades del objeto Stream](../../../ado/reference/ado-api/stream-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vea también  
 [Registros y secuencias](../../../ado/guide/data/records-and-streams.md)
