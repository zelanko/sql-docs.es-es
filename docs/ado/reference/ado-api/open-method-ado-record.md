---
title: Open (método) (record de ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Record::raw_Open
- _Record::Open
helpviewer_keywords:
- Open method [ADO]
ms.assetid: ab79a623-88a9-40b6-a017-a658bf19b778
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 97c7f1c143c83dd35ca5ff17e9776d79fb734ff9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67917924"
---
# <a name="open-method-ado-record"></a>Open (método) (registro de ADO)
Abre un objeto [Record](../../../ado/reference/ado-api/record-object-ado.md) existente o crea un nuevo elemento representado por el **registro**, como un archivo o un directorio.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Open Source, ActiveConnection, Mode, CreateOptions, Options, UserName, Password  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Origen*  
 Opcional. Una **variante** que puede representar la dirección URL de la entidad que va a representar este objeto de **registro** , un **comando**, un [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) abierto u otro objeto de **registro** , una cadena que contiene una instrucción SELECT de SQL o un nombre de tabla.  
  
 *ActiveConnection*  
 Opcional. **Variante** que representa la cadena de conexión o el objeto de [conexión](../../../ado/reference/ado-api/connection-object-ado.md) abierto.  
  
 *Modo*  
 Opcional. Valor [ConnectModeEnum](../../../ado/reference/ado-api/connectmodeenum.md) que especifica el modo de acceso para el objeto de **registro** resultante. El valor predeterminado es **adModeUnknown**.  
  
 *CreateOptions*  
 Opcional. Un valor [RecordCreateOptionsEnum](../../../ado/reference/ado-api/recordcreateoptionsenum.md) que especifica si se debe abrir un archivo o directorio existente o se debe crear un nuevo archivo o directorio. El valor predeterminado es **adFailIfNotExists**. Si se establece en el valor predeterminado, el modo de acceso se obtiene de la propiedad [mode](../../../ado/reference/ado-api/mode-property-ado.md) . Este parámetro se omite cuando el parámetro de *origen* no contiene una dirección URL.  
  
 *Opciones*  
 Opcional. Valor de [RecordOpenOptionsEnum](../../../ado/reference/ado-api/recordopenoptionsenum.md) que especifica las opciones para abrir el **registro**. El valor predeterminado es **adOpenRecordUnspecified**. Estos valores se pueden combinar.  
  
 *Nombre*  
 Opcional. Valor de **cadena** que contiene el ID. de usuario que, si es necesario, autoriza el acceso al *origen*.  
  
 *Contraseña*  
 Opcional. Valor de **cadena** que contiene la contraseña que, si es necesaria, comprueba el *nombre de usuario*.  
  
## <a name="remarks"></a>Observaciones  
 El *origen* puede ser:  
  
-   Una dirección URL. Si el protocolo de la dirección URL es http, se invocará el proveedor de Internet de forma predeterminada. Si la dirección URL apunta a un nodo que contiene un script ejecutable (como. Página ASP), se abre de forma predeterminada un **registro** que contiene el origen en lugar del contenido ejecutado. Use el argumento *Options* para modificar este comportamiento.  
  
-   Objeto de **registro** . Un objeto de **registro** abierto desde otro **registro** clonará el objeto de **registro** original.  
  
-   Objeto de **comando** . El objeto de **registro** abierto representa la fila única devuelta al ejecutar el **comando**. Si los resultados contienen más de una fila, el contenido de la primera fila se coloca en el registro y se puede Agregar un error a la colección de **errores** .  
  
-   Instrucción SELECT de SQL. El objeto de **registro** abierto representa la fila única devuelta al ejecutar el contenido de la cadena. Si los resultados contienen más de una fila, el contenido de la primera fila se coloca en el registro y se puede Agregar un error a la colección de **errores** .  
  
-   Un nombre de tabla.  
  
 Si el objeto **Record** representa una entidad a la que no se puede tener acceso con una dirección URL (por ejemplo, una fila de un **conjunto de registros** derivado de una base de datos), los valores de la propiedad [ParentURL](../../../ado/reference/ado-api/parenturl-property-ado.md) y el campo al que se obtiene acceso con la constante **adRecordURL** son NULL.  
  
> [!NOTE]
>  Las direcciones URL que usan el esquema http invocarán automáticamente el [proveedor de Microsoft OLE DB para la publicación en Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obtener más información, consulte [direcciones URL absolutas y relativas](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
  
## <a name="see-also"></a>Consulte también  
 [Open (método) (conexión de ADO)](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Open (método) (conjunto de registros ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Open (método, secuencia de ADO)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [Método OpenSchema](../../../ado/reference/ado-api/openschema-method.md)
