---
title: ActiveConnection (propiedad, ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::ActiveConnection
- Recordset15::get_ActiveConnection
- _Record::ActiveConnection
helpviewer_keywords:
- ActiveConnection property [ADO]
ms.assetid: 52d0a96c-14fb-4ad9-b004-4d821bc0a6db
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 951f43a2842162aa00f664dc83b754d06d8aafb2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63065543"
---
# <a name="activeconnection-property-ado"></a>ActiveConnection (propiedad, ADO)
Indica a qué [conexión](../../../ado/reference/ado-api/connection-object-ado.md) objeto especificado [comando](../../../ado/reference/ado-api/command-object-ado.md), [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md), o [registro](../../../ado/reference/ado-api/record-object-ado.md) pertenece actualmente el objeto.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un **cadena** valor que contiene una definición para una conexión si la conexión está cerrada, o un **Variant** que contiene el actual **conexión** objeto si el conexión está abierta. Valor predeterminado es una referencia de objeto nulo. Consulte la [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) propiedad.  
  
## <a name="remarks"></a>Comentarios  
 Use la **ActiveConnection** propiedad para determinar el **conexión** objeto sobre el que especificado **comando** objeto ejecutará o especificado  **Conjunto de registros** se abrirá.  
  
## <a name="command"></a>Comando  
 Para **comando** objetos, el **ActiveConnection** propiedad es de lectura/escritura.  
  
 Si intenta llamar a la [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) método en un **comando** objeto antes de establecer esta propiedad en un abrir **conexión** objeto o cadena de conexión válida, se produce un error.  
  
 Si un **conexión** se asigna a la **ActiveConnection** propiedad, se debe abrir el objeto. Asignación de un objeto de conexión cerrado, produce un error.  
  
### <a name="note"></a>Nota  
 **Microsoft Visual Basic** configuración la **ActiveConnection** propiedad *nada* desasocia la **comando** objeto desde la actual **Conexión** y hace que el proveedor liberar todos los recursos asociados en el origen de datos. A continuación, puede asociar el **comando** objeto con la misma u otra **conexión** objeto. Algunos proveedores le permiten cambiar la configuración de la propiedad de un **conexión** a otro, sin tener que establecer primero la propiedad en *nada*.  
  
 Si el [parámetros](../../../ado/reference/ado-api/parameters-collection-ado.md) colección de la **comando** objeto contiene los parámetros proporcionados por el proveedor, se borra la colección si se establece la **ActiveConnection** propiedad *nada* o a otro **conexión** objeto. Si crea manualmente [parámetro](../../../ado/reference/ado-api/parameter-object.md) objetos y usarlos para rellenar el **parámetros** colección de la **comando** objeto, estableciendo el **ActiveConnection**  propiedad *nada* o a otro **conexión** objeto deja el **parámetros** intacta de la colección.  
  
 Cerrar la **conexión** objeto con el que un **comando** objeto es conjuntos asociados el **ActiveConnection** propiedad *nada*. Establecer esta propiedad en un cerrado **conexión** objeto genera un error.  
  
## <a name="recordset"></a>Conjunto de registros  
 Para abrir **Recordset** objetos o para **Recordset** objetos cuya propiedad [origen](../../../ado/reference/ado-api/source-property-ado-recordset.md) propiedad está establecida en válido **comando** (objeto), el **ActiveConnection** propiedad es de solo lectura. En caso contrario, es de sólo lectura.  
  
 Puede establecer esta propiedad a una **conexión** objeto o en una cadena de conexión válida. En este caso, el proveedor crea un nuevo **conexión** utilizando esta definición de objeto y se abre la conexión. Además, el proveedor puede establecer esta propiedad a la nueva **conexión** objeto para ofrecerle una manera de obtener acceso a la **conexión** objeto para obtener información extendida de errores o ejecutar otros comandos.  
  
 Si usas el *ActiveConnection* argumento de la [abrir](../../../ado/reference/ado-api/open-method-ado-recordset.md) método para abrir un **Recordset** objeto, el **ActiveConnection** propiedad heredar el valor del argumento.  
  
 Si establece la **origen** propiedad de la **Recordset** objeto válido **comando** variable de objeto, el **ActiveConnection** propiedad de el **Recordset** hereda la configuración de la **comando** del objeto **ActiveConnection** propiedad.  
  
> [!NOTE]
>  **Uso del servicio de datos remoto** cuando se usa en un cliente **Recordset** objeto, esta propiedad puede establecerse solo en una cadena de conexión o (en Microsoft Visual Basic o Visual Basic Scripting Edition) para *nada* .  
  
## <a name="record"></a>Grabar  
 Esta propiedad es de lectura/escritura cuando el **registro** objeto está cerrado y puede contener una cadena de conexión o una referencia a una apertura **conexión** objeto. Esta propiedad es de solo lectura cuando el **registro** objeto está abierto y contiene una referencia a una apertura **conexión** objeto.  
  
 Un **conexión** objeto se crea implícitamente cuando el **registro** se abre el objeto desde una dirección URL. Abra el **registro** con una existente, abra **conexión** objeto asignando el **conexión** a esta propiedad de objeto, o mediante el **conexión** objeto como un parámetro en el [abierto](../../../ado/reference/ado-api/open-method-ado-record.md) llamada al método. Si el **registro** se abre en una existente **registro** o [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md), a continuación, se asocia automáticamente con la que **registro** o  **Conjunto de registros** del objeto **conexión** objeto.  
  
> [!NOTE]
>  Las direcciones URL con el esquema http, se invocarán automáticamente el [proveedor Microsoft OLE DB para la publicación en Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obtener más información, consulte [absoluto y las direcciones URL relativas](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Se aplica a  
  
||||  
|-|-|-|  
|[Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)|[Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)|[Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|  
  
## <a name="see-also"></a>Vea también  
 [ActiveConnection, CommandText, CommandTimeout, CommandType, tamaño y ejemplo de propiedades de dirección (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, tamaño y ejemplo de propiedades de dirección (VC ++)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, tamaño y ejemplo de propiedades de dirección (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)   
 [Objeto de conexión (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Propiedad ConnectionString (ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md)
