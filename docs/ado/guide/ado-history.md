---
title: Historial de ADO | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2019
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ADO, what's new
ms.assetid: 667673f2-3151-432b-894a-3fc60b704ea4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7e3e491ccb659d8739cb93d72e0c923fce480015
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62695430"
---
# <a name="ado-features-for-each-release"></a>Características de ADO para cada versión

En este tema se enumera las nuevas características introducidas con cada versión de ADO MD ADO y ADOX.

## <a name="ado-60"></a>ADO 6.0

 ADO 6.0 se incluye en Windows Vista, como parte de Windows Data Access Components (Windows DAC) 6.0. ADO 6.0 es funcionalmente equivalente a ADO 2.8.

## <a name="ado-28"></a>ADO 2.8

 ADO 2.8 se incluyó en Windows XP y Windows Server 2003, como parte de Microsoft Data Access Components (MDAC) 2.8. Una versión redistribuible de MDAC 2.8 también está disponible; Tenga en cuenta que esta versión redistribuible solo debe instalarse en Windows 2000. ADO 2.8 aborda varios aspectos relacionados con la seguridad:

 *No se permite el acceso de unidad de disco duro fuera de una zona de confianza.*
En dominios que implican los sitios de confianza de secuencias de comandos, se deshabilitan las siguientes operaciones: **Stream.SaveToFile**, **Stream.LoadFromFile**, **Recordset.Save**, y **Recordset.Open**, que se usa junto con el **adCmdFile**  marca o con el proveedor Microsoft OLE DB persistencia (MSPersist).

 **Recordset.Open** _,_ **Recordset.Save** _,_ **Stream.SaveToFile** _, y_ **Stream.LoadFromFile** _operará solo los archivos físicos._
Estos métodos ahora para comprobar que los identificadores de archivos punto a solo los archivos físicos.

 **Recordset.ActiveCommand** _devuelve un error cuando se invoca desde una página ASP/HTML._ 
Esto evita la **comando** objeto desde el que se utiliza incorrectamente.

 _El número de_**conjuntos de registros**_devuelto por una anidada_**forma**_comando tiene un límite superior._
Un comando shape anidado ahora devuelve un máximo de 512 **conjuntos de registros**. Esto significa que un **forma** comando ya no se puede anidar a cualquier profundidad. En su lugar, la profundidad máxima de nivel es 512, si cada comando genera un único (elemento secundario) **Recordset**. If, en cualquier nivel, una **forma** comando devuelve varios **conjuntos de registros**, el nivel máximo de profundidad será inferior a 512.

## <a name="ado-27"></a>ADO 2.7

 *compatibilidad con plataformas de 64 bits* ADO 2.7 introduce compatibilidad con procesadores de 64 bits.

## <a name="ado-26"></a>ADO 2.6

 **CubDef.GetSchemaObject**_método_ desde ADO 2.6, los objetos ADO MD se pueden recuperar mediante nombres únicos, según lo especificado por el [UniqueName (propiedad, ADO MD)](../../ado/reference/ado-md-api/uniquename-property-ado-md.md). Los nombres de los objetos primarios no se necesiten conocer y colecciones de elementos primarios no es necesario que se debe rellenar para recuperar un objeto de esquema. Consulte [método GetSchemaObject (ADO MD)](../../ado/reference/ado-md-api/getschemaobject-method-ado-md.md).

 *Secuencias de comandos* el **comando** objeto es compatible con los comandos en formato de secuencia como una alternativa al uso de la **CommandText** propiedad. El [propiedad CommandStream (ADO)](../../ado/reference/ado-api/commandstream-property-ado.md) puede utilizarse para especificar plantillas XML o diagramas de actualización como el **comando** la entrada con el proveedor Microsoft OLE DB para SQL Server.

 **Dialecto**_propiedad_ [dialecto](../../ado/reference/ado-api/dialect-property.md) es una nueva propiedad que define la sintaxis y reglas generales que el proveedor se usa para analizar la cadena o secuencia.

 **Command.Execute**_método_ el [Ejecutar método](../../ado/reference/ado-api/execute-method-ado-command.md) de ADO **comando** objeto se ha mejorado para usar flujos de entrada y salida.

 *Campo statusvalues* si el usuario encuentra un error DB_E_ERRORSOCCURRED cuando se modifica un **campo** de un **Recordset**, ADO ahora rellenará el **Field.Status**propiedad con la información de estado adecuado para que el usuario tendrá que obtener más información sobre qué salió mal. Consulte [propiedad Status (Field ADO)](../../ado/reference/ado-api/status-property-ado-field.md).

 **NamedParameters**_propiedad_ [NamedParameters](../../ado/reference/ado-api/namedparameters-property-ado.md) es una nueva propiedad de la **comando** denominado objeto que indica que debe utilizar el proveedor parámetros.

 *Los conjuntos de resultados en secuencias* ADO puede devolver conjuntos de resultados de un origen de datos en un **Stream**, en lugar de un **Recordset** objeto. Con la versión más reciente del proveedor de Microsoft OLE DB para SQL Server, puede obtener los resultados XML del proveedor mediante la ejecución de una consulta de "XML". Un **Stream** que recibe el conjunto de resultados se pueden abrir con un comando "XML" como el origen. Consulte [recuperar conjuntos de resultados en secuencias](../../ado/guide/data/retrieving-resultsets-into-streams.md).

 *Conjunto de resultados de fila única* The ADO **registro** ahora se puede abrir el objeto en una cadena de comandos o **comando** objeto que devuelve una fila de datos del proveedor. Esto da como resultado un mejor rendimiento con proveedores de MDAC 2.6. Consulte [método Open (Record ADO)](../../ado/reference/ado-api/open-method-ado-record.md).

## <a name="ado-25"></a>ADO 2.5

 **Registro** _objeto_ ADO 2.5 presenta el **registro** objetos para representar y administrar una fila de un **Recordset** o un proveedor de datos o un objeto que encapsula un datos semiestructurados, como un archivo o directorio.

 **Stream** _objeto_ ADO 2.5 también introduce el **Stream** objetos para representar un flujo de datos binarios o texto.

 *Enlace de la dirección URL* ADO 2.5 presenta el uso de una dirección URL, como una alternativa a un texto de comando y la cadena de conexión, como nombres de objetos de almacén de datos. Se puede usar una dirección URL con el existente **conexión** y **Recordset** objetos, así como con el nuevo **registro** y **Stream** objetos.

 *Proveedores de datos que admiten el enlace de la dirección URL* ADO 2.5 es compatible con proveedores de OLE DB que reconocen los esquemas de URL. Esto incluye el proveedor OLE DB para la publicación en Internet, que tiene acceso al sistema de archivos de Windows 2000 y reconoce el esquema HTTP existente.
