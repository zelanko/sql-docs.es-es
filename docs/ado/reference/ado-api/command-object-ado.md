---
title: Comando (objeto) (ADO) | Documentos de Microsoft
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
- Command
helpviewer_keywords:
- Command object [ADO]
ms.assetid: a02c22fb-542d-465e-a629-30fd59dcbebf
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bf4a875b8ffbae9442f415fcf56d72809900da81
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="command-object-ado"></a>Objeto de comando (ADO)
Define un comando específico que se va a ejecutar en un origen de datos.  
  
## <a name="remarks"></a>Comentarios  
 Use un **comando** objeto para consultar una base de datos y devolver registros en un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto, para ejecutar una operación masiva, o para manipular la estructura de una base de datos. Dependiendo de la funcionalidad del proveedor, algunas **comando** colecciones, métodos o propiedades pueden generar un error al que se hace referencia.  
  
 Con las colecciones, métodos y propiedades de un **comando** de objeto, puede hacer lo siguiente:  
  
-   Definir el texto ejecutable del comando (por ejemplo, una instrucción SQL) con la [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) propiedad. O bien, para el comando o consulta de las estructuras no sea simple cadenas (por ejemplo, consultas de plantilla XML) definen el comando con el [CommandStream](../../../ado/reference/ado-api/commandstream-property-ado.md) propiedad.  
  
-   También puede indicar el dialecto del comando utilizado en el **CommandText** o **CommandStream** con el [dialecto](../../../ado/reference/ado-api/dialect-property.md) propiedad.  
  
-   Definir consultas parametrizadas o argumentos de procedimientos almacenados con [parámetro](../../../ado/reference/ado-api/parameter-object.md) objetos y [parámetros](../../../ado/reference/ado-api/parameters-collection-ado.md) colección.  
  
-   Indicar si los nombres de parámetro se deberían pasar al proveedor con el [NamedParameters](../../../ado/reference/ado-api/namedparameters-property-ado.md) propiedad.  
  
-   Ejecutar un comando y devolver un **Recordset** objeto si procede, con el [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) método.  
  
-   Especificar el tipo de comando con el [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md) propiedad antes de la ejecución para optimizar el rendimiento.  
  
-   Controlar si el proveedor guarda una versión preparada (o compilada) del comando antes de la ejecución con el [Prepared](../../../ado/reference/ado-api/prepared-property-ado.md) propiedad.  
  
-   Establecer el número de segundos que esperará un proveedor para que un comando para ejecutar con la [CommandTimeout](../../../ado/reference/ado-api/commandtimeout-property-ado.md) propiedad.  
  
-   Asociar una conexión abierta con un **comando** objeto estableciendo su [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) propiedad.  
  
-   Establecer el [nombre](../../../ado/reference/ado-api/name-property-ado.md) propiedad para identificar el **comando** objeto como un método en el asociado [conexión](../../../ado/reference/ado-api/connection-object-ado.md) objeto.  
  
-   Pasar un **comando** el objeto a la [origen](../../../ado/reference/ado-api/source-property-ado-recordset.md) propiedad de un **Recordset** para obtener los datos.  
  
-   Obtener acceso a atributos específicos del proveedor con el [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) colección.  
  
> [!NOTE]
>  Para ejecutar una consulta sin utilizar un **comando** de objetos, pasar una cadena de consulta a la [Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md) método de un **conexión** objeto o a la [abrir](../../../ado/reference/ado-api/open-method-ado-recordset.md)método de un **Recordset** objeto. Sin embargo, un **comando** objeto es necesaria cuando desea conservar el texto del comando y volver a ejecutarlo o usar parámetros de consulta.  
  
 Para crear un **comando** objeto independientemente definido anteriormente **conexión** de objetos, establecer su **ActiveConnection** propiedad en una cadena de conexión válida. ADO sigue creando una **conexión** objeto, pero no asignará ese objeto a una variable de objeto. Sin embargo, si va a asociar varios **comando** objetos que tienen la misma conexión, debe crear y abrir explícitamente un **conexión** objeto; esta asigna el **conexión** objeto a una variable de objeto. Asegúrese de que el **conexión** objeto se abrió correctamente antes de asignarlo a la **ActiveConnection** propiedad de la **comando** objeto, porque la asignación de un cerrado **conexión** objeto produce un error. Si no establece la **ActiveConnection** propiedad de la **comando** el objeto a esta variable de objeto ADO crea un nuevo **conexión** para cada objeto  **Comando** objeto, incluso si utiliza la misma cadena de conexión.  
  
 Para ejecutar un **comando**, llamarlo su [nombre](../../../ado/reference/ado-api/name-property-ado.md) propiedad asociado **conexión** objeto. El **comando** debe tener su **ActiveConnection** propiedad establecida en el **conexión** objeto. Si el **comando** tiene parámetros, pase sus valores como argumentos al método.  
  
 Si dos o más **comando** los objetos se ejecutan en la misma conexión y, o bien **comando** objeto es un procedimiento almacenado con parámetros de salida, se produce un error. Para ejecutar cada uno de ellos **comando** objeto, use conexiones independientes o desconecte todos los demás **comando** objetos de la conexión.  
  
 El **parámetros** colección es el miembro predeterminado de la **comando** objeto. Como resultado, las dos instrucciones de código siguientes son equivalentes.  
  
```  
objCmd.Parameters.Item(0)  
objCmd(0)  
```  
  
-   El **comando** objeto no es seguro para scripting.  
  
 Esta sección contiene el siguiente tema.  
  
-   [Propiedades del objeto de comando, métodos y eventos](../../../ado/reference/ado-api/command-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vea también  
 [Objeto de conexión (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Colección de parámetros (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)   
 [Colección de propiedades (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Apéndice A: Proveedores](../../../ado/guide/appendixes/appendix-a-providers.md)
