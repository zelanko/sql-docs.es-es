---
title: Propiedad CommandText (ADO) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Command15::CommandText
helpviewer_keywords:
- CommandText property [ADO]
ms.assetid: 4dd7e82a-8da5-4a4e-b439-11a29286fa0e
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 60ee83c7d1f667feb0b1fcb4985dcd50edfda27b
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="commandtext-property-ado"></a>Propiedad CommandText (ADO)
Indica el texto de un comando que se emita en un proveedor.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Obtiene o establece un **cadena** valor que contiene un comando de proveedor, como una instrucción SQL, un nombre de tabla, una dirección URL relativa o una llamada de procedimiento almacenado. El valor predeterminado es una cadena vacía ("").  
  
## <a name="remarks"></a>Comentarios  
 Use la **CommandText** propiedad para establecer o devolver el texto de un comando representado por un [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto. Normalmente esto será una instrucción SQL, pero también puede ser cualquier otro tipo de instrucción de comando reconocido por el proveedor, como una llamada de procedimiento almacenado. Una instrucción SQL debe tener el dialecto específico o versión admitida por el procesador de consultas del proveedor.  
  
 Si el [Prepared](../../../ado/reference/ado-api/prepared-property-ado.md) propiedad de la **comando** objeto se establece en **True** y **comando** objeto está enlazado a una conexión abierta cuando establece el **CommandText** propiedad, ADO preparará la consulta (es decir, una forma compilada de la consulta que se almacena por el proveedor) cuando se llama a la [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) o [abrir](../../../ado/reference/ado-api/open-method-ado-connection.md)métodos.  
  
 En función de la [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md) valor, de la propiedad ADO puede modificar el **CommandText** propiedad. Puede leer el **CommandText** propiedad en cualquier momento para ver el texto real del comando que ADO va a utilizar durante la ejecución.  
  
 Use la **CommandText** propiedad para establecer o devolver una dirección URL relativa que especifica un recurso, como un archivo o directorio. El recurso es relativo a una ubicación especificada explícitamente por una dirección URL absoluta o implícitamente mediante un formato de archivo [conexión](../../../ado/reference/ado-api/connection-object-ado.md) objeto.  
  
> [!NOTE]
>  Direcciones URL que utilizan el esquema http, se invocarán automáticamente el [proveedor Microsoft OLE DB para Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obtener más información, consulte [absoluto y direcciones URL relativas](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de comando (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [ActiveConnection, CommandText, CommandTimeout, CommandType, tamaño y ejemplo de propiedades de dirección (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, tamaño y ejemplo de propiedades de dirección (VC ++)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [Requery (método)](../../../ado/reference/ado-api/requery-method.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, tamaño y ejemplo de propiedades de dirección (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)

