---
title: Objeto Command (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command
helpviewer_keywords:
- Command object [ADO]
ms.assetid: a02c22fb-542d-465e-a629-30fd59dcbebf
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bbce299e2e9f67b705f940480913c7d8ac367d0d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67919796"
---
# <a name="command-object-ado"></a>Objeto Command (ADO)
Define un comando específico que se va a ejecutar en un origen de datos.  
  
## <a name="remarks"></a>Observaciones  
 Use un objeto de **comando** para consultar una base de datos y devolver registros en un objeto de [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) , para ejecutar una operación masiva o para manipular la estructura de una base de datos. Dependiendo de la funcionalidad del proveedor, algunas colecciones de **comandos** , métodos o propiedades pueden generar un error cuando se hace referencia a ellos.  
  
 Con las colecciones, los métodos y las propiedades de un objeto de **comando** , puede hacer lo siguiente:  
  
-   Defina el texto ejecutable del comando (por ejemplo, una instrucción SQL) con la propiedad [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) . O bien, para estructuras de comandos o de consultas que no sean cadenas simples (por ejemplo, consultas de plantilla XML), defina el comando con la propiedad [CommandStream](../../../ado/reference/ado-api/commandstream-property-ado.md) .  
  
-   Opcionalmente, indique el dialecto de comando usado en **CommandText** o **CommandStream** con la propiedad de [dialecto](../../../ado/reference/ado-api/dialect-property.md) .  
  
-   Defina consultas con parámetros o argumentos de procedimiento almacenado con objetos de [parámetro](../../../ado/reference/ado-api/parameter-object.md) y la colección de [parámetros](../../../ado/reference/ado-api/parameters-collection-ado.md) .  
  
-   Indica si los nombres de parámetro se deben pasar al proveedor con la propiedad [NamedParameters](../../../ado/reference/ado-api/namedparameters-property-ado.md) .  
  
-   Ejecute un comando y devuelva un objeto de **conjunto de registros** si es adecuado con el método [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) .  
  
-   Especifique el tipo de comando con la propiedad [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md) antes de la ejecución para optimizar el rendimiento.  
  
-   Controla si el proveedor guarda una versión preparada (o compilada) del comando antes de la ejecución con la propiedad [Prepared](../../../ado/reference/ado-api/prepared-property-ado.md) .  
  
-   Establezca el número de segundos que un proveedor esperará a que un comando se ejecute con la propiedad [CommandTimeout](../../../ado/reference/ado-api/commandtimeout-property-ado.md) .  
  
-   Asocie una conexión abierta a un objeto de **comando** estableciendo su propiedad [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) .  
  
-   Establezca la propiedad [nombre](../../../ado/reference/ado-api/name-property-ado.md) para identificar el objeto de **comando** como un método en el objeto de [conexión](../../../ado/reference/ado-api/connection-object-ado.md) asociado.  
  
-   Pase un objeto de **comando** a la propiedad de [origen](../../../ado/reference/ado-api/source-property-ado-recordset.md) de un **conjunto de registros** para obtener los datos.  
  
-   Obtener acceso a los atributos específicos del proveedor con la colección [Properties](../../../ado/reference/ado-api/properties-collection-ado.md) .  
  
> [!NOTE]
>  Para ejecutar una consulta sin usar un **objeto Command** , pase una cadena de consulta al método [Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md) de un objeto **Connection** o al método [Open](../../../ado/reference/ado-api/open-method-ado-recordset.md) de un objeto **Recordset** . Sin embargo, se requiere un objeto de **comando** si desea conservar el texto del comando y volver a ejecutarlo, o usar parámetros de consulta.  
  
 Para crear un objeto de **comando** independientemente de un objeto de **conexión** definido previamente, establezca su propiedad **ActiveConnection** en una cadena de conexión válida. ADO todavía crea un objeto de **conexión** , pero no asigna ese objeto a una variable de objeto. Sin embargo, si va a asociar varios objetos de **comando** con la misma conexión, debe crear y abrir explícitamente un objeto de **conexión** . Esto asigna el objeto de **conexión** a una variable de objeto. Asegúrese de que el objeto de **conexión** se ha abierto correctamente antes de asignarlo a la propiedad **ActiveConnection** del objeto de **comando** , ya que la asignación de un objeto de **conexión** cerrado produce un error. Si no establece la propiedad **ActiveConnection** del objeto de **comando** en esta variable de objeto, ADO crea un nuevo objeto de **conexión** para cada objeto de **comando** , incluso si utiliza la misma cadena de conexión.  
  
 Para ejecutar un **comando**, llámelo mediante su propiedad [Name](../../../ado/reference/ado-api/name-property-ado.md) en el objeto de **conexión** asociado. El **comando** debe tener su propiedad **ActiveConnection** establecida en el objeto de **conexión** . Si el **comando** tiene parámetros, pase sus valores como argumentos al método.  
  
 Si dos o más objetos de **comando** se ejecutan en la misma conexión y cualquier objeto de **comando** es un procedimiento almacenado con parámetros de salida, se produce un error. Para ejecutar cada objeto de **comando** , utilice conexiones independientes o desconecte todos los demás objetos de **comando** de la conexión.  
  
 La colección **Parameters** es el miembro predeterminado del objeto **Command** . Como resultado, las dos instrucciones de código siguientes son equivalentes.  
  
```  
objCmd.Parameters.Item(0)  
objCmd(0)  
```  
  
-   El objeto **Command** no es seguro para el scripting.  
  
 Esta sección contiene el siguiente tema.  
  
-   [Propiedades, métodos y eventos del objeto Command](../../../ado/reference/ado-api/command-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte también  
 [Connection (objeto) (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Parameters (colección) (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)   
 [Colección Properties (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Apéndice A: Proveedores](../../../ado/guide/appendixes/appendix-a-providers.md)
