---
title: "Método ReadText | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Stream::raw_ReadText
- _Stream::ReadText
helpviewer_keywords: ReadText method [ADO]
ms.assetid: be5a409e-cf87-4859-9ea5-713401755a77
caps.latest.revision: "16"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9915f0bfe1b70cef5cab39a058f7131ceaa44f98
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="readtext-method"></a>Método ReadText
Lee un número de caracteres del texto especificado [flujo](../../../ado/reference/ado-api/stream-object-ado.md) objeto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
String = Stream.ReadText ( NumChars)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *NumChars*  
 Opcional. A **largo** valor que especifica el número de caracteres que se va a leer el archivo, o un [StreamReadEnum](../../../ado/reference/ado-api/streamreadenum.md) valor. El valor predeterminado es **adReadAll**.  
  
## <a name="return-value"></a>Valor devuelto  
 El **ReadText** método lee un número especificado de caracteres, una línea completa o la totalidad de la secuencia de un **flujo** de objetos y devuelve la cadena resultante.  
  
## <a name="remarks"></a>Comentarios  
 Si *NumChar* es mayor que el número de caracteres quedan en la secuencia, se devuelven sólo los caracteres restantes. La cadena leída no se rellena para que coincida con la longitud especificada por *NumChar*. Si no hay ningún carácter restante para leer, se devuelve un valor de tipo variant cuyo valor es null. **ReadText** no se puede usar para leer hacia atrás.  
  
> [!NOTE]
>  El **ReadText** método se utiliza con secuencias de texto ([tipo](../../../ado/reference/ado-api/type-property-ado-stream.md) es **adTypeText**). Para secuencias binarias (**tipo** es **adTypeBinary**), utilice [lectura](../../../ado/reference/ado-api/read-method.md).  
  
 Las consultas que dan como resultado una gran cantidad de datos XML que se devuelven a través de la **ReadText** método del objeto de flujo de objeto de datos ActiveX (ADO) puede tardar una gran cantidad de tiempo de ejecución; si esto se hace en un componente COM + que se invoca desde una Página ASP, en la sesión del usuario se puede agotar el tiempo. ADO convierte datos de objeto de secuencia de codificación UTF-8 a Unicode; la reasignación de memoria frecuentes implicada en la conversión de una gran cantidad de datos a la vez lleva bastante tiempo. Para resolver, realizar llamadas repetidas a la **ReadText** método de la propiedad ADO objeto command y especifique un número más pequeño de caracteres. Las pruebas han demostrado que un valor equivalente a 128K (131.072) es óptimo. Tiempo de respuesta disminuye a medida que se reduce este valor. Para obtener más información, vea el artículo de Knowledge Base 280067, "PRB: recuperar documentos XML muy grandes de SQL Server 2000 mediante el método ReadText de objeto de secuencia de ADO puede ser lento", en Microsoft Knowledge Base en http://support.microsoft.com.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de secuencia (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Método Read](../../../ado/reference/ado-api/read-method.md)
