---
title: Registros y secuencias | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- streams [ADO]
- streams [ADO], about streams
- records [ADO]
ms.assetid: 4d68868e-2611-4b5c-9a89-7caa5f753151
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 19fc6e61a10e1a92f0f674a23d00f1e1b06a596c
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66701700"
---
# <a name="records-and-streams"></a>Registros y secuencias
ADO proporciona actualmente las [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto como medio principal para acceder a la información de orígenes de datos, como bases de datos relacionales. Sin embargo, algunos proveedores admiten la [registro](../../../ado/reference/ado-api/record-object-ado.md) y [Stream](../../../ado/reference/ado-api/stream-object-ado.md) objetos como objetos alternativos o complementarios para manipular los datos de proveedores. Para obtener información específica sobre **registro** comportamiento, consulte la documentación del proveedor.  
  
## <a name="records"></a>Registros  
 **Registro** objetos funcionan básicamente como una fila **Recordset**s. Sin embargo, **registros** limitada en comparación con la funcionalidad **conjuntos de registros** y tienen diferentes propiedades y métodos. El origen de datos en un **registro** objeto puede ser un comando que devuelve una fila de datos del proveedor. Mediante **registro** objetos en lugar de **Recordset** objetos para recibir los resultados de una consulta que devuelve una fila de datos elimina la sobrecarga de crear instancias más complejas **conjunto de registros**  objeto.  
  
 **Registro** objetos pueden servir para otro propósito, especialmente con proveedores de orígenes de datos que no sean bases de datos relacionales tradicionales, como el [proveedor Microsoft OLE DB para la publicación en Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Gran parte de la información que se debe procesar existe, no como tablas en bases de datos, pero como mensajes en sistemas de correo electrónico y archivos en modernos sistemas de archivos. El **registro** y **Stream** objetos facilitan el acceso a información almacenada en los orígenes que no sean bases de datos relacionales.  
  
 El **registro** objeto puede representar y administrar datos, como archivos y directorios en un sistema de archivos o carpetas y mensajes en un sistema de correo electrónico. Para estos fines, el origen de la **registro** puede ser la fila actual de una abierta **Recordset**, una dirección URL absoluta o una dirección URL relativa junto con una apertura [conexión](../../../ado/reference/ado-api/connection-object-ado.md) objeto.  
  
 Normalmente, un **Recordset** puede usarse para representar un contenedor o la entidad primaria en una jerarquía como una carpeta o un directorio. Un **registro** puede usarse para devolver información específica sobre un nodo en el contenedor primario, como un archivo o documento. La razón principal **registros** se utilizan para representar este tipo de información es que estos orígenes de datos heterogéneos. Esto significa que cada **registro** puede tener un conjunto diferente y el número de campos. Tradicional **conjuntos de registros** que contienen filas de una base de datos son homogéneas, lo que significa que cada fila tiene el mismo número y tipo de campos.  
  
 Para obtener más información sobre el uso de la **registro** de objetos para el procesamiento de datos heterogéneos de proveedores como el proveedor de publicación en Internet, consulte [utilizar ADO para publicación en Internet](../../../ado/guide/data/using-ado-for-internet-publishing.md).  
  
## <a name="streams"></a>Flujos  
 El **Stream** objeto proporciona los medios para leer, escribir y administrar una secuencia de bytes. Esta secuencia de bytes puede ser texto o binario y tiene un tamaño limitada únicamente por los recursos del sistema. Normalmente, ADO **Stream** objetos se usan para los siguientes fines:  
  
-   Para que contenga los datos de un **Recordset** guarda en formato XML. Guardan estas secuencias XML desde **Recordset**s puede usarse como origen al abrir un nuevo **Recordset**. Para obtener más información, consulte [secuencias y persistencia](../../../ado/guide/data/streams-and-persistence.md).  
  
-   Para que contenga [CommandStreams](../../../ado/reference/ado-api/commandstream-property-ado.md) que se ejecutan en el proveedor como una alternativa a [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md). Por ejemplo, diagramas de actualización XML puede usarse como origen para un comando con el proveedor Microsoft OLE DB para SQL Server.  
  
-   Para recibir los resultados del proveedor en un formato distinto de un **Recordset**, tales como los resultados XML desde el proveedor Microsoft OLE DB para SQL Server. Para obtener más información, consulte [recuperar conjuntos de resultados en secuencias](../../../ado/guide/data/retrieving-resultsets-into-streams.md).  
  
-   Para contener el texto o bytes que componen un archivo o mensaje que normalmente se utiliza con los proveedores como el proveedor Microsoft OLE DB para la publicación en Internet. Para obtener más información acerca de este uso de **Stream** objetos, vea [utilizar ADO para publicación en Internet](../../../ado/guide/data/using-ado-for-internet-publishing.md).  
  
 Un **Stream** se puede abrir el objeto en:  
  
-   Un archivo simple especificado con una dirección URL.  
  
-   Un campo de un **registro** o **Recordset** que contiene un **Stream** objeto.  
  
-   La secuencia predeterminada de un **registro** o **Recordset** objeto que representa un directorio o un archivo compuesto.  
  
-   Un campo de recursos que contiene la dirección URL de un archivo simple.  
  
-   Ningún origen particular en absoluto. En este caso, un **Stream** se abre el objeto en memoria. Datos se pueden escritos en él y, a continuación, se guarda en otra **Stream** o archivo.  
  
-   Un campo BLOB en un **Recordset**.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Secuencias y persistencia](../../../ado/guide/data/streams-and-persistence.md)  
  
-   [Secuencias de comandos](../../../ado/guide/data/command-streams.md)  
  
-   [Recuperar conjuntos de resultados en secuencias](../../../ado/guide/data/retrieving-resultsets-into-streams.md)  
  
-   [Utilizar ADO para publicación en Internet](../../../ado/guide/data/using-ado-for-internet-publishing.md)
