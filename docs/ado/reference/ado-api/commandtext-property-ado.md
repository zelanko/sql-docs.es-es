---
title: Propiedad CommandText (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::CommandText
helpviewer_keywords:
- CommandText property [ADO]
ms.assetid: 4dd7e82a-8da5-4a4e-b439-11a29286fa0e
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 7ebc6a783aa8520c3ab16465143acdf1a6bf6628
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66698950"
---
# <a name="commandtext-property-ado"></a>Propiedad CommandText (ADO)
Indica el texto de un comando que se puede emitir en un proveedor.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Obtiene o establece un **cadena** valor que contiene un comando de proveedor, como una instrucción SQL, un nombre de tabla, una dirección URL relativa o una llamada a procedimiento almacenado. El valor predeterminado es una cadena vacía ("").  
  
## <a name="remarks"></a>Comentarios  
 Use la **CommandText** propiedad para establecer o devolver el texto de un comando representado por un [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto. Normalmente, esto será una instrucción SQL, pero también puede ser cualquier otro tipo de instrucción de comando reconocido por el proveedor, como una llamada a procedimiento almacenado. Una instrucción SQL debe tener el dialecto en concreto o versión admitida por el procesador de consultas del proveedor.  
  
 Si el [Prepared](../../../ado/reference/ado-api/prepared-property-ado.md) propiedad de la **comando** objeto se establece en **True** y **comando** objeto está enlazado a una conexión abierta cuando se establece el **CommandText** propiedad, ADO prepara la consulta (es decir, una forma compilada de la consulta que se almacena por el proveedor) cuando se llama a la [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) o [abrir](../../../ado/reference/ado-api/open-method-ado-connection.md)métodos.  
  
 En función de la [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md) la propiedad, ADO puede alterar el **CommandText** propiedad. Puede leer el **CommandText** propiedad en cualquier momento para ver el texto del comando real que ADO va a utilizar durante la ejecución.  
  
 Use la **CommandText** propiedad para establecer o devolver una dirección URL relativa que especifica un recurso, como un archivo o directorio. El recurso es relativo a una ubicación especificada explícitamente por una dirección URL absoluta, o implícitamente por una apertura [conexión](../../../ado/reference/ado-api/connection-object-ado.md) objeto.  
  
> [!NOTE]
>  Las direcciones URL con el esquema http, se invocarán automáticamente el [proveedor Microsoft OLE DB para la publicación en Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obtener más información, consulte [absoluto y las direcciones URL relativas](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [ActiveConnection, CommandText, CommandTimeout, CommandType, tamaño y ejemplo de propiedades de dirección (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, tamaño y ejemplo de propiedades de dirección (VC ++)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [Requery (método)](../../../ado/reference/ado-api/requery-method.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, tamaño y ejemplo de propiedades de dirección (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)
