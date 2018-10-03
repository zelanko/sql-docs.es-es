---
title: Objeto de conexión (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection
helpviewer_keywords:
- Connection object [ADO]
ms.assetid: ef6b1824-5b12-43db-89d7-8f3d13896d4d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4a3b13402f20c149c438aa5a2c678afb068fb0f3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47623993"
---
# <a name="connection-object-ado"></a>Objeto de conexión (ADO)
Representa una conexión abierta a un origen de datos.  
  
## <a name="remarks"></a>Comentarios  
 Un **conexión** objeto representa una única sesión con un origen de datos. En un sistema de base de datos cliente/servidor, puede ser equivalente a una conexión de red real con el servidor. Dependiendo de la funcionalidad admitida por el proveedor, algunas colecciones, métodos o propiedades de un **conexión** objeto no esté disponible.  
  
 Con las colecciones, métodos y propiedades de un **conexión** objeto, puede hacer lo siguiente:  
  
-   Configurar la conexión antes de abrirlo con la [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md), [ConnectionTimeout](../../../ado/reference/ado-api/connectiontimeout-property-ado.md), y [modo](../../../ado/reference/ado-api/mode-property-ado.md) propiedades. **ConnectionString** es la propiedad predeterminada de la **conexión** objeto.  
  
-   Establecer el [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) propiedad al cliente para invocar el [servicio de cursores de Microsoft para OLE DB](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md), que es compatible con las actualizaciones de batch.  
  
-   Establecer la base de datos predeterminada para la conexión con el [DefaultDatabase](../../../ado/reference/ado-api/defaultdatabase-property.md) propiedad.  
  
-   El nivel de aislamiento para las transacciones abierto en la conexión con el conjunto del [IsolationLevel](../../../ado/reference/ado-api/isolationlevel-property.md) propiedad.  
  
-   Especificar un proveedor OLE DB con la [proveedor](../../../ado/reference/ado-api/provider-property-ado.md) propiedad.  
  
-   Establecer y, posteriormente, interrumpir la conexión física al origen de datos con el [abierto](../../../ado/reference/ado-api/open-method-ado-connection.md) y [cerrar](../../../ado/reference/ado-api/close-method-ado.md) métodos.  
  
-   Ejecutar un comando en la conexión con el [Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md) método y configure la ejecución con el [CommandTimeout](../../../ado/reference/ado-api/commandtimeout-property-ado.md) propiedad.  
  
    > [!NOTE]
    >  Para ejecutar una consulta sin utilizar un objeto de comando, pase una cadena de consulta a la **Execute** método de un **conexión** objeto. Sin embargo, un [comando](../../../ado/reference/ado-api/command-object-ado.md) se requiere el objeto cuando desea conservar el texto del comando y vuelva a ejecutarla o usar parámetros de consulta.  
  
-   Administrar transacciones en la conexión abierta, incluidas las transacciones anidadas si el proveedor es compatible con ellos, con el [BeginTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md), [CommitTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md), y [RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) los métodos y las [atributos](../../../ado/reference/ado-api/attributes-property-ado.md) propiedad.  
  
-   Examinar los errores devueltos desde el origen de datos con el [errores](../../../ado/reference/ado-api/errors-collection-ado.md) colección.  
  
-   Leer la versión de la implementación de ADO utilizada con el [versión](../../../ado/reference/ado-api/version-property-ado.md) propiedad.  
  
-   Obtener información de esquema de la base de datos con el [OpenSchema](../../../ado/reference/ado-api/openschema-method.md) método.  
  
 Puede crear **conexión** objetos independientemente de cualquier otro objeto definido anteriormente.  
  
 Puede ejecutar comandos con nombre o los procedimientos almacenados como si fueran métodos nativos en un **conexión** de objeto, como se muestra en la sección siguiente. Cuando un comando con nombre tiene el mismo nombre que el de un procedimiento almacenado, invocar la llamada de método nativo"" en un **conexión** objeto siempre ejecutar el comando con nombre en lugar del procedimiento almacenado.  
  
> [!NOTE]
>  No use esta característica (llamar a un procedimiento almacenado o un comando con nombre como si fuera un método nativo en el **conexión** objeto) en una aplicación de Microsoft® .NET Framework, porque la implementación subyacente de los conflictos de característica con la forma en que .NET Framework interopera con COM.  
  
## <a name="execute-a-command-as-a-native-method-of-a-connection-object"></a>Ejecutar un comando como un método nativo de un objeto de conexión  
 Para ejecutar un comando, asigne el comando un nombre con el **comando** objeto [nombre](../../../ado/reference/ado-api/name-property-ado.md) propiedad. Establecer el **ActiveConnection** propiedad de la **comando** objeto a la conexión. A continuación, emita una instrucción donde se usa el nombre de comando como si fuera un método en el **conexión** objeto seguida de cualquier parámetro y un **Recordset** objeto si se devuelven filas. Establecer el **Recordset** propiedades para personalizar resultante **Recordset**. Por ejemplo:  
  
```  
Dim cnn As New ADODB.Connection  
Dim cmd As New ADODB.Command  
Dim rst As New ADODB.Recordset  
...  
cnn.Open "..."  
cmd.Name = "yourCommandName"  
cmd.ActiveConnection = cnn  
...  
'Your command name, any parameters, and an optional Recordset.  
cnn. "parameter", rst  
```  
  
## <a name="execute-a-stored-procedure-as-a-native-method-of-a-connection-object"></a>Ejecutar un procedimiento almacenado como un método nativo de un objeto de conexión  
 Para ejecutar un procedimiento almacenado, emita una instrucción donde se usa el nombre del procedimiento almacenado como si fuera un método en el **conexión** objeto, seguido de los parámetros. ADO hará que una "mejor aproximación" tipos de parámetros. Por ejemplo:  
  
```  
Dim cnn As New ADODB.Connection  
...  
'Your stored procedure name and any parameters.  
cnn. "parameter"  
```  
  
 El **conexión** objeto es seguro para scripting.  
  
 Esta sección contiene el siguiente tema.  
  
-   [Los eventos, métodos y propiedades del objeto de conexión](../../../ado/reference/ado-api/connection-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vea también  
 [Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)   
 [Colección de errores (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)   
 [Colección de propiedades (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Apéndice A: Proveedores](../../../ado/guide/appendixes/appendix-a-providers.md)
