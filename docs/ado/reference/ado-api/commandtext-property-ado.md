---
title: Propiedad CommandText (ADO) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::CommandText
helpviewer_keywords:
- CommandText property [ADO]
ms.assetid: 4dd7e82a-8da5-4a4e-b439-11a29286fa0e
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8c333cd961ea8b4b3f37f78c682ebe65c7ac9001
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35276864"
---
# <a name="commandtext-property-ado"></a>Propiedad CommandText (ADO)
Indica el texto de un comando que se emita en un proveedor.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Obtiene o establece un **cadena** valor que contiene un comando de proveedor, como una instrucción SQL, un nombre de tabla, una dirección URL relativa o una llamada de procedimiento almacenado. El valor predeterminado es una cadena vacía ("").  
  
## <a name="remarks"></a>Notas  
 Use la **CommandText** propiedad para establecer o devolver el texto de un comando representado por un [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto. Normalmente esto será una instrucción SQL, pero también puede ser cualquier otro tipo de instrucción de comando reconocido por el proveedor, como una llamada de procedimiento almacenado. Una instrucción SQL debe tener el dialecto específico o versión admitida por el procesador de consultas del proveedor.  
  
 Si el [Prepared](../../../ado/reference/ado-api/prepared-property-ado.md) propiedad de la **comando** objeto se establece en **True** y **comando** objeto está enlazado a una conexión abierta cuando establece el **CommandText** propiedad, ADO preparará la consulta (es decir, una forma compilada de la consulta que se almacena por el proveedor) cuando se llama a la [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) o [abrir](../../../ado/reference/ado-api/open-method-ado-connection.md)métodos.  
  
 En función de la [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md) valor, de la propiedad ADO puede modificar el **CommandText** propiedad. Puede leer el **CommandText** propiedad en cualquier momento para ver el texto real del comando que ADO va a utilizar durante la ejecución.  
  
 Use la **CommandText** propiedad para establecer o devolver una dirección URL relativa que especifica un recurso, como un archivo o directorio. El recurso es relativo a una ubicación especificada explícitamente por una dirección URL absoluta o implícitamente mediante un formato de archivo [conexión](../../../ado/reference/ado-api/connection-object-ado.md) objeto.  
  
> [!NOTE]
>  Direcciones URL que utilizan el esquema http, se invocarán automáticamente el [proveedor Microsoft OLE DB para Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obtener más información, consulte [absoluto y direcciones URL relativas](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [ActiveConnection, CommandText, CommandTimeout, CommandType, tamaño y ejemplo de propiedades de dirección (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, tamaño y ejemplo de propiedades de dirección (VC ++)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [Requery (método)](../../../ado/reference/ado-api/requery-method.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, tamaño y ejemplo de propiedades de dirección (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)
