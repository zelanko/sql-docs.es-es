---
title: Comando (objeto) (ADO) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: ab3348906affc9a1c1a4b5471de861831992dc32
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63126800"
---
# <a name="command-object-ado"></a>Objeto Command (ADO)
Define un comando específico que se va a ejecutar en un origen de datos.  
  
## <a name="remarks"></a>Comentarios  
 Use un **comando** objeto para consultar una base de datos y devolver los registros en un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto, para ejecutar una operación masiva, o para manipular la estructura de una base de datos. Según la funcionalidad del proveedor, algunos **comando** colecciones, métodos o propiedades pueden generar un error que se hace referencia.  
  
 Con las colecciones, métodos y propiedades de un **comando** de objeto, puede hacer lo siguiente:  
  
-   Definir el texto ejecutable del comando (por ejemplo, una instrucción SQL) con el [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) propiedad. Como alternativa, para el comando o consulta estructuras distinto simple cadenas (por ejemplo, consultas de plantilla XML) definen el comando con el [CommandStream](../../../ado/reference/ado-api/commandstream-property-ado.md) propiedad.  
  
-   También puede indicar el dialecto del comando utilizado en el **CommandText** o **CommandStream** con el [dialecto](../../../ado/reference/ado-api/dialect-property.md) propiedad.  
  
-   Definir consultas parametrizadas o argumentos de procedimiento almacenado con [parámetro](../../../ado/reference/ado-api/parameter-object.md) objetos y el [parámetros](../../../ado/reference/ado-api/parameters-collection-ado.md) colección.  
  
-   Indicar si los nombres de parámetro se deben pasar al proveedor con el [NamedParameters](../../../ado/reference/ado-api/namedparameters-property-ado.md) propiedad.  
  
-   Ejecutar un comando y devolver un **Recordset** objeto si es necesario con el [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) método.  
  
-   Especificar el tipo de comando con el [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md) propiedad antes de la ejecución para optimizar el rendimiento.  
  
-   Controlar si el proveedor guarda una versión preparada (o compilada) del comando antes de la ejecución con el [Prepared](../../../ado/reference/ado-api/prepared-property-ado.md) propiedad.  
  
-   Establecer el número de segundos que esperará un proveedor de un comando con el [CommandTimeout](../../../ado/reference/ado-api/commandtimeout-property-ado.md) propiedad.  
  
-   Asociar una conexión abierta con un **comando** objeto estableciendo sus [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) propiedad.  
  
-   Establecer el [nombre](../../../ado/reference/ado-api/name-property-ado.md) propiedad para identificar el **comando** objeto como un método en el asociado [conexión](../../../ado/reference/ado-api/connection-object-ado.md) objeto.  
  
-   Pasar un **comando** de objeto para el [origen](../../../ado/reference/ado-api/source-property-ado-recordset.md) propiedad de un **Recordset** para obtener los datos.  
  
-   Obtener acceso a atributos específicos del proveedor con el [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) colección.  
  
> [!NOTE]
>  Para ejecutar una consulta sin utilizar un **comando** de objeto, pase una cadena de consulta a la [Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md) método de un **conexión** objeto o a la [abrir](../../../ado/reference/ado-api/open-method-ado-recordset.md)método de un **Recordset** objeto. Sin embargo, un **comando** se requiere el objeto cuando desea conservar el texto del comando y vuelva a ejecutarla o usar parámetros de consulta.  
  
 Para crear un **comando** objeto independientemente definidos previamente **conexión** de objetos, establezca su **ActiveConnection** propiedad en una cadena de conexión válida. ADO sigue creando un **conexión** objeto, pero no asignará ese objeto a una variable de objeto. Sin embargo, si va a asociar varios **comando** los objetos que tienen la misma conexión, debe crear y abrir explícitamente un **conexión** objeto; este asigna el **conexión** objeto a una variable de objeto. Asegúrese de que el **conexión** se abrió correctamente al objeto antes de asignarlo a la **ActiveConnection** propiedad de la **comando** objeto, porque la asignación de un cerrado **conexión** objeto produce un error. Si no establece la **ActiveConnection** propiedad de la **comando** oponerse a esta variable de objeto, crea un nuevo ADO **conexión** para cada objeto  **Comando** objeto, incluso si usa la misma cadena de conexión.  
  
 Para ejecutar un **comando**, invocarlo mediante su [nombre](../../../ado/reference/ado-api/name-property-ado.md) propiedad asociado **conexión** objeto. El **comando** debe tener su **ActiveConnection** propiedad establecida en el **conexión** objeto. Si el **comando** tiene parámetros, pase sus valores como argumentos al método.  
  
 Si dos o más **comando** los objetos que se ejecutan en la misma conexión y, o bien **comando** objeto es un procedimiento almacenado con parámetros de salida, se produce un error. Para ejecutar cada **comando** objeto, use conexiones independientes o desconecte todos los demás **comando** objetos desde la conexión.  
  
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
 [Apéndice A: proveedores](../../../ado/guide/appendixes/appendix-a-providers.md)
