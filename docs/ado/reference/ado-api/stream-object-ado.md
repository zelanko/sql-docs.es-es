---
title: Transmitir por secuencias (objeto) (ADO) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Stream
helpviewer_keywords:
- Stream object [ADO]
ms.assetid: 0514531f-009d-4519-abc3-d727014a39f1
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 32d4082ed203bc789ecb7dce03ce4ecfd422ceb7
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2018
---
# <a name="stream-object-ado"></a>Objeto de secuencia (ADO)
Representa un flujo de datos binarios o de texto.  
  
 En jerarquías con estructura de árbol como un sistema de archivos o un sistema de correo electrónico, un [registro](../../../ado/reference/ado-api/record-object-ado.md) puede tener una secuencia binaria predeterminada de bits asociados que contiene el contenido del archivo o el correo electrónico. A **flujo** objeto puede utilizarse para manipular campos o registros que contengan estas secuencias de datos. A **flujo** objeto puede obtenerse de las siguientes maneras:  
  
-   Desde una dirección URL que apunta a un objeto (normalmente un archivo) que contiene datos binarios o de texto. Este objeto puede ser un documento simple, un **registro** objeto que representa un documento estructurado, o una carpeta.  
  
-   Abriendo el valor predeterminado **flujo** objeto asociado con un **registro** objeto. Puede obtener la secuencia predeterminada asociada con un **registro** objeto cuando la **registro** se abre, para eliminar una ida y vuelta para abrir la secuencia.  
  
-   Creando un **flujo** objeto. Estos **flujo** objetos pueden utilizarse para almacenar los datos para los fines de la aplicación. A diferencia de un **flujo** asociado a una dirección URL o el valor predeterminado **flujo** de un **registro**, una instancia **flujo** no tiene ninguna asociación con un origen subyacente de forma predeterminada.  
  
 Con los métodos y propiedades de un **flujo** objeto, puede hacer lo siguiente:  
  
-   Abrir un **flujo** del objeto de un **registro** o dirección URL con el [abierto](../../../ado/reference/ado-api/open-method-ado-stream.md) método.  
  
-   Cerrar un **flujo** con el [cerrar](../../../ado/reference/ado-api/close-method-ado.md) método.  
  
-   Entrada bytes o texto en un **flujo** con el [escribir](../../../ado/reference/ado-api/write-method.md) y [WriteText](../../../ado/reference/ado-api/writetext-method.md) métodos.  
  
-   Leer los bytes de la **flujo** con el [lectura](../../../ado/reference/ado-api/read-method.md) y [ReadText](../../../ado/reference/ado-api/readtext-method.md) métodos.  
  
-   Escribir cualquier **flujo** del búfer de datos en la propiedad ADO para el objeto subyacente con el [vaciar](../../../ado/reference/ado-api/flush-method-ado.md) método.  
  
-   Copie el contenido de un **flujo** a otro **flujo** con el [CopyTo](../../../ado/reference/ado-api/copyto-method-ado.md) método.  
  
-   Controlar cómo se leen las líneas del archivo de origen con la [SkipLine](../../../ado/reference/ado-api/skipline-method.md)método y [separador de línea](../../../ado/reference/ado-api/lineseparator-property-ado.md) propiedad.  
  
-   Determinar el extremo de la posición de la secuencia con el [sobrecargas eléctricas](../../../ado/reference/ado-api/eos-property.md)propiedad y [SetEOS](../../../ado/reference/ado-api/seteos-method.md) método.  
  
-   Guardar y restaurar datos en archivos con la [SaveToFile](../../../ado/reference/ado-api/savetofile-method.md)y [LoadFromFile](../../../ado/reference/ado-api/loadfromfile-method-ado.md) métodos.  
  
-   Especifique el juego de caracteres utilizado para almacenar el **flujo** con el [Charset](../../../ado/reference/ado-api/charset-property-ado.md) propiedad.  
  
-   Detener una asincrónica **flujo** operación con el [cancelar](../../../ado/reference/ado-api/cancel-method-ado.md) método.  
  
-   Determinar el número de bytes en un **flujo** con el [tamaño](../../../ado/reference/ado-api/size-property-ado-stream.md) propiedad.  
  
-   Controlar la posición actual dentro de un **flujo** con el [posición](../../../ado/reference/ado-api/position-property-ado.md) propiedad.  
  
-   Determinar el tipo de datos en un **flujo** con el [tipo](../../../ado/reference/ado-api/type-property-ado-stream.md) propiedad.  
  
-   Determinar el estado actual de la **flujo** (cerrar, abrir o ejecutar) con el [estado](../../../ado/reference/ado-api/state-property-ado.md) propiedad.  
  
-   Especificar el modo de acceso para la **flujo** con el [modo](../../../ado/reference/ado-api/mode-property-ado.md) propiedad.  
  
> [!NOTE]
>  Direcciones URL que utilizan el esquema http, se invocarán automáticamente el [proveedor Microsoft OLE DB para Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obtener más información, consulte [absoluto y direcciones URL relativas](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
 El **flujo** objeto es seguro para scripting.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Eventos, métodos y propiedades del objeto de secuencia](../../../ado/reference/ado-api/stream-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vea también  
 [Registros y secuencias](../../../ado/guide/data/records-and-streams.md)
