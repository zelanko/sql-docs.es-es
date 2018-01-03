---
title: "Open (método) (registro de ADO) | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Record::raw_Open
- _Record::Open
helpviewer_keywords: Open method [ADO]
ms.assetid: ab79a623-88a9-40b6-a017-a658bf19b778
caps.latest.revision: "15"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 627000fbf4b3b153895d64ba0bd7560654d63719
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="open-method-ado-record"></a>Open (método) (registro de ADO)
Se abre una existente [registro](../../../ado/reference/ado-api/record-object-ado.md) objeto o crea un nuevo elemento representado por la **registro**, por ejemplo, un archivo o directorio.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Open Source, ActiveConnection, Mode, CreateOptions, Options, UserName, Password  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Source*  
 Opcional. A **Variant** que puede representar la dirección URL de la entidad para ser representado por este **registro** objeto, un **comando**, abierto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) o otro **registro** (objeto), una cadena que contiene una instrucción SELECT de SQL o un nombre de tabla.  
  
 *ActiveConnection*  
 Opcional. A **Variant** que representa la cadena de conexión o abra [conexión](../../../ado/reference/ado-api/connection-object-ado.md) objeto.  
  
 *Modo*  
 Opcional. A [ConnectModeEnum](../../../ado/reference/ado-api/connectmodeenum.md) valor que especifica el modo de acceso para los resultantes **registro** objeto. Valor predeterminado es **adModeUnknown**.  
  
 *CreateOptions*  
 Opcional. A [RecordCreateOptionsEnum](../../../ado/reference/ado-api/recordcreateoptionsenum.md) valor que especifica si se debe abrir un archivo existente o un directorio o se debe crear un nuevo archivo o directorio. Valor predeterminado es **adFailIfNotExists**. Si se establece en el valor predeterminado, el modo de acceso se obtiene de la [modo](../../../ado/reference/ado-api/mode-property-ado.md) propiedad. Este parámetro se ignora cuando la *origen* parámetro no contiene una dirección URL.  
  
 *Opciones*  
 Opcional. A [RecordOpenOptionsEnum](../../../ado/reference/ado-api/recordopenoptionsenum.md) valor que especifica opciones para abrir la **registro**. Valor predeterminado es **adOpenRecordUnspecified**. Estos valores se pueden combinar.  
  
 *UserName*  
 Opcional. A **cadena** valor que contiene el identificador de usuario que, si es necesario, autoriza el acceso a *origen*.  
  
 *Contraseña*  
 Opcional. A **cadena** valor que contiene la contraseña que comprueba si es necesario, *nombre de usuario*.  
  
## <a name="remarks"></a>Comentarios  
 *Origen* puede ser:  
  
-   UNA DIRECCIÓN URL. Si el protocolo para la dirección URL es http, se invocará el proveedor de Internet de forma predeterminada. Si la dirección URL señala a un nodo que contiene una secuencia de comandos ejecutable (como un. Página ASP), un **registro** que contiene el origen en lugar de ejecutado contenido se abre de forma predeterminada. Use la *opciones* argumento para modificar este comportamiento.  
  
-   A **registro** objeto. A **registro** objeto abierto desde otro **registro** duplicará el original **registro** objeto.  
  
-   A **comando** objeto. El abierto **registro** objeto representa la fila devuelta por la ejecución del **comando**. Si los resultados contienen más de una sola fila, el contenido de la primera fila se coloca en el registro y se pueden agregar a un error la **errores** colección.  
  
-   Una instrucción SELECT de SQL. El abierto **registro** objeto representa la fila devuelta por la ejecución del contenido de la cadena. Si los resultados contienen más de una sola fila, el contenido de la primera fila se coloca en el registro y se pueden agregar a un error la **errores** colección.  
  
-   Un nombre de tabla.  
  
 Si el **registro** objeto representa una entidad que no se puede tener acceso mediante una dirección URL (por ejemplo, una fila de un **Recordset** derivado de una base de datos), los valores de la [ParentURL](../../../ado/reference/ado-api/parenturl-property-ado.md)propiedad y el campo que se obtiene acceso con el **adRecordURL** constante son null.  
  
> [!NOTE]
>  Direcciones URL que utilizan el esquema http, se invocarán automáticamente el [proveedor Microsoft OLE DB para Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obtener más información, consulte [absoluto y direcciones URL relativas](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Open (método) (conexión de ADO)](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Open (método) (conjunto de registros ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Open (método) (Stream de ADO)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [Método OpenSchema](../../../ado/reference/ado-api/openschema-method.md)
