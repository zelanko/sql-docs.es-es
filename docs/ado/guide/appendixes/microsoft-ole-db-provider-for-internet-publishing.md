---
title: Proveedor Microsoft OLE DB para la publicación en Internet | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB provider for Internet publishing [ADO]
- providers [ADO], OLE DB provider for Internet publishing
- Internet Publishing provider [ADO]
ms.assetid: 66a208d9-b580-4655-a41e-1d36e5b5bfca
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 939cc21d8f89d93dca9249efcad82a85874a00c4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62509907"
---
# <a name="microsoft-ole-db-provider-for-internet-publishing-overview"></a>Proveedor Microsoft OLE DB para la publicación de información general en Internet
El proveedor Microsoft OLE DB para la publicación en Internet permite ADO para acceder a recursos atendidos por FrontPage de Microsoft o Microsoft Internet Information Server. Los recursos incluyen archivos de código fuente de web, como archivos HTML o las carpetas web de Windows 2000.

## <a name="connection-string-parameters"></a>Parámetros de cadena de conexión
 Para conectarse a este proveedor, establezca el *proveedor* argumento de la [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) propiedad:

```vb
MSDAIPP.DSO
```

 Este valor también se puede establecer o leer utilizando el [proveedor](../../../ado/reference/ado-api/provider-property-ado.md) propiedad.

## <a name="typical-connection-string"></a>Cadena de conexión típica
 Una cadena de conexión típica para este proveedor es:

```vb
"Provider=MSDAIPP.DSO;Data Source=ResourceURL;User ID=MyUserID;Password=MyPassword;"
```

 -o bien-

```vb
"URL=ResourceURL;User ID=MyUserID;Password=MyPassword;"
```

 La cadena consta de estas palabras clave:

|Palabra clave|Descripción|
|-------------|-----------------|
|**Proveedor**|Especifica el proveedor OLE DB para la publicación en Internet.|
|**Origen de datos** - o - **URL**|Especifica la dirección URL de un archivo o directorio publicado en una carpeta Web.|
|**Id. de usuario**|Especifica el nombre de usuario.|
|**Contraseña**|Especifica la contraseña del usuario.|

> [!NOTE]
>  Si se conecta a un proveedor de origen de datos que admite la autenticación de Windows, debe especificar **Trusted_Connection = yes** o **Integrated Security = SSPI** en lugar de Id. de usuario y contraseña información de la cadena de conexión.

 Si establece la *ResourceURL* valor desde la "URL =" en la cadena de conexión a un valor no válido, de forma predeterminada, el proveedor de publicación en Internet provoca que un cuadro de diálogo para solicitar un valor válido. Se trata de un comportamiento no deseado para un componente en el nivel intermedio de una aplicación, ya que se suspende la ejecución del programa hasta que el cuadro de diálogo está desactivado y el cliente parece inmovilizar porque no ha recibido una respuesta desde el componente.

> [!NOTE]
>  Si MSDAIPP. DSO se especifica explícitamente como valor del proveedor, ya sea con la *proveedor* palabra clave de cadena de conexión o la **proveedor** propiedad, no se puede usar "URL =" en la cadena de conexión. Si lo hace, se producirá un error. En su lugar, especifique la dirección URL como se muestra en el tema [utilizar ADO con el proveedor OLE DB para la publicación en Internet](../../../ado/guide/data/the-ole-db-provider-for-internet-publishing.md).

## <a name="see-also"></a>Vea también
 [Escenario de publicación en Internet](../../../ado/guide/data/internet-publishing-scenario.md) [el proveedor OLE DB para la publicación en Internet](../../../ado/guide/data/the-ole-db-provider-for-internet-publishing.md)
