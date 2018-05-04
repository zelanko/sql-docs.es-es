---
title: Propiedad ConnectionString (ADO) | Documentos de Microsoft
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
apitype: COM
f1_keywords:
- Connection15::ConnectionString
helpviewer_keywords:
- ConnectionString property [ADO]
ms.assetid: 3be75b75-4d36-4479-ab64-9a456869252a
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7e0eefcbbd5a19a161beced2be719326a420577e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="connectionstring-property-ado"></a>Propiedad ConnectionString (ADO)
Indica la información utilizada para establecer una conexión con un origen de datos.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un **cadena** valor.  
  
## <a name="remarks"></a>Comentarios  
 Use la **ConnectionString** propiedad para especificar un origen de datos pasando una cadena de conexión detallada que contiene una serie de *argumento* *= valor* instrucciones separan por punto y coma.  
  
 ADO admite cinco argumentos para la **ConnectionString** propiedad; cualquier otro paso de argumentos directamente al proveedor sin ningún procesamiento mediante ADO. Los argumentos admitidos por ADO son los siguientes.  
  
|Argumento|Description|  
|--------------|-----------------|  
|*Proveedor =*|Especifica el nombre de un proveedor que se usará para la conexión.|  
|*Nombre de archivo =*|Especifica el nombre de un archivo específico del proveedor (por ejemplo, un objeto de origen de datos almacenados) que contiene información de conexión predefinida.|  
|*Proveedor remoto =*|Especifica el nombre de un proveedor que se usará al abrir una conexión de cliente. (Solo servicio de datos remotos).|  
|*Servidor remoto =*|Especifica el nombre de ruta de acceso del servidor que se usará al abrir una conexión de cliente. (Solo servicio de datos remotos).|  
|*DIRECCIÓN URL =*|Especifica la cadena de conexión como una dirección URL absoluta que identifica un recurso, como un archivo o directorio.|  
  
 Después de establecer el **ConnectionString** propiedad y abra el [conexión](../../../ado/reference/ado-api/connection-object-ado.md) de objeto, el proveedor puede alterar el contenido de la propiedad, por ejemplo, mediante la asignación de los nombres de argumento definidos por ADO a sus equivalentes para el proveedor específico.  
  
 El **ConnectionString** propiedad hereda automáticamente el valor utilizado para la *ConnectionString* argumento de la [abiertos](../../../ado/reference/ado-api/open-method-ado-connection.md) método, por lo que puede invalidar actual  **ConnectionString** propiedad durante la **abiertos** llamada al método.  
  
 Dado que la *nombre de archivo* argumento hace que ADO cargue el proveedor asociado, no se puede pasar tanto el *proveedor* y *nombre de archivo* argumentos.  
  
 El **ConnectionString** propiedad es de lectura/escritura cuando la conexión está cerrada y de solo lectura cuando se abre.  
  
 Duplicados de un argumento en el **ConnectionString** propiedad se omite. Se utiliza la última instancia de uno de los argumentos.  
  
> [!NOTE]
>  **Uso de servicios de datos remoto** cuando se utiliza en un lado del cliente **conexión** objeto, el **ConnectionString** propiedad puede incluir solo el *proveedor remoto* y *servidor remoto* parámetros.  
  
 La tabla siguiente muestra el proveedor de ADO predeterminado para cada sistema operativo Windows:  
  
|Proveedor de ADO predeterminado|Sistema operativo Windows|  
|--------------------------|------------------------------|  
|MSDASQL<br /><br /> (Para mejorar la legibilidad del código fuente, especificar explícitamente el nombre del proveedor en la cadena de conexión.)|Windows 2000 (32 bits)<br /><br /> Windows XP (32 bits)<br /><br /> Windows 2003 Server (32 bits)<br /><br /> Windows Vista (32 bits)<br /><br /> Windows Vista Service Pack 1 o posterior (32 bits y 64 bits)<br /><br /> Versiones de Windows posteriores a Windows Vista (32 bits y 64 bits)|  
|No tiene valor predeterminado.<br /><br /> Cuando una aplicación ADO se ejecuta en los siguientes sistemas operativos y no especifica explícitamente el proveedor, ADO devuelve el siguiente error: "ADODB". Conexión: no se especificó ningún proveedor y no hay ningún proveedor predeterminado designado "|Windows 2000 (64 bits)<br /><br /> Windows XP (64 bits)<br /><br /> Windows 2003 Server (64 bits)<br /><br /> Windows Vista (64 bits)|  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conexión (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [ConnectionString, ConnectionTimeout y ejemplo de las propiedades de estado (VB)](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vb.md)   
 [ConnectionString, ConnectionTimeout y ejemplo de las propiedades de estado (VC ++)](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vc.md)   
 [Apéndice A: Proveedores](../../../ado/guide/appendixes/appendix-a-providers.md)
