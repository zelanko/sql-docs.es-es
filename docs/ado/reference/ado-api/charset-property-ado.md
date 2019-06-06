---
title: Juego de caracteres (propiedad, ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::Charset
helpviewer_keywords:
- Charset property [ADO]
ms.assetid: e42507cb-9b46-4ce4-8191-2948eaf14ca2
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: da9e41d594890b399be975a9f1465a6bff50010a
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66698804"
---
# <a name="charset-property-ado"></a>Propiedad de conjunto de caracteres (ADO)
Indica el juego de caracteres al que el contenido de un texto [Stream](../../../ado/reference/ado-api/stream-object-ado.md) debe convertirse para el almacenamiento en búfer interno de la **Stream** objeto.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un **cadena** establece el valor que especifica el carácter en la que el contenido de la **Stream** se va a traducir. El valor predeterminado es **Unicode**. Los valores permitidos son cadenas típicas pasadas a través de la interfaz como nombres de conjunto de caracteres de Internet (por ejemplo, "iso-8859-1", "Windows-1252" etc.). Para obtener una lista de los nombres de conjunto de caracteres que se conocen por un sistema, vea las subclaves de HKEY_CLASSES_ROOT\MIME\Database\Charset en el registro de Windows.  
  
## <a name="remarks"></a>Comentarios  
 En el texto **Stream** de objetos, datos de texto se almacenan en el juego de caracteres especificado por el **Charset** propiedad. El valor predeterminado es Unicode. El **Charset** propiedad se utiliza para convertir datos en el **Stream** o estará disponible fuera de la **Stream**. Por ejemplo, si la **Stream** contiene datos de ISO-8859-1 y que los datos se copian en una cadena BSTR, el **Stream** objeto convertirá los datos a Unicode. Lo contrario también es cierto.  
  
 Para que uno abierto **Stream**, actual [posición](../../../ado/reference/ado-api/position-property-ado.md) debe estar al principio de la **Stream** (0) para poder establecer **Charset**.  
  
 **Juego de caracteres** solo se usa con texto **Stream** objetos ([tipo](../../../ado/reference/ado-api/type-property-ado-stream.md) es **adTypeText**). Esta propiedad se omite si **tipo** es **adTypeBinary**.  
  
 Para obtener un ejemplo de código, vea [paso 4: Rellenar el cuadro de texto detalles](../../../ado/guide/data/step-4-populate-the-details-text-box.md).  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de secuencia (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
