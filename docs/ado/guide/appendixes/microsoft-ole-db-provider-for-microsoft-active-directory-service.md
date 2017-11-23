---
title: Proveedor Microsoft OLE DB para el servicio de Microsoft Active Directory | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ADSI provider [ADO]
- Active Directory Service Interfaces provider [ADO]
- providers [ADO], OLE DB provider for Active Directory service
- OLE DB provider for Active Directory service [ADO]
ms.assetid: f9e81452-5675-4cfc-9949-cfbd2fe57534
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: c90c411842da3033b0be46330a2d9f2cb421c90b
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="microsoft-ole-db-provider-for-microsoft-active-directory-service"></a>Proveedor Microsoft OLE DB para el servicio de Microsoft Active Directory
El proveedor de Interfaces de servicio de Active Directory (ADSI) permite ADO para conectarse a servicios de directorio heterogéneos mediante ADSI. Esto proporciona a las aplicaciones ADO acceso de solo lectura a los servicios de directorio de Microsoft Windows NT 4.0 y Microsoft Windows 2000, además de cualquier servicio de directorio compatible con LDAP y servicios de directorio Novell. ADSI se basa en un modelo de proveedor, por lo que si hay un nuevo acceso determinado de proveedor a otro directorio, la aplicación ADO podrá obtener acceso a él sin problemas. El proveedor ADSI es de subprocesamiento libre y está habilitado para Unicode.  
  
## <a name="connection-string-parameters"></a>Parámetros de cadena de conexión  
 Para conectarse a este proveedor, establezca el **proveedor** argumento de la [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) propiedad al siguiente:  
  
```  
ADSDSOObject  
```  
  
 Leer la [proveedor](../../../ado/reference/ado-api/provider-property-ado.md) propiedad devolverá también esta cadena.  
  
## <a name="typical-connection-string"></a>Cadena de conexión típica  
 Una cadena de conexión típica para este proveedor es como sigue:  
  
```  
"Provider=ADSDSOObject;User ID=MyUserID;Password=MyPassword;"  
```  
  
 La cadena consta de las siguientes palabras clave.  
  
|Palabra clave|Description|  
|-------------|-----------------|  
|**Proveedor**|Especifica el proveedor OLE DB para servicios de Active Directory.|  
|**Id. de usuario**|Especifica el nombre de usuario. Si se omite esta palabra clave, se utiliza el inicio de sesión actual.|  
|**Contraseña**|Especifica la contraseña del usuario. Si se omite esta palabra clave. A continuación, se utiliza el inicio de sesión actual.|  
  
> [!NOTE]
>  Si se conecta a un proveedor de origen de datos que admita la autenticación de Windows, debe especificar **Trusted_Connection = yes** o **Integrated Security = SSPI** en lugar de Id. de usuario y contraseña información de la cadena de conexión.  
  
## <a name="command-text"></a>Texto de comando  
 Una cadena de texto de comando de cuatro partes es reconocida por el proveedor en la sintaxis siguiente:  
  
```  
"Root; Filter; Attributes[; Scope]"  
```  
  
|Valor|Description|  
|-----------|-----------------|  
|*Root*|Indica el **ADsPath** objeto desde el que se va a iniciar la búsqueda (es decir, la raíz de la búsqueda).|  
|*Filter*|Indica que el filtro de búsqueda en el formato RFC 1960.|  
|*Atributos*|Indica una lista delimitada por comas de los atributos que se devuelvan.|  
|*Ámbito*|Opcional. A **cadena** que especifica el ámbito de la búsqueda. Puede ser uno de los valores siguientes:<br /><br /> -Base: Sólo busca el objeto base (raíz de la búsqueda).<br />-Nivel: Buscar un solo nivel.<br />-Subárbol, Buscar en todo el subárbol.|  
  
 Por ejemplo:  
  
```  
"<LDAP://DC=ArcadiaBay,DC=COM>;(objectClass=*);sn, givenName; subtree"  
```  
  
 El proveedor también admite la SELECT de SQL para el texto de comando. Por ejemplo:  
  
```  
"SELECT title, telephoneNumber From 'LDAP://DC=Microsoft, DC=COM' WHERE   
objectClass='user' AND objectCategory='Person'"  
```  
  
## <a name="remarks"></a>Comentarios  
 El proveedor no acepta llamadas a procedimientos almacenados o nombres de tabla simples (por ejemplo, el [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md) propiedad siempre será **adCmdText**). Consulte la documentación de Active Directory Service Interfaces para obtener una descripción más detallada de los elementos de texto de comando.  
  
## <a name="recordset-behavior"></a>Comportamiento del conjunto de registros  
 Las tablas siguientes enumeran las características disponibles en un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto abierto mediante este proveedor. El tipo de cursor estático (**adOpenStatic**) está disponible.  
  
 Para obtener más información acerca de **Recordset** comportamiento de la configuración del proveedor, ejecute el [admite](../../../ado/reference/ado-api/supports-method.md) método y enumerar el [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) colección de la  **Conjunto de registros** para determinar si las propiedades dinámicas específicas del proveedor están presentes.  
  
 **Disponibilidad de las propiedades de conjunto de registros ADO estándares:**  
  
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
|[PageCount](../../../ado/reference/ado-api/pagecount-property-ado.md)|solo lectura|  
|[PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md)|lectura/escritura|  
|[RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md)|solo lectura|  
|[Source](../../../ado/reference/ado-api/source-property-ado-recordset.md)|lectura/escritura|  
|[State](../../../ado/reference/ado-api/state-property-ado.md)|solo lectura|  
|[Estado](../../../ado/reference/ado-api/status-property-ado-recordset.md)|solo lectura|  
  
 **Disponibilidad de los métodos de conjunto de registros ADO estándar:**  
  
|Método|¿Está disponible?|  
|------------|----------------|  
|[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)|No|  
|[Cancelar](../../../ado/reference/ado-api/cancel-method-ado.md)|No|  
|[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)|No|  
|[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)|No|  
|[Clon](../../../ado/reference/ado-api/clone-method-ado.md)|Sí|  
|[Cerrar](../../../ado/reference/ado-api/close-method-ado.md)|Sí|  
|[Eliminar](../../../ado/reference/ado-api/delete-method-ado-recordset.md)|No|  
|[GetRows](../../../ado/reference/ado-api/getrows-method-ado.md)|Sí|  
|[Mover](../../../ado/reference/ado-api/move-method-ado.md)|Sí|  
|[MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|Sí|  
|[MoveLast](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|Sí|  
|[MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|Sí|  
|[MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|Sí|  
|[NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)|Sí|  
|[Abrir](../../../ado/reference/ado-api/open-method-ado-recordset.md)|Sí|  
|[Requery](../../../ado/reference/ado-api/requery-method.md)|Sí|  
|[Resincronización](../../../ado/reference/ado-api/resync-method.md)|Sí|  
|[Es compatible con](../../../ado/reference/ado-api/supports-method.md)|Sí|  
|[Update](../../../ado/reference/ado-api/update-method.md)|No|  
|[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)|No|  
  
 Para obtener más información acerca de ADSI y los detalles del proveedor, consulte la documentación de Active Directory Service Interfaces o visite la página Web de ADSI.  
  
## <a name="see-also"></a>Vea también  
 [Propiedad CommandType (ADO)](../../../ado/reference/ado-api/commandtype-property-ado.md)   
 [Propiedad ConnectionString (ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md)   
 [Colección de propiedades (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Propiedad de proveedor (ADO)](../../../ado/reference/ado-api/provider-property-ado.md)   
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Método Supports](../../../ado/reference/ado-api/supports-method.md)
