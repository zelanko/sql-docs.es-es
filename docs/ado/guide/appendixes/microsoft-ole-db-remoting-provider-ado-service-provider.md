---
title: Proveedor de servicios remotos de Microsoft OLE DB (proveedor de servicios de ADO) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB remoting provider [ADO]
- providers [ADO], OLE DB remoting provider
- remoting provider [ADO]
ms.assetid: a4360ed4-b70f-4734-9041-4025d033346b
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 125ec1708c93abf78b4d4fa4663b287579d45f5e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="microsoft-ole-db-remoting-provider-overview"></a>Introducción al proveedor Microsoft OLE DB comunicación remota
El proveedor de servicios remotos de Microsoft OLE DB permite a un usuario local en un equipo cliente invocar proveedores de datos en un equipo remoto. Especifique los parámetros de proveedor de datos para el equipo remoto tal y como lo haría si fuese un usuario local en el equipo remoto. A continuación, especifique los parámetros utilizados por el proveedor de servicios remotos para tener acceso a la máquina remota. A continuación, puede tener acceso a la máquina remota como si fuera un usuario local.

> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar a [servicio de datos de WCF](http://go.microsoft.com/fwlink/?LinkId=199565).

## <a name="provider-keyword"></a>Palabra clave del proveedor
 Para invocar el proveedor de servicios remotos de OLE DB, especifique la siguiente palabra clave y valor en la cadena de conexión. (Tenga en cuenta el espacio en blanco en el nombre del proveedor).

```
"Provider=MS Remote"
```

## <a name="additional-keywords"></a>Palabras clave adicionales
 Cuando se invoca este proveedor de servicios, las siguientes palabras clave adicionales son relevantes.

|Palabra clave|Description|
|-------------|-----------------|
|**Origen de datos**|Especifica el nombre del origen de datos remoto. Se pasa al proveedor de servicios remotos de OLE DB para su procesamiento.<br /><br /> Esta palabra clave es equivalente a la [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) del objeto [conectar](../../../ado/reference/rds-api/connect-property-rds.md) propiedad.|

## <a name="dynamic-properties"></a>Propiedades dinámicas
 Cuando se invoca este proveedor de servicios, se agregan las siguientes propiedades dinámicas a la [conexión](../../../ado/reference/ado-api/connection-object-ado.md)del objeto [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) colección.

|Nombre de la propiedad dinámica|Description|
|---------------------------|-----------------|
|**DFMode**|Indica el modo DataFactory. Una cadena que especifica la versión deseada de la [DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) objeto en el servidor. Establezca esta propiedad antes de abrir una conexión para solicitar una versión concreta de la **DataFactory**. Si la versión solicitada no está disponible, se realizará un intento para usar la versión anterior. Si no hay ninguna versión anterior, se producirá un error. Si **DFMode** es menor que la versión disponible, se producirá un error. Esta propiedad es de solo lectura una vez realizada una conexión.<br /><br /> Puede ser uno de los siguientes valores de cadena válida:<br /><br /> -"25" — versión 2.5 (valor predeterminado)<br />-"21", versión 2.1<br />-"20", versión 2.0<br />-"15", versión 1.5|
|**Propiedades de comando**|Indica los valores que se agregarán a la cadena de propiedades de comando (conjunto de filas) enviados al servidor por el proveedor MS Remote. El valor predeterminado de esta cadena es vt_empty.|
|**DFMode actual**|Indica el número de versión real de la **DataFactory** en el servidor. Compruebe esta propiedad para ver si la versión solicitada en la **DFMode** se respeta la propiedad.<br /><br /> Puede ser uno de los siguientes valores de entero largo válido:<br /><br /> -25: versión 2.5 (valor predeterminado)<br />-21: versión 2.1<br />-20: versión 2.0<br />-15: versión 1.5<br /><br /> Adición de "DFMode = 20;" a la cadena de conexión cuando se usa el **MSRemote** proveedor puede mejorar el rendimiento del servidor durante la actualización de datos. Con esta configuración, el **RDSServer.DataFactory** objeto en el servidor usa el modo de requiere menos recursos. Sin embargo, las siguientes características no están disponibles en esta configuración:<br /><br /> -Uso de consultas parametrizadas.<br />-Obtención de información de parámetro o columna antes de llamar a la **Execute** método.<br />-Establecer **Transact actualizaciones** a **True**.<br />-Obtener el estado de fila.<br />-Una llamada a la **Resync** método.<br />-Actualización (de forma explícita o automáticamente) a través de la **Update Resync** propiedad.<br />-Establecer **comando** o **conjunto de registros** propiedades.<br />-Uso **adCmdTableDirect**.|
|**Controlador**|Indica el nombre de un programa de personalización de servidor (o controlador) que amplía la funcionalidad de la [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)y todos los parámetros utilizados por el controlador *,* todas separadas por comas ( ","). A **cadena** valor.|
|**Tiempo de espera de Internet**|Indica el número máximo de milisegundos de espera para que una solicitud viajar a y desde el servidor. (El valor predeterminado es 5 minutos).|
|**Proveedor remoto**|Indica el nombre del proveedor de datos que se usará en el servidor remoto.|
|**Servidor remoto**|Indica el protocolo de nombre y la comunicación del servidor que va a usar esta conexión. Esta propiedad es equivalente a la [RDS. DataContro](../../../ado/reference/rds-api/datacontrol-object-rds.md) objeto [Server](../../../ado/reference/rds-api/server-property-rds.md) propiedad.|
|**Transact actualizaciones**|Cuando se establece en **True**, este valor indica que, cuando [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) se lleva a cabo en el servidor, se llevará a cabo dentro de una transacción. El valor predeterminado de esta propiedad dinámica booleana es **False**.|

 También puede establecer propiedades dinámicas escritura especificando sus nombres como palabras clave en la cadena de conexión. Por ejemplo, establecer el **tiempo de espera de Internet** propiedades dinámicas en cinco segundos al especificar:

```
Dim cn as New ADODB.Connection
cn.Open "Provider=MS Remote;Internet Timeout=5000"
```

 También puede establecer o recuperar una propiedad dinámica al especificar su nombre como el índice de la **propiedades** propiedad. En el ejemplo siguiente se muestra cómo obtener e imprimir el valor actual de la **tiempo de espera de Internet** propiedad dinámica y, a continuación, establezca un nuevo valor:

```
Debug.Print cn.Properties("Internet Timeout")
cn.Properties("Internet Timeout") = 5000
```

## <a name="remarks"></a>Comentarios
 En ADO 2.0, solo se podía especificar el proveedor de servicios remotos de OLE DB en el *ActiveConnection* parámetro de la [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto **abiertos** método. A partir de ADO 2.1, el proveedor también se puede especificar en el *ConnectionString* parámetro de la [conexión](../../../ado/reference/ado-api/connection-object-ado.md) objeto **abiertos** método.

 El equivalente de la **RDS. DataControl** objeto [SQL](../../../ado/reference/rds-api/sql-property.md) propiedad no está disponible. El [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto **abiertos** método *origen* argumento se utiliza en su lugar.

 **Tenga en cuenta** especificar "...;" Proveedor remoto = MS Remote;... "crearía un escenario de cuatro niveles. Escenarios de más de tres niveles no se ha probado y no deberían ser necesario.

## <a name="example"></a>Ejemplo
 Este ejemplo realiza una consulta en el **autores** tabla de la **Pubs** base de datos en un servidor denominado *YourServer*. Los nombres del origen de datos remoto y el servidor remoto se proporcionan en el [abiertos](../../../ado/reference/ado-api/open-method-ado-connection.md) método de la[conexión](../../../ado/reference/ado-api/connection-object-ado.md) objeto y la consulta SQL se especifica en el[abrir](../../../ado/reference/ado-api/open-method-ado-recordset.md) método de la [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto. A **Recordset** objeto se devuelve, editar y utiliza para actualizar el origen de datos.

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
 [Información general sobre el proveedor de servicios remotos OLE DB](http://msdn.microsoft.com/en-us/4083b72f-68c4-4252-b366-abb70db5ca2b)
