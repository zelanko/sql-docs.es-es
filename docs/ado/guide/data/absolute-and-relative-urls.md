---
title: Las direcciones URL absolutas y relativas | Documentos de Microsoft
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- relative URLs [ADO]
- absolute URLs [ADO]
- URLs [ADO]
ms.assetid: 6a34a7ef-50cc-4c3d-82f7-106b9a8f3caf
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c87fea24a0f03bbf179c74102fbb5514873f134a
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="absolute-and-relative-urls"></a>Direcciones URL absolutas y relativas
Una dirección URL especifica la ubicación de un destino almacenado en un equipo local o en red. El destino puede ser un archivo, directorio, página HTML, imagen, programa y así sucesivamente*.*  
  
 Un *dirección URL absoluta* contiene toda la información necesaria para localizar un recurso.  
  
 A *dirección URL relativa* localiza un recurso mediante una dirección URL absoluta como punto de partida. De hecho, la "dirección URL completa" del destino se especifica mediante la concatenación de las direcciones URL absolutas y relativas.  
  
 Un *dirección URL absoluta* utiliza el formato siguiente: *scheme://server/path/resource*  
  
 Una dirección URL relativa normalmente consta solo de la *ruta de acceso*y, opcionalmente, el *recursos*, pero no *esquema* o *server*. Las tablas siguientes definen las partes individuales del formato de dirección URL completa.  
  
 *esquema*  
 Especifica cómo el *recursos* se tiene acceso.  
  
 *servidor*  
 Especifica el nombre del equipo donde el *recursos* se encuentra.  
  
 *ruta de acceso*  
 Especifica la secuencia de directorios que conducen al destino. Si *recursos* es se omite, el destino es el último directorio en *ruta de acceso*.  
  
 *recursos*  
 Si se incluye, *recursos* es el destino, y normalmente es el nombre de un archivo. Puede ser un *archivo simple,* que contiene una secuencia binaria única de bytes, o un *documentos estructurados,* que contiene uno o varios almacenamientos y secuencias binarias de bytes.  
  
## <a name="url-scheme-registration"></a>Registro del esquema de direcciones URL  
 Si un proveedor admite las direcciones URL, el proveedor registrará uno o varios esquemas de dirección URL. Registro significa que las direcciones URL mediante el esquema invocará automáticamente el proveedor registrado. Por ejemplo, el *http* esquema está registrado en el [proveedor Microsoft OLE DB para Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). ADO se da por supuesto que todas las direcciones URL precedidas con "http" representan carpetas Web o archivos que se usará con el proveedor de publicación en Internet. Para obtener información sobre los esquemas registrados por el proveedor, consulte la documentación del proveedor.  
  
## <a name="defining-context-with-a-url"></a>Definir contexto con una dirección URL  
 Una función de una conexión abierta, representada por un [conexión](../../../ado/reference/ado-api/connection-object-ado.md) objeto restringir las operaciones subsiguientes en el origen de datos representado por esa conexión. Es decir, la conexión define el contexto para las operaciones posteriores.  
  
 Con ADO 2.7 o posterior, una dirección URL absoluta también puede definir un contexto. Por ejemplo, cuando un [registro](../../../ado/reference/ado-api/record-object-ado.md) objeto se abre con una dirección URL absoluta, un **conexión** objeto se crea implícitamente para representar el recurso especificado por la dirección URL.  
  
 Se puede especificar una dirección URL absoluta que define un contexto en el *ActiveConnection* parámetro de la **registro** objeto [abiertos](../../../ado/reference/ado-api/open-method-ado-record.md) método. También se puede especificar una dirección URL absoluta como el valor de la "dirección URL**=**" palabra clave en el **conexión** objeto [abiertos](../../../ado/reference/ado-api/open-method-ado-connection.md) método * ConnectionString* parámetro y el [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto [abiertos](../../../ado/reference/ado-api/open-method-ado-recordset.md) método *ActiveConnection* parámetro.  
  
 También puede definirse contexto abriendo un **registro** o **Recordset** objeto que representa un directorio porque estos objetos ya tienen un implícita o explícitamente declarado **conexión ** objeto que especifica el contexto.  
  
## <a name="scoped-operations"></a>Operaciones de ámbito  
 El contexto también define el ámbito, es decir, el directorio y sus subdirectorios que pueden participar en operaciones posteriores. El **registro** objeto tiene varios métodos con ámbito que operan en un directorio y todos sus subdirectorios. Estos métodos incluyen [CopyRecord](../../../ado/reference/ado-api/copyrecord-method-ado.md), [MoveRecord](../../../ado/reference/ado-api/moverecord-method-ado.md), y [DeleteRecord](../../../ado/reference/ado-api/deleterecord-method-ado.md).  
  
## <a name="relative-urls-as-command-text"></a>Direcciones URL relativas como texto de comando  
 Puede especificar un comando que se ejecuta en el origen de datos, escriba una cadena en el *CommandText* parámetro de la **conexión** del objeto [Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md) método y en el * Origen* parámetro de la **Recordset** del objeto [abiertos](../../../ado/reference/ado-api/open-method-ado-recordset.md) método.  
  
 Se puede especificar una dirección URL relativa en el *CommandText* o *origen* parámetro. La dirección URL relativa no representa realmente un comando, por ejemplo, un comando SQL; simplemente especifica los parámetros. El contexto de la conexión activa debe ser una dirección URL absoluta y el *opción* parámetro debe establecerse en **adCmdTableDirect**.  
  
 Por ejemplo, el ejemplo de código siguiente muestra cómo abrir un **Recordset** en el archivo Readme25.txt del directorio Winnt/system32:  
  
```  
recordset.Open "system32/Readme25.txt", "URL=http://YourServer/Winnt/",,,adCmdTableDirect  
```  
  
 La dirección URL absoluta en la cadena de conexión especifica el servidor (`YourServer`) y la ruta de acceso (`Winnt`). Esta dirección URL también define el contexto.  
  
 La dirección URL relativa en el texto de comando utiliza la dirección URL absoluta como punto de partida y especifica el resto de la ruta de acceso (`system32`) y abrir el archivo (`Readme25.txt`).  
  
 El campo de opciones (`adCmdTableDirect`) indica que el tipo de comando es una dirección URL relativa.  
  
 Como otro ejemplo, el código siguiente se abrirá una **Recordset** en el contenido de la `Winnt` directorio:  
  
```  
recordset.Open "", "URL=http://YourServer/Winnt/",,,adCmdTableDirect  
```  
  
## <a name="ole-db-provider-supplied-url-schemes"></a>Esquemas de direcciones URL proporcionados por el proveedor OLE DB  
 La parte inicial de una dirección URL completa es el *esquema* que se usa para tener acceso al recurso identificado por el resto de la dirección URL. Algunos ejemplos son HTTP (Protocolo de transferencia de hipertexto) y FTP (Protocolo de transferencia de archivos).  
  
 ADO admite proveedores OLE DB que reconocen sus propios esquemas de dirección URL. Por ejemplo, el [proveedor Microsoft OLE DB para Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)*,* que tiene acceso a archivos "publicados" de Windows 2000, reconoce el esquema HTTP existente.  
  
## <a name="see-also"></a>Vea también  
 [Objeto de conexión (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Objeto de registro (ADO)](../../../ado/reference/ado-api/record-object-ado.md)   
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)

