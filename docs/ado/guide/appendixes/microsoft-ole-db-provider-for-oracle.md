---
title: Proveedor Microsoft OLE DB para Oracle | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- providers [ADO], OLE DB provider for Oracle
- OLE DB provider for Oracle [ADO]
- Oracle provider [ADO]
ms.assetid: 44fae9dd-5585-4cd6-8bbd-3248a78931b4
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d92236375a3ac152dbe7f5a2f259ce2a5f2edb79
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="microsoft-ole-db-provider-for-oracle-overview"></a>Proveedor Microsoft OLE DB para Oracle Introducción
> [!IMPORTANT]
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, use el proveedor de OLE DB de Oracle.

 El proveedor Microsoft OLE DB para Oracle permite que ADO tener acceso a las bases de datos de Oracle.

## <a name="connection-string-parameters"></a>Parámetros de cadena de conexión
 Para conectarse a este proveedor, establezca el *proveedor* argumento de la [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) propiedad:

```
MSDAORA
```

 Leer la [proveedor](../../../ado/reference/ado-api/provider-property-ado.md) propiedad devolverá también esta cadena.

 Si se ejecuta una consulta de combinación con un cursor keyset o dynamic en una base de datos de Oracle, se produce un error. Oracle sólo admite un cursor estático de solo lectura.

## <a name="typical-connection-string"></a>Cadena de conexión típica
 Una cadena de conexión típica para este proveedor es:

```
"Provider=MSDAORA;Data Source=serverName;User ID=MyUserID; Password=MyPassword;"
```

 La cadena consta de estas palabras clave:

|Palabra clave|Description|
|-------------|-----------------|
|**Proveedor**|Especifica el proveedor OLE DB para Oracle.|
|**Origen de datos**|Especifica el nombre de un servidor.|
|**Id. de usuario**|Especifica el nombre de usuario.|
|**Contraseña**|Especifica la contraseña del usuario.|

> [!NOTE]
>  Si se conecta a un proveedor de origen de datos que admita la autenticación de Windows, debe especificar **Trusted_Connection = yes** o **Integrated Security = SSPI** en lugar de Id. de usuario y contraseña información de la cadena de conexión.

## <a name="provider-specific-connection-parameters"></a>Parámetros de conexión específica del proveedor
 El proveedor admite varios parámetros de conexión específica del proveedor además de los definidos por ADO. Como con las propiedades de conexión ADO, estas propiedades específicas del proveedor se pueden establecer a través de la [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) colección de un [conexión](../../../ado/reference/ado-api/connection-object-ado.md) o como parte de la **ConnectionString**.

 Estos parámetros se describen detalladamente en la [referencia del programador de OLE DB](http://msdn.microsoft.com/en-us/3c5e2dd5-35e5-4a93-ac3a-3818bb43bbf8). El [índice de propiedades dinámicas de ADO](../../../ado/reference/ado-api/ado-dynamic-property-index.md) proporciona una referencia cruzada entre estos nombres de parámetro y las propiedades de OLE DB correspondientes.

|Parámetro|Description|
|---------------|-----------------|
|**Identificador de ventana**|Indica el identificador de ventana que se usará para solicitar información adicional.|
|**Identificador de configuración regional**|Indica un único número de 32 bits (por ejemplo, 1033) que especifica las preferencias relacionadas con el idioma del usuario. Estas preferencias indican cómo se da formato a fechas y horas, los elementos se ordenan alfabéticamente, se comparan las cadenas y así sucesivamente.|
|**Servicios OLE DB**|Indica una máscara de bits que especifica los servicios OLE DB para habilitar o deshabilitar.|
|**Símbolo del sistema**|Indica si se debe preguntar al usuario mientras se está estableciendo una conexión.|
|**Propiedades extendidas**|Una cadena que contiene información de conexión ampliada específica del proveedor. Utilice esta propiedad solo para obtener información de conexión específica del proveedor que no se puede describir mediante un mecanismo de propiedad.|

## <a name="see-also"></a>Vea también
 [Propiedad ConnectionString (ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md) [(ADO) de la propiedad de proveedor](../../../ado/reference/ado-api/provider-property-ado.md) [objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)

