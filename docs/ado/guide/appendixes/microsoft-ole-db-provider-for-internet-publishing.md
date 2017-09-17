---
title: "Proveedor Microsoft OLE DB para la publicación en Internet | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: H1Hack27Feb2017
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- OLE DB provider for Internet publishing [ADO]
- providers [ADO], OLE DB provider for Internet publishing
- Internet Publishing provider [ADO]
ms.assetid: 66a208d9-b580-4655-a41e-1d36e5b5bfca
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d466123e7330eb599847225d2b108ec7f80d9ea9
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="microsoft-ole-db-provider-for-internet-publishing-overview"></a>Proveedor Microsoft OLE DB para la publicación de información general en Internet
El proveedor Microsoft OLE DB para publicación en Internet permite a ADO para tener acceso a recursos atendido por Microsoft FrontPage o Microsoft Internet Information Server. Los recursos incluyen archivos de código fuente de web, como archivos HTML o carpetas de web de Windows 2000.

## <a name="connection-string-parameters"></a>Parámetros de cadena de conexión
 Para conectarse a este proveedor, establezca el *proveedor* argumento de la [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) propiedad:

```
MSDAIPP.DSO
```

 Este valor también se puede establecer o leer utilizando el [proveedor](../../../ado/reference/ado-api/provider-property-ado.md) propiedad.

## <a name="typical-connection-string"></a>Cadena de conexión típica
 Una cadena de conexión típica para este proveedor es:

```
"Provider=MSDAIPP.DSO;Data Source=ResourceURL;User ID=MyUserID;Password=MyPassword;"
```

 -O bien-

```
"URL=ResourceURL;User ID=MyUserID;Password=MyPassword;"
```

 La cadena consta de estas palabras clave:

|Palabra clave|Description|
|-------------|-----------------|
|**Proveedor**|Especifica el proveedor OLE DB para la publicación en Internet.|
|**Origen de datos** - o - **dirección URL**|Especifica la dirección URL de un archivo o directorio publicado en una carpeta Web.|
|**Id. de usuario**|Especifica el nombre de usuario.|
|**Contraseña**|Especifica la contraseña del usuario.|

> [!NOTE]
>  Si se conecta a un proveedor de origen de datos que admita la autenticación de Windows, debe especificar **Trusted_Connection = yes** o **Integrated Security = SSPI** en lugar de Id. de usuario y contraseña información de la cadena de conexión.

 Si establece la *ResourceURL* valor de la "URL =" en la cadena de conexión en un valor no válido, de forma predeterminada, el proveedor de publicación en Internet provoca que un cuadro de diálogo para solicitar un valor válido. Se trata de un comportamiento no deseado para un componente en el nivel intermedio de una aplicación, ya que se suspende la ejecución del programa hasta que el cuadro de diálogo está desactivado y el cliente parece inmovilizar porque no recibió una respuesta desde el componente.

> [!NOTE]
>  Si MSDAIPP. DSO de forma explícita como valor del proveedor, ya sea con la *proveedor* palabra clave de cadena de conexión o la **proveedor** propiedad, no se puede utilizar "URL =" en la cadena de conexión. Si lo hace, se producirá un error. En su lugar, especifique la dirección URL como se muestra en el tema [usar ADO con el proveedor OLE DB para la publicación en Internet](../../../ado/guide/data/the-ole-db-provider-for-internet-publishing.md).

## <a name="see-also"></a>Vea también
 [Escenario de Internet Publishing](../../../ado/guide/data/internet-publishing-scenario.md) [el proveedor OLE DB para la publicación en Internet](../../../ado/guide/data/the-ole-db-provider-for-internet-publishing.md)

