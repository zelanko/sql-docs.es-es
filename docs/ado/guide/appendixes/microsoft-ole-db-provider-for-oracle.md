---
title: Proveedor OLE DB de Microsoft para Oracle | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- providers [ADO], OLE DB provider for Oracle
- OLE DB provider for Oracle [ADO]
- Oracle provider [ADO]
ms.assetid: 44fae9dd-5585-4cd6-8bbd-3248a78931b4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 60510302525562d9c3007a6ef57213fc261b4c60
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67926624"
---
# <a name="microsoft-ole-db-provider-for-oracle-overview"></a>Información general de Proveedor OLE DB de Microsoft para Oracle
> [!IMPORTANT]
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, use el proveedor de OLE DB de Oracle.

 El Proveedor OLE DB de Microsoft para Oracle permite a ADO obtener acceso a las bases de datos de Oracle.

## <a name="connection-string-parameters"></a>Parámetros de la cadena de conexión
 Para conectarse a este proveedor, establezca el argumento de *proveedor* de la propiedad [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) en:

```vb
MSDAORA
```

 La lectura de la propiedad [Provider](../../../ado/reference/ado-api/provider-property-ado.md) también devolverá esta cadena.

 Si se ejecuta una consulta join con un cursor Keyset o Dynamic en una base de datos de Oracle, se produce un error. Oracle solo admite un cursor estático de solo lectura.

## <a name="typical-connection-string"></a>Cadena de conexión típica
 Una cadena de conexión típica para este proveedor es:

```vb
"Provider=MSDAORA;Data Source=serverName;User ID=MyUserID; Password=MyPassword;"
```

 La cadena consta de estas palabras clave:

|Palabra clave|Descripción|
|-------------|-----------------|
|**Proveedor**|Especifica el proveedor de OLE DB para Oracle.|
|**Data Source** (Origen de datos)|Especifica el nombre de un servidor.|
|**Id. de usuario**|Especifica el nombre de usuario.|
|**Contraseña**|Especifica la contraseña del usuario.|

> [!NOTE]
>  Si se va a conectar a un proveedor de origen de datos que admite la autenticación de Windows, debe especificar **Trusted_Connection = Yes** o **Integrated Security = SSPI** en lugar de la información de identificador de usuario y contraseña en la cadena de conexión.

## <a name="provider-specific-connection-parameters"></a>Parámetros de conexión específicos del proveedor
 El proveedor admite varios parámetros de conexión específicos del proveedor además de los definidos por ADO. Al igual que con las propiedades de conexión ADO, estas propiedades específicas del proveedor se pueden establecer a través de la colección [Properties](../../../ado/reference/ado-api/properties-collection-ado.md) de una [conexión](../../../ado/reference/ado-api/connection-object-ado.md) o como parte de **ConnectionString**.

 Estos parámetros se describen totalmente en la [Referencia del programador de OLE DB](https://msdn.microsoft.com/3c5e2dd5-35e5-4a93-ac3a-3818bb43bbf8). El [Índice de propiedades dinámicas de ADO](../../../ado/reference/ado-api/ado-dynamic-property-index.md) proporciona una referencia cruzada entre estos nombres de parámetro y las propiedades de OLE DB correspondientes.

|Parámetro|Descripción|
|---------------|-----------------|
|**Identificador de ventana**|Indica el identificador de ventana que se va a usar para solicitar información adicional.|
|**Identificador de configuración regional**|Indica un número único de 32 bits (por ejemplo, 1033) que especifica las preferencias relacionadas con el idioma del usuario. Estas preferencias indican cómo se da formato a las fechas y horas, los elementos se ordenan alfabéticamente, las cadenas se comparan, etc.|
|**Servicios OLE DB**|Indica una máscara de máscara que especifica OLE DB servicios que se van a habilitar o deshabilitar.|
|**Pregunta**|Indica si se debe preguntar al usuario mientras se establece una conexión.|
|**Propiedades extendidas**|Cadena que contiene información de conexión ampliada específica del proveedor. Utilice esta propiedad únicamente para la información de conexión específica del proveedor que no se puede describir a través del mecanismo de propiedad.|

## <a name="see-also"></a>Consulte también
 [Propiedad ConnectionString (ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md) [Provider (propiedad](../../../ado/reference/ado-api/provider-property-ado.md) , ADO) [RECORDSET (objeto) (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
