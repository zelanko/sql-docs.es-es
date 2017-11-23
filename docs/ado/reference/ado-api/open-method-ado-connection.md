---
title: "Open (método) (conexión de ADO) | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Connection15::raw_Open
- Connection15::Open
- _Connection::Open
helpviewer_keywords: Open method [ADO]
ms.assetid: 663defab-5545-4973-9036-24d5882c9737
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 9133d8e959d1831fc1ff64ed1d8ecace96c3f882
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="open-method-ado-connection"></a>Open (método) (conexión de ADO)
Abre una conexión a un origen de datos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
connection.Open ConnectionString, UserID, Password, Options  
```  
  
#### <a name="parameters"></a>Parámetros  
 *ConnectionString*  
 Opcional. A **cadena** valor que contiene información de conexión. Consulte la [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) propiedad para obtener más información sobre los valores válidos.  
  
 *Identificador de usuario*  
 Opcional. A **cadena** valor que contiene un nombre de usuario que se usará al establecer la conexión.  
  
 *Contraseña*  
 Opcional. A **cadena** valor que contiene una contraseña que se usará al establecer la conexión.  
  
 *Opciones*  
 Opcional. A [ConnectOptionEnum](../../../ado/reference/ado-api/connectoptionenum.md) valor que determina si este método debe devolver después (sincrónicamente) o antes (asincrónicamente) se establece la conexión.  
  
## <a name="remarks"></a>Comentarios  
 Mediante el **abiertos** método en un [conexión](../../../ado/reference/ado-api/connection-object-ado.md) objeto establece la conexión física a un origen de datos. Cuando este método finaliza correctamente, la conexión está activa y puede emitir comandos y procesar los resultados.  
  
 Usar opcional *ConnectionString* argumento para especificar una cadena de conexión que contiene una serie de *argumento* *= valor* instrucciones separadas por punto y coma, o un recurso de archivo o directorio identificado con una dirección URL. El **ConnectionString** propiedad hereda automáticamente el valor utilizado para la *ConnectionString* argumento. Por lo tanto, puede establecer la **ConnectionString** propiedad de la **conexión** objeto antes de abrirlo o usar el *ConnectionString* argumento para establecer o reemplazar los parámetros de conexión actual durante la **abiertos** llamada al método.  
  
 Si se pasa de usuario y una contraseña información tanto en el *ConnectionString* argumento y en la parte opcional *UserID* y *contraseña* argumentos, la *UserID*  y *contraseña* argumentos reemplazarán los valores especificados en *ConnectionString*.  
  
 Cuando haya finalizado las operaciones en un formato de archivo **conexión**, use la [cerrar](../../../ado/reference/ado-api/close-method-ado.md) método para liberarlos recursos del sistema asociados. Cerrar un objeto no se quita de la memoria; puede cambiar sus valores de propiedad y usar el **abrir** método para abrirla de nuevo más tarde. Para eliminar completamente un objeto de la memoria, establezca la variable de objeto *nada*.  
  
> [!NOTE]
>  **Uso de servicios de datos remoto** cuando se utiliza en un lado del cliente **conexión** objeto, el **abiertos** método realmente no establece una conexión con el servidor hasta que un [conjunto de registros ](../../../ado/reference/ado-api/recordset-object-ado.md) se abre en el **conexión** objeto.  
  
> [!NOTE]
>  Direcciones URL que utilizan el esquema http, se invocarán automáticamente el [proveedor Microsoft OLE DB para Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obtener más información, consulte [absoluto y direcciones URL relativas](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conexión (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de los métodos de apertura y cierre (VB)](../../../ado/reference/ado-api/open-and-close-methods-example-vb.md)   
 [Ejemplo de los métodos de apertura y cierre (VBScript)](../../../ado/reference/ado-api/open-and-close-methods-example-vbscript.md)   
 [Ejemplo de los métodos de apertura y cierre (VC ++)](../../../ado/reference/ado-api/open-and-close-methods-example-vc.md)   
 [Open (método) (registro de ADO)](../../../ado/reference/ado-api/open-method-ado-record.md)   
 [Open (método) (conjunto de registros ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Open (método) (Stream de ADO)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [Método OpenSchema](../../../ado/reference/ado-api/openschema-method.md)
