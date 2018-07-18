---
title: Proveedor Microsoft OLE DB para Oracle | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- providers [ADO], OLE DB provider for Oracle
- OLE DB provider for Oracle [ADO]
- Oracle provider [ADO]
ms.assetid: 44fae9dd-5585-4cd6-8bbd-3248a78931b4
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 66e2994479c222c5f050ce13e19eb3a9ed5c01e8
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/12/2018
ms.locfileid: "38979217"
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

 Leer el [proveedor](../../../ado/reference/ado-api/provider-property-ado.md) propiedad devolverá también esta cadena.

 Si se ejecuta una consulta de combinación con un cursor keyset o dynamic en una base de datos de Oracle, se produce un error. Oracle sólo admite un cursor estático de solo lectura.

## <a name="typical-connection-string"></a>Cadena de conexión típica
 Una cadena de conexión típica para este proveedor es:

```
"Provider=MSDAORA;Data Source=serverName;User ID=MyUserID; Password=MyPassword;"
```

 La cadena consta de estas palabras clave:

|Palabra clave|Descripción|
|-------------|-----------------|
|**Proveedor**|Especifica el proveedor OLE DB para Oracle.|
|**Origen de datos**|Especifica el nombre de un servidor.|
|**Id. de usuario**|Especifica el nombre de usuario.|
|**Contraseña**|Especifica la contraseña del usuario.|

> [!NOTE]
>  Si se conecta a un proveedor de origen de datos que admite la autenticación de Windows, debe especificar **Trusted_Connection = yes** o **Integrated Security = SSPI** en lugar de Id. de usuario y contraseña información de la cadena de conexión.

## <a name="provider-specific-connection-parameters"></a>Parámetros de conexión específica del proveedor
 El proveedor admite varios parámetros de conexión específica del proveedor además de los definidos por ADO. Como con las propiedades de conexión ADO, se pueden establecer estas propiedades específicas del proveedor a través de la [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) colección de un [conexión](../../../ado/reference/ado-api/connection-object-ado.md) o como parte de la **ConnectionString**.

 Estos parámetros se describe detalladamente en la [referencia del programador de OLE DB](http://msdn.microsoft.com/3c5e2dd5-35e5-4a93-ac3a-3818bb43bbf8). El [índice de propiedades dinámicas de ADO](../../../ado/reference/ado-api/ado-dynamic-property-index.md) proporciona una referencia cruzada entre estos nombres de parámetro y las propiedades de OLE DB correspondientes.

|Parámetro|Descripción|
|---------------|-----------------|
|**Identificador de ventana**|Indica el identificador de ventana se utiliza para solicitar información adicional.|
|**Identificador de configuración regional**|Indica un número único de 32 bits (por ejemplo, 1033) que especifica las preferencias relacionadas con el idioma del usuario. Estas preferencias indican cómo se da formato a fechas y horas, los elementos se ordenan alfabéticamente, se comparan cadenas y así sucesivamente.|
|**Servicios OLE DB**|Indica una máscara de bits que especifica los servicios de OLE DB para habilitar o deshabilitar.|
|**Símbolo del sistema**|Indica si se debe preguntar al usuario mientras se está estableciendo una conexión.|
|**Propiedades extendidas**|Una cadena que contiene información de conexión ampliada específica del proveedor. Utilice esta propiedad solo para obtener información de conexión específica del proveedor que no se puede describir mediante un mecanismo de propiedad.|

## <a name="see-also"></a>Vea también
 [Propiedad ConnectionString (ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md) [proveedor (propiedad, ADO)](../../../ado/reference/ado-api/provider-property-ado.md) [el objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
