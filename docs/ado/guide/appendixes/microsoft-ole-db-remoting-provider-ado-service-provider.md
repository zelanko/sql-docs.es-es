---
title: Proveedor de servicios remotos de Microsoft OLE DB (proveedor de servicios de ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB remoting provider [ADO]
- providers [ADO], OLE DB remoting provider
- remoting provider [ADO]
ms.assetid: a4360ed4-b70f-4734-9041-4025d033346b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b0c58d6c90b67369f969a37cc2ad7e03cc6cad82
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47624613"
---
# <a name="microsoft-ole-db-remoting-provider-overview"></a>Introducción al proveedor de comunicación remota de Microsoft OLE DB
El proveedor de servicios remotos de Microsoft OLE DB permite que un usuario local en un equipo cliente invocar los proveedores de datos en un equipo remoto. Especifique los parámetros del proveedor de datos para la máquina remota como lo haría si fuera un usuario local en el equipo remoto. A continuación, especifique los parámetros utilizados por el proveedor de servicios remotos para tener acceso a la máquina remota. A continuación, puede tener acceso a la máquina remota como si fuera un usuario local.

> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo de Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Deben migrar las aplicaciones que usan RDS a [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).

## <a name="provider-keyword"></a>Palabra clave del proveedor
 Para invocar el proveedor OLE DB comunicación remota, especifique la siguiente palabra clave y valor en la cadena de conexión. (Tenga en cuenta el espacio en blanco en el nombre del proveedor).

```
"Provider=MS Remote"
```

## <a name="additional-keywords"></a>Palabras clave adicionales
 Cuando se invoca este proveedor de servicios, las palabras clave adicionales siguientes son relevantes.

|Palabra clave|Descripción|
|-------------|-----------------|
|**Origen de datos**|Especifica el nombre del origen de datos remoto. Se pasa al proveedor de servicios remotos de OLE DB para su procesamiento.<br /><br /> Esta palabra clave es equivalente a la [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) del objeto [Connect](../../../ado/reference/rds-api/connect-property-rds.md) propiedad.|

## <a name="dynamic-properties"></a>Propiedades dinámicas
 Cuando se invoca este proveedor de servicios, se agregan las siguientes propiedades dinámicas a la [conexión](../../../ado/reference/ado-api/connection-object-ado.md)del objeto [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) colección.

|Nombre de propiedad dinámica|Descripción|
|---------------------------|-----------------|
|**DFMode**|Indica el modo de DataFactory. Una cadena que especifica la versión deseada de la [DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) objeto en el servidor. Establezca esta propiedad antes de abrir una conexión para solicitar una versión concreta de la **DataFactory**. Si la versión solicitada no está disponible, se realizará un intento para usar la versión anterior. Si no hay ninguna versión anterior, se producirá un error. Si **DFMode** es menor que la versión disponible, se producirá un error. Esta propiedad es de solo lectura una vez realizada una conexión.<br /><br /> Puede ser uno de los siguientes valores de cadena válida:<br /><br /> -"25", versión 2.5 (valor predeterminado)<br />-"21", versión 2.1<br />-"20", versión 2.0<br />-"15", versión 1.5|
|**Propiedades de comando**|Indica los valores que se agregarán a la cadena de propiedades de comando (conjunto de filas) enviados al servidor por el proveedor MS Remote. El valor predeterminado de esta cadena es un vt_empty.|
|**DFMode actual**|Indica el número de versión real de la **DataFactory** en el servidor. Compruebe esta propiedad para ver si la versión solicitada en el **DFMode** propiedad se ha respetado.<br /><br /> Puede ser uno de los siguientes valores válidos de entero largo:<br /><br /> -25, versión 2.5 (valor predeterminado)<br />-21: versión 2.1<br />-20: versión 2.0<br />-15, versión 1.5<br /><br /> Adición de "DFMode = 20;" a la cadena de conexión cuando se usa el **MSRemote** proveedor puede mejorar el rendimiento del servidor durante la actualización de datos. Con esta configuración, el **RDSServer.DataFactory** objeto en el servidor usa un modo menos intensivo de recursos. Sin embargo, las siguientes características no están disponibles en esta configuración:<br /><br /> -Usar consultas parametrizadas.<br />-Obtención de información de parámetro o columna antes de llamar a la **Execute** método.<br />-Establecer **Transact actualizaciones** a **True**.<br />-Al obtener el estado de fila.<br />-Llamar el **Resync** método.<br />-Actualizar (explícita o automáticamente) a través de la **Update Resync** propiedad.<br />-Establecer **comando** o **Recordset** propiedades.<br />-Usar **adCmdTableDirect**.|
|**controlador**|Indica el nombre de un programa de personalización de servidor (o controlador) que amplía la funcionalidad de la [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)y todos los parámetros utilizados por el controlador *,* todas separadas por comas ( ","). Un valor **String**.|
|**Tiempo de espera de Internet**|Indica el número máximo de milisegundos de espera para que una solicitud de viaje hacia y desde el servidor. (El valor predeterminado es 5 minutos).|
|**Proveedor remoto**|Indica el nombre del proveedor de datos que se usará en el servidor remoto.|
|**Servidor remoto**|Indica el protocolo de nombre y la comunicación del servidor que va a usar esta conexión. Esta propiedad es equivalente a la [RDS. DataContro](../../../ado/reference/rds-api/datacontrol-object-rds.md) objeto [Server](../../../ado/reference/rds-api/server-property-rds.md) propiedad.|
|**Transact actualizaciones**|Cuando se establece en **True**, este valor indica que cuando [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) se lleva a cabo en el servidor, se llevará a cabo dentro de una transacción. El valor predeterminado de esta propiedad booleana dinámico es **False**.|

 También puede establecer propiedades dinámicas grabables especificando sus nombres como palabras clave en la cadena de conexión. Por ejemplo, establecer el **Internet Timeout** propiedad dinámica a cinco segundos especificando:

```
Dim cn as New ADODB.Connection
cn.Open "Provider=MS Remote;Internet Timeout=5000"
```

 También puede establecer o recuperar una propiedad dinámica especificando su nombre como índice de la **propiedades** propiedad. El ejemplo siguiente muestra cómo obtener e imprimir el valor actual de la **Internet Timeout** propiedad dinámica y, después, establezca un nuevo valor:

```
Debug.Print cn.Properties("Internet Timeout")
cn.Properties("Internet Timeout") = 5000
```

## <a name="remarks"></a>Comentarios
 En ADO 2.0, el proveedor OLE DB comunicación remota solo puede especificarse en el *ActiveConnection* parámetro de la [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto **abierto** método. A partir de ADO 2.1, el proveedor también se puede especificar en el *ConnectionString* parámetro de la [conexión](../../../ado/reference/ado-api/connection-object-ado.md) objeto **abierto** método.

 El equivalente de la **RDS. DataControl** objeto [SQL](../../../ado/reference/rds-api/sql-property.md) propiedad no está disponible. El [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto **abierto** método *origen* argumento se utiliza en su lugar.

 **Tenga en cuenta** especificando "...; Proveedor remoto = MS Remote;... "crearía un escenario de cuatro niveles. Escenarios de más de tres niveles no se han probado y no deberían ser necesario.

## <a name="example"></a>Ejemplo
 En este ejemplo realiza una consulta en el **autores** tabla de la **Pubs** base de datos en un servidor denominado *YourServer*. Los nombres del origen de datos remoto y el servidor remoto se proporcionan en el [abierto](../../../ado/reference/ado-api/open-method-ado-connection.md) método de la[conexión](../../../ado/reference/ado-api/connection-object-ado.md) objeto y la consulta SQL se especifica en el[abierto](../../../ado/reference/ado-api/open-method-ado-recordset.md) método de la [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto. Un **Recordset** objeto se devuelve, editar y usa para actualizar el origen de datos.

```
Dim rs as New ADODB.Recordset
Dim cn as New ADODB.Connection
cn.Open  "Provider=MS Remote;Data Source=pubs;" & _
         "Remote Server=http://YourServer"
rs.Open "SELECT * FROM authors", cn
...                'Edit the recordset
rs.UpdateBatch     'Equivalent of RDS SubmitChanges
...
```

## <a name="see-also"></a>Vea también
 [Información general sobre el proveedor de servicios remotos OLE DB](http://msdn.microsoft.com/4083b72f-68c4-4252-b366-abb70db5ca2b)
