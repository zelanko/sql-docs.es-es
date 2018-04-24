---
title: Registros y secuencias | Documentos de Microsoft
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
- streams [ADO]
- streams [ADO], about streams
- records [ADO]
ms.assetid: 4d68868e-2611-4b5c-9a89-7caa5f753151
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9a107f9322758453222982b7f8ad9c1c4a5a15c7
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2018
---
# <a name="records-and-streams"></a>Registros y secuencias
ADO proporciona actualmente el [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto como medio principal para acceder a información en orígenes de datos, como bases de datos relacionales. Sin embargo, algunos proveedores admiten la [registro](../../../ado/reference/ado-api/record-object-ado.md) y [flujo](../../../ado/reference/ado-api/stream-object-ado.md) objetos como objetos alternativos o complementarios con el que se pueden manipular los datos de proveedores. Para obtener información específica sobre **registro** comportamiento, consulte la documentación del proveedor.  
  
## <a name="records"></a>Registros  
 **Registro** objetos funcionan básicamente como una fila **Recordset**s. Sin embargo, **registros** tienen una funcionalidad en comparación con limitada **conjuntos de registros** y tienen propiedades y métodos diferentes. El origen de datos en un **registro** objeto puede ser un comando que devuelve una fila de datos desde el proveedor. Usando **registro** objetos en lugar de **Recordset** objetos que se va a recibir los resultados de una consulta que devuelve una fila de datos elimina la sobrecarga de una instancia más complejo **conjunto de registros**  objeto.  
  
 **Registro** objetos pueden servir para otro propósito, especialmente con proveedores para orígenes de datos distintos de las bases de datos relacionales tradicionales, como el [proveedor Microsoft OLE DB para Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Gran parte de la información que se debe procesar existe, como tablas en bases de datos, sino como mensajes en sistemas de correo electrónico y archivos en sistemas de archivos modernos. El **registro** y **flujo** objetos facilitan el acceso a información almacenada en orígenes que no sean bases de datos relacionales.  
  
 El **registro** objeto puede representar y administrar datos tales como directorios y archivos en un sistema de archivos o carpetas y mensajes en un sistema de correo electrónico. Para ello, el origen de la **registro** puede ser la fila actual de un formato de archivo **Recordset**, una dirección URL absoluta o una dirección URL relativa junto con un formato de archivo [conexión](../../../ado/reference/ado-api/connection-object-ado.md) objeto.  
  
 Normalmente, un **Recordset** puede usarse para representar un contenedor o el elemento primario en una jerarquía como una carpeta o un directorio. A **registro** puede utilizarse para devolver información específica sobre un nodo en el contenedor primario, como un archivo o documento. La razón principal **registros** se utilizan para representar este tipo de información es que estos orígenes de datos heterogéneos. Esto significa que cada **registro** puede tener un conjunto diferente y el número de campos. Tradicional **conjuntos de registros** que contienen filas de una base de datos son homogéneos, lo cual significa que cada fila tiene el mismo número y tipo de campos.  
  
 Para obtener más información sobre el uso de la **registro** de objetos para procesar datos heterogéneos de proveedores como el proveedor de publicación en Internet, consulte [utilizar ADO para publicación en Internet](../../../ado/guide/data/using-ado-for-internet-publishing.md).  
  
## <a name="streams"></a>Flujos  
 El **flujo** objeto proporciona los medios para leer, escribir y administrar una secuencia de bytes. Esta secuencia de bytes puede ser texto o binario y tamaño está limitada por los recursos del sistema. Por lo general, ADO **flujo** objetos se utilizan para los siguientes fines:  
  
-   Para contener los datos de un **Recordset** guardado en formato XML. Guardan estas secuencias XML desde **Recordset**s puede usarse como origen al abrir un nuevo **conjunto de registros**. Para obtener más información, consulte [secuencias y persistencia](../../../ado/guide/data/streams-and-persistence.md).  
  
-   Para que contenga [CommandStreams](../../../ado/reference/ado-api/commandstream-property-ado.md) va a ejecutar en el proveedor como una alternativa a [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md). Por ejemplo, los diagramas de actualización de XML puede utilizarse como origen para un comando en el proveedor Microsoft OLE DB para SQL Server.  
  
-   Para recibir resultados desde el proveedor en un formato distinto de un **Recordset**, tales como los resultados XML desde el proveedor Microsoft OLE DB para SQL Server. Para obtener más información, consulte [recuperar conjuntos de resultados en secuencias](../../../ado/guide/data/retrieving-resultsets-into-streams.md).  
  
-   Para contener el texto o los bytes que componen un archivo o un mensaje, que se utiliza normalmente con los proveedores como el proveedor Microsoft OLE DB para la publicación en Internet. Para obtener más información acerca de este uso de **flujo** los objetos, vea [utilizar ADO para publicación en Internet](../../../ado/guide/data/using-ado-for-internet-publishing.md).  
  
 A **flujo** se puede abrir el objeto en:  
  
-   Un archivo simple especificado con una dirección URL.  
  
-   Un campo de un **registro** o **Recordset** que contiene un **flujo** objeto.  
  
-   La secuencia predeterminada de un **registro** o **Recordset** objeto que representa un directorio o un archivo compuesto.  
  
-   Un campo de recursos que contiene la dirección URL de un archivo simple.  
  
-   Ningún origen determinado en absoluto. En este caso, un **flujo** objeto está abierto en la memoria. Datos pueden escritos en él y, a continuación, se guarda en otra **flujo** o archivo.  
  
-   Un campo BLOB de un **conjunto de registros**.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Secuencias y persistencia](../../../ado/guide/data/streams-and-persistence.md)  
  
-   [Secuencias de comandos](../../../ado/guide/data/command-streams.md)  
  
-   [Recuperar conjuntos de resultados en secuencias](../../../ado/guide/data/retrieving-resultsets-into-streams.md)  
  
-   [Utilizar ADO para publicación en Internet](../../../ado/guide/data/using-ado-for-internet-publishing.md)
