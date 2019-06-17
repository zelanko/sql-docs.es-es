---
title: Método Open (ADO Connection) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::raw_Open
- Connection15::Open
- _Connection::Open
helpviewer_keywords:
- Open method [ADO]
ms.assetid: 663defab-5545-4973-9036-24d5882c9737
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 01d18e643dd769daa22309bb6c3df6407ab9043f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66719167"
---
# <a name="open-method-ado-connection"></a>Open (método) (conexión de ADO)
Abre una conexión a un origen de datos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
connection.Open ConnectionString, UserID, Password, Options  
```  
  
#### <a name="parameters"></a>Parámetros  
 *ConnectionString*  
 Opcional. Un **cadena** valor que contiene información de conexión. Consulte la [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) propiedad para obtener más información sobre los valores válidos.  
  
 *UserID*  
 Opcional. Un **cadena** valor que contiene un nombre de usuario que se usará al establecer la conexión.  
  
 *Contraseña*  
 Opcional. Un **cadena** valor que contiene una contraseña que se usará al establecer la conexión.  
  
 *Opciones*  
 Opcional. Un [ConnectOptionEnum](../../../ado/reference/ado-api/connectoptionenum.md) valor que determina si este método debe devolver después (sincrónicamente) o antes (asincrónicamente) se establece la conexión.  
  
## <a name="remarks"></a>Comentarios  
 Mediante el **abierto** método en un [conexión](../../../ado/reference/ado-api/connection-object-ado.md) objeto establece la conexión física a un origen de datos. Cuando este método finaliza correctamente, la conexión está activa y puede emitir comandos y procesar los resultados.  
  
 Usar el elemento opcional *ConnectionString* argumento para especificar una cadena de conexión que contiene una serie de *argumento* *= valor* instrucciones separadas por punto y coma, o un recurso de archivo o directorio identificado con una dirección URL. El **ConnectionString** propiedad hereda automáticamente el valor utilizado para la *ConnectionString* argumento. Por lo tanto, puede establecer el **ConnectionString** propiedad de la **conexión** objeto antes de abrirlo o usar el *ConnectionString* argumento para establecer o reemplazar los parámetros de conexión actual durante la **abierto** llamada al método.  
  
 Si se pasa el usuario y contraseña información tanto en el *ConnectionString* argumento y opcional *UserID* y *contraseña* argumentos, el *UserID*  y *contraseña* argumentos reemplazarán los valores especificados en *ConnectionString*.  
  
 Cuando haya finalizado las operaciones a través de una abierta **conexión**, utilice el [cerrar](../../../ado/reference/ado-api/close-method-ado.md) método para liberarlos recursos del sistema asociados. Cerrar un objeto no quita de la memoria; puede cambiar la configuración de sus propiedades y utilizar el **abrir** método abrirlo de nuevo más tarde. Para eliminar completamente un objeto de la memoria, establezca la variable de objeto *nada*.  
  
> [!NOTE]
>  **Uso del servicio de datos remoto** cuando se usa en un cliente **conexión** objeto, el **abierto** método no establece una conexión con el servidor hasta que un [conjunto de registros ](../../../ado/reference/ado-api/recordset-object-ado.md) se abre en el **conexión** objeto.  
  
> [!NOTE]
>  Las direcciones URL con el esquema http, se invocarán automáticamente el [proveedor Microsoft OLE DB para la publicación en Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obtener más información, consulte [absoluto y las direcciones URL relativas](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conexión (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de los métodos de apertura y cierre (VB)](../../../ado/reference/ado-api/open-and-close-methods-example-vb.md)   
 [Ejemplo de los métodos Open y Close (VBScript)](../../../ado/reference/ado-api/open-and-close-methods-example-vbscript.md)   
 [Ejemplo de los métodos Open y Close (VC ++)](../../../ado/reference/ado-api/open-and-close-methods-example-vc.md)   
 [Método Open (Record ADO)](../../../ado/reference/ado-api/open-method-ado-record.md)   
 [Método Open (ADO Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Método Open (Stream de ADO)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [Método OpenSchema](../../../ado/reference/ado-api/openschema-method.md)
