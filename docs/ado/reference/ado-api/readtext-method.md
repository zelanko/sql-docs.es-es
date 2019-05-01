---
title: Método ReadText | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_ReadText
- _Stream::ReadText
helpviewer_keywords:
- ReadText method [ADO]
ms.assetid: be5a409e-cf87-4859-9ea5-713401755a77
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b095e034df987fd580b5f5855993c9cf070a1236
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63278606"
---
# <a name="readtext-method"></a>Método ReadText
Lee un número de caracteres de un texto especificado [Stream](../../../ado/reference/ado-api/stream-object-ado.md) objeto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
String = Stream.ReadText ( NumChars)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *NumChars*  
 Opcional. Un **largo** valor que especifica el número de caracteres que se va a leer el archivo, o un [StreamReadEnum](../../../ado/reference/ado-api/streamreadenum.md) valor. El valor predeterminado es **adReadAll**.  
  
## <a name="return-value"></a>Valor devuelto  
 El **ReadText** método lee un número especificado de caracteres, una línea completa o la totalidad de la secuencia desde un **Stream** de objetos y devuelve la cadena resultante.  
  
## <a name="remarks"></a>Comentarios  
 Si *NumChar* es mayor que el número de caracteres restante en la secuencia, se devuelven solo los caracteres restantes. La cadena de lectura no se rellena para que coincida con la longitud especificada por *NumChar*. Si no hay ningún carácter restante para leer, se devuelve una variante cuyo valor es null. **ReadText** no se puede usar para leer hacia atrás.  
  
> [!NOTE]
>  El **ReadText** método se utiliza con secuencias de texto ([tipo](../../../ado/reference/ado-api/type-property-ado-stream.md) es **adTypeText**). Para secuencias binarias (**tipo** es **adTypeBinary**), utilice [lectura](../../../ado/reference/ado-api/read-method.md).  
  
 Las consultas que producen una gran cantidad de datos XML devueltos a través de la **ReadText** método del objeto Stream de objeto de datos ActiveX (ADO) puede tardar mucho tiempo en ejecutarse; si esto se realiza en un componente COM + que se invoca desde una Página ASP, la sesión del usuario puede agotar el tiempo. ADO convierte datos del objeto Stream de codificación UTF-8 a Unicode; la reasignación de memoria frecuentes implicada en la conversión de una gran cantidad de datos a la vez es bastante lenta. Para resolver, realizar llamadas repetidas a la **ReadText** método de ADO, el objeto command y especifique un número menor de caracteres. Las pruebas han demostrado que un valor equivalente a 128K (131.072) es óptimo. Tiempo de respuesta disminuye a medida que se reduce este valor. Para obtener más información, consulte el artículo de Knowledge Base 280067, "PRB: Recuperar documentos XML muy grandes de SQL Server 2000 mediante el método ReadText del objeto stream de ADO puede resultar lento", en Microsoft Knowledge Base en https://support.microsoft.com.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de secuencia (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Método Read](../../../ado/reference/ado-api/read-method.md)
