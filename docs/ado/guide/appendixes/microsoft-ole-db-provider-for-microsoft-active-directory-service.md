---
title: Proveedor de Microsoft OLE DB para el servicio Microsoft Active Directory | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADSI provider [ADO]
- Active Directory Service Interfaces provider [ADO]
- providers [ADO], OLE DB provider for Active Directory service
- OLE DB provider for Active Directory service [ADO]
ms.assetid: f9e81452-5675-4cfc-9949-cfbd2fe57534
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e204a4f6f7f395ca93198bc560f4a216d5a70673
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67926679"
---
# <a name="microsoft-ole-db-provider-for-microsoft-active-directory-service"></a>Proveedor de Microsoft OLE DB para el servicio Microsoft Active Directory
El proveedor de interfaces de servicio Active Directory (ADSI) permite a ADO conectarse a servicios de directorio heterogéneos a través de ADSI. Esto proporciona a las aplicaciones ADO acceso de solo lectura a los servicios de directorio Microsoft Windows NT 4,0 y Microsoft Windows 2000, además de cualquier servicio de directorio compatible con LDAP y servicios de directorio de Novell. ADSI se basa en un modelo de proveedor, de modo que si hay un nuevo proveedor que concede acceso a otro directorio, la aplicación ADO podrá tener acceso a él sin problemas. El proveedor ADSI es de subprocesamiento libre y está habilitado para Unicode.  
  
## <a name="connection-string-parameters"></a>Parámetros de la cadena de conexión  
 Para conectarse a este proveedor, establezca el argumento de **proveedor** de la propiedad [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) en lo siguiente:  
  
```vb
ADSDSOObject  
```  
  
 La lectura de la propiedad [Provider](../../../ado/reference/ado-api/provider-property-ado.md) también devolverá esta cadena.  
  
## <a name="typical-connection-string"></a>Cadena de conexión típica  
 Una cadena de conexión típica para este proveedor es la siguiente:  
  
```vb
"Provider=ADSDSOObject;User ID=MyUserID;Password=MyPassword;"  
```  
  
 La cadena consta de las siguientes palabras clave.  
  
|Palabra clave|Descripción|  
|-------------|-----------------|  
|**Proveedor**|Especifica el proveedor de OLE DB para Active Directory servicio.|  
|**Id. de usuario**|Especifica el nombre de usuario. Si se omite esta palabra clave, se usa el inicio de sesión actual.|  
|**Contraseña**|Especifica la contraseña del usuario. Si se omite esta palabra clave. A continuación, se usa el inicio de sesión actual.|  
  
> [!NOTE]
>  Si se va a conectar a un proveedor de origen de datos que admite la autenticación de Windows, debe especificar **Trusted_Connection = Yes** o **Integrated Security = SSPI** en lugar de la información de identificador de usuario y contraseña en la cadena de conexión.  
  
## <a name="command-text"></a>Texto de comando  
 El proveedor reconoce una cadena de texto de comando de cuatro partes en la siguiente sintaxis:  
  
```vb
"Root; Filter; Attributes[; Scope]"  
```  
  
|Value|Descripción|  
|-----------|-----------------|  
|*Raíces*|Indica el objeto **ADsPath** desde el que se va a iniciar la búsqueda (es decir, la raíz de la búsqueda).|  
|*Filter*|Indica el filtro de búsqueda en el formato RFC 1960.|  
|*Atributos*|Indica una lista delimitada por comas de atributos que se van a devolver.|  
|*Ámbito*|Opcional. **Cadena** que especifica el ámbito de la búsqueda. Puede ser uno de los siguientes:<br /><br /> -Base: busca solo el objeto base (raíz de la búsqueda).<br />-OneLevel: busca solo un nivel.<br />-Subárbol: busca en todo el subárbol.|  
  
 Por ejemplo:  
  
```vb
"<LDAP://DC=ArcadiaBay,DC=COM>;(objectClass=*);sn, givenName; subtree"  
```  
  
 El proveedor también admite la selección de SQL para el texto del comando. Por ejemplo:  
  
```vb
"SELECT title, telephoneNumber From 'LDAP://DC=Microsoft, DC=COM' WHERE   
objectClass='user' AND objectCategory='Person'"  
```  
  
## <a name="remarks"></a>Observaciones  
 El proveedor no acepta llamadas a procedimientos almacenados ni nombres de tabla simples (por ejemplo, la propiedad [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md) siempre será **adCmdText**). Consulte la documentación sobre las interfaces de servicio de Active Directory para obtener una descripción más detallada de los elementos de texto de comando.  
  
## <a name="recordset-behavior"></a>Comportamiento del conjunto de registros  
 En las tablas siguientes se enumeran las características disponibles en un objeto de [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) abierto con este proveedor. Solo está disponible el tipo de cursor estático (**adOpenStatic**).  
  
 Para obtener más información sobre el comportamiento del **conjunto de registros** para la configuración del proveedor, ejecute el método [Supports](../../../ado/reference/ado-api/supports-method.md) y enumere la colección [Properties](../../../ado/reference/ado-api/properties-collection-ado.md) del **conjunto de registros** para determinar si las propiedades dinámicas específicas del proveedor están presentes.  
  
 **Disponibilidad de propiedades de conjunto de registros de ADO estándar:**  
  
|Propiedad|Disponibilidad|  
|--------------|------------------|  
|[AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)|lectura/escritura|  
|[AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)|lectura/escritura|  
|[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)|solo lectura|  
|[BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)|solo lectura|  
|[Marcador](../../../ado/reference/ado-api/bookmark-property-ado.md)|lectura/escritura|  
|[CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md)|lectura/escritura|  
|[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)|siempre **adUseServer**|  
|[CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)|siempre **adOpenStatic**|  
|[EditMode](../../../ado/reference/ado-api/editmode-property.md)|siempre **adEditNone**|  
|[EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)|solo lectura|  
|[Filter](../../../ado/reference/ado-api/filter-property.md)|lectura/escritura|  
|[LockType](../../../ado/reference/ado-api/locktype-property-ado.md)|lectura/escritura|  
|[MarshalOptions](../../../ado/reference/ado-api/marshaloptions-property-ado.md)|no disponible|  
|[MaxRecords](../../../ado/reference/ado-api/maxrecords-property-ado.md)|lectura/escritura|  
|[NúmeroDePáginas](../../../ado/reference/ado-api/pagecount-property-ado.md)|solo lectura|  
|[PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md)|lectura/escritura|  
|[RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md)|solo lectura|  
|[Origen](../../../ado/reference/ado-api/source-property-ado-recordset.md)|lectura/escritura|  
|[State](../../../ado/reference/ado-api/state-property-ado.md)|solo lectura|  
|[Estado](../../../ado/reference/ado-api/status-property-ado-recordset.md)|solo lectura|  
  
 **Disponibilidad de métodos de conjunto de registros de ADO estándar:**  
  
|Método|¿Disponible?|  
|------------|----------------|  
|[AgregarNuevo](../../../ado/reference/ado-api/addnew-method-ado.md)|No|  
|[Cancelar](../../../ado/reference/ado-api/cancel-method-ado.md)|No|  
|[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)|No|  
|[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)|No|  
|[Clonar](../../../ado/reference/ado-api/clone-method-ado.md)|Sí|  
|[Cerrar](../../../ado/reference/ado-api/close-method-ado.md)|Sí|  
|[Eliminar](../../../ado/reference/ado-api/delete-method-ado-recordset.md)|No|  
|[GetRows](../../../ado/reference/ado-api/getrows-method-ado.md)|Sí|  
|[Move](../../../ado/reference/ado-api/move-method-ado.md)|Sí|  
|[MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|Sí|  
|[MoveLast](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|Sí|  
|[MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|Sí|  
|[MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|Sí|  
|[NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)|Sí|  
|[Abrir](../../../ado/reference/ado-api/open-method-ado-recordset.md)|Sí|  
|[Requery](../../../ado/reference/ado-api/requery-method.md)|Sí|  
|[Resincronizar](../../../ado/reference/ado-api/resync-method.md)|Sí|  
|[Admite](../../../ado/reference/ado-api/supports-method.md)|Sí|  
|[Actualizar](../../../ado/reference/ado-api/update-method.md)|No|  
|[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)|No|  
  
 Para obtener más información acerca de ADSI y los detalles del proveedor, consulte la documentación sobre las interfaces del servicio Active Directory o visite la Página Web de ADSI.  
  
## <a name="see-also"></a>Consulte también  
 [CommandType (propiedad, ADO)](../../../ado/reference/ado-api/commandtype-property-ado.md)   
 [ConnectionString (propiedad, ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md)   
 [Colección Properties (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Provider (propiedad, ADO)](../../../ado/reference/ado-api/provider-property-ado.md)   
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Método Supports](../../../ado/reference/ado-api/supports-method.md)
