---
title: Interfaz IMDEmbedded | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
ms.assetid: 9dba8c68-4bef-4c2b-815c-c286f1a1939b
author: minewiskan
ms.author: owend
ms.openlocfilehash: 331f8c33f7748e6591acd6d6ecda7a03ef7d8137
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84940116"
---
# <a name="imdembedded-interface"></a>Interfaz IMDEmbedded
  La interfaz IMDEmbedded es una interfaz pública utilizada para administrar una base de datos incrustada de PowerPivot o una base de datos de modelo tabular. La interfaz hereda de la interfaz `IPersistStream`. La interfaz permite las siguientes operaciones:  
  
-   Obtenga un identificador para el flujo incrustado en el documento contenedor.  
  
-   Establezca la dirección URL del documento contenedor.  
  
-   Establezca una marca para indicar si la aplicación de incrustación está en un entorno hospedado.  
  
-   Establezca la ruta de acceso a los archivos temporales que usa la aplicación de incrustación.  
  
-   Cancele la operación incrustada actual.  
  
-   Obtenga el tamaño calculado (en bytes) del flujo para guardar el objeto incrustado. Se hereda de `IPersistStream`.  
  
-   Compruebe si la base de datos incrustada ha cambiado desde que se guardó por última vez. Se hereda de `IPersistStream`.  
  
-   Cargue la base de datos incrustada en el motor local o en proceso. Se hereda de `IPersistStream`.  
  
-   Guarde la base de datos local o en proceso en el flujo incrustado en el documento contenedor. Se hereda de `IPersistStream`.  
  
## <a name="reference"></a>Referencia  
 La siguiente referencia documenta la `IMDEmbedded` interfaz, tal como se presenta en el archivo de encabezado **msmd. h** .  
  
### <a name="source-file-pxoembeddeddataidl"></a>Archivo de origen: PXOEmbeddedData.idl  
  
```  
[  
  local,                            
  object,                           
  uuid(6B6691CF-5453-41c2-ADD9-4F320B7FD421),                       
  pointer_default(unique)           
]  
interface IMDEmbeddedData : IPersistStream  
{  
 [id(1), helpstring("Set flag indicating if the application is in a hosted environment")]   
 HRESULT SetHosted(  
  [in] BOOL in_fIsHosted);  
  
 [id(2), helpstring("Set the URL for the document containing the embedded stream")]   
 HRESULT SetContainerURL(  
  [in] BSTR in_bstrURL);  
  
 [id(3), helpstring("Get identifier used to look up embedded stream in container document")]   
 HRESULT GetStreamIdentifier(  
  [out, retval] BSTR* out_pbstrStreamId);  
  
 [id(4), helpstring("Set the path used by the embedding application for temporary files")]   
 HRESULT SetTempDirPath(  
  [in]  BSTR in_bstrPath);  
  
 [id(5), helpstring("Cancel the current operation")]   
 HRESULT Cancel();  
};  
```  
  
### <a name="imdembeddeddatagetstreamidentifier"></a>IMDEmbeddedData::GetStreamIdentifier  
  
```  
HRESULT GetStreamIdentifier (  
    [out, retval] BSTR * out_pbstrStreamId  
    )  
```  
  
#### <a name="description"></a>Descripción  
 Obtiene el identificador que usa la aplicación host para el flujo incrustado en el documento contenedor.  
  
#### <a name="parameters"></a>Parámetros  
 *out_pbstrStreamId*  
 Especifica la ubicación del identificador del flujo.  
  
#### <a name="return-value"></a>Valor devuelto  
 `S_OK`  
 El identificador del flujo se devolvió correctamente.  
  
 `S_FALSE`  
 No hay ningún identificador del flujo.  
  
 `E_FAIL`  
 Se produjo un error al tener acceso al identificador del flujo.  
  
#### <a name="remarks"></a>Comentarios  
 Para comprobar si la conexión actual contiene una base de datos incrustada, el usuario debería comprobar el valor de la propiedad DBPROP_MSMD_EMBEDDED_DATA de las propiedades de conexión OLE DB.  
  
 Los valores posibles de DBPROP_MSMD_EMBEDDED_DATA son:  
  
|Nombre|Value|Definición|  
|----------|-----------|----------------|  
|DBPROPVAL_EMBED_NONE|0x00|No hay ninguna base de datos incrustada|  
|DBPROPVAL_EMBED_EMBEDDED|0x01|La aplicación actual contiene la base de datos incrustada|  
|DBPROPVAL_EMBED_LINKED|0x02|La base de datos incrustada se hospeda en una aplicación remota (es decir, el servidor de SharePoint)|  
  
#### <a name="source"></a>Source  
  
```  
[id(1), helpstring("Get identifier used to look up embedded stream in container document")]   
 HRESULT GetStreamIdentifier(  
  [out, retval] BSTR* out_pbstrStreamId);  
```  
  
### <a name="imdembeddeddatasetcontainerurl"></a>IMDEmbeddedData::SetContainerURL  
  
```  
HRESULT SetContainerURL (  
    [in] BSTR in_bstrURL  
    )  
```  
  
#### <a name="description"></a>Descripción  
 Establece la dirección URL del archivo que contiene el flujo incrustado.  
  
#### <a name="parameters"></a>Parámetros  
 *in_bstrURL*  
 Especifica la dirección URL del documento contenedor.  
  
#### <a name="return-value"></a>Valor devuelto  
 `S_OK`  
 La dirección URL del elemento contenedor se estableció correctamente.  
  
 `E_FAIL`  
 Se produjo un error al establecer la dirección URL del elemento contenedor.  
  
#### <a name="source"></a>Source  
  
```  
[id(2), helpstring("Set the URL for the document containing the embedded stream")]   
 HRESULT SetContainerURL(  
  [in] BSTR in_bstrURL);  
```  
  
### <a name="imdembeddeddatasethosted"></a>IMDEmbeddedData::SetHosted  
  
```  
HRESULT SetHosted (  
    [in] BOOL in_fIsHosted  
    )  
```  
  
#### <a name="description"></a>Descripción  
 Establezca una marca para indicar si la aplicación de incrustación está en un entorno hospedado.  
  
#### <a name="parameters"></a>Parámetros  
 *in_ftHosted*  
 TRUE, si el autor de la llamada se hospeda en una aplicación de servicio (como IIS).  
  
#### <a name="return-value"></a>Valor devuelto  
 `S_OK`  
 La marca se estableció correctamente.  
  
 `E_FAIL`  
 Se produjo un error al establecer la marca.  
  
#### <a name="source"></a>Source  
  
```  
[id(5), helpstring("Set flag indicating if the application is in a hosted environment")]   
 HRESULT SetHosted(  
  [in]  BOOL in_fIsHosted);  
```  
  
### <a name="imdembeddeddatasettempdirpath"></a>IMDEmbeddedData::SetTempDirPath  
  
```  
HRESULT SetTempDirPath (  
    [in] BSTR in_bstrPath  
    )  
```  
  
#### <a name="description"></a>Descripción  
 Establezca la ruta de acceso a los archivos temporales que usa la aplicación de incrustación.  
  
#### <a name="parameters"></a>Parámetros  
 *in_bstrPath*  
 Ruta de acceso que usa la aplicación host para los archivos temporales.  
  
#### <a name="return-value"></a>Valor devuelto  
 `S_OK`  
 El directorio de archivo temporal se estableció correctamente.  
  
 `E_FAIL`  
 Se produjo un error al establecer la ruta de acceso.  
  
#### <a name="source"></a>Source  
  
```  
[id(4), helpstring("Set the path used by the host application for temporary files")]   
 HRESULT SetTempDirPath(  
  [in]  BSTR in_bstrPath);  
```  
  
### <a name="imdembeddeddatacancel"></a>IMDEmbeddedData::Cancel  
  
```  
HRESULT Cancel ( void )  
```  
  
#### <a name="description"></a>Descripción  
 Cancela la operación de base de datos incrustada actual  
  
#### <a name="parameters"></a>Parámetros  
 Ninguno.  
  
#### <a name="return-value"></a>Valor devuelto  
 `S_OK`  
 La operación se canceló correctamente.  
  
 `DB_E_CANTCANCEL`  
 No hay ninguna operación cancelable actualmente en curso.  
  
 `E_FAIL`  
 Se produjo un error al cancelar la operación incrustada.  
  
#### <a name="source"></a>Source  
  
```  
[id(5), helpstring("Cancel the current operation")]   
 HRESULT Cancel();  
```  
  
### <a name="imdembeddeddatagetsizemax-ipersiststreamgetsizemax"></a>IMDEmbeddedData::GetSizeMax (IPersistStream::GetSizeMax)  
  
```  
HRESULT GetSizeMax (  
    [out] ULARGE_INTEGER * out_pcbSize  
    )  
```  
  
#### <a name="description"></a>Descripción  
 Obtiene el tamaño calculado (en bytes) del flujo para guardar el objeto incrustado. Se hereda de `IPersistStream`.  
  
#### <a name="parameters"></a>Parámetros  
 *in_bstrPath*  
 Tamaño calculado (en bytes) de la imagen de la base de datos incrustada.  
  
#### <a name="return-value"></a>Valor devuelto  
 `S_OK`  
 El tamaño se obtuvo correctamente.  
  
 `E_FAIL`  
 Se produjo un error al obtener el tamaño.  
  
### <a name="imdembeddeddataisdirty-ipersiststreamisdirty"></a>IMDEmbeddedData::IsDirty (IPersistStream::IsDirty)  
  
```  
HRESULT IsDirty ( void )  
```  
  
#### <a name="description"></a>Descripción  
 Comprueba si la base de datos incrustada ha cambiado desde que se guardó por última vez. Se hereda de `IPersistStream`.  
  
#### <a name="parameters"></a>Parámetros  
 ninguno  
  
#### <a name="return-values"></a>Valores devueltos  
 `S_OK`  
 La base de datos ha cambiado desde que se guardó por última vez.  
  
 `S_FALSE`  
 La base de datos no ha cambiado desde que se guardó por última vez.  
  
 `E_FAIL`  
 Se produjo un error al obtener el estado de la base de datos.  
  
### <a name="imdembeddeddataload-ipersiststreamload"></a>IMDEmbeddedData::Load (IPersistStream::Load)  
  
```  
HRESULT Load (   
    [in] IStream * in_pStm   
    )  
```  
  
#### <a name="description"></a>Descripción  
 Carga la base de datos incrustada en el motor local o en proceso. Se hereda de `IPersistStream`.  
  
#### <a name="parameters"></a>Parámetros  
 *in_pStm*  
 Puntero a una interfaz de flujo desde donde cargar la base de datos incrustada.  
  
#### <a name="return-values"></a>Valores devueltos  
 `S_OK`  
 La base de datos se cargó correctamente.  
  
 `E_OUTOFMEMORY`  
 No hay suficiente memoria para cargar la base de datos.  
  
 `E_FAIL`  
 Se produjo un error al cargar la base de datos, diferente de `E_OUTOFMEMORY`.  
  
### <a name="imdembeddeddatasave-ipersiststreamsave"></a>IMDEmbeddedData::Save (IPersistStream::Save)  
  
```  
HRESULT Save (   
    [in] IStream * in_pStm,  
    [in] BOOL in_fClearDirty  
    )  
```  
  
#### <a name="description"></a>Descripción  
 Guarda la base de datos local o en proceso en el flujo incrustado en el documento contenedor. Se hereda de `IPersistStream`.  
  
#### <a name="parameters"></a>Parámetros  
 *in_pStm*  
 Puntero a una interfaz de flujo donde guardar la base de datos incrustada.  
  
 *in_fClearDirty*  
 Marca que indica si la marca modificada se debería borrar después de esta operación.  
  
#### <a name="return-values"></a>Valores devueltos  
 `S_OK`  
 La base de datos se guardó correctamente.  
  
 `STG_E_CANTSAVE`  
 Se produjo un error al guardar la base de datos, diferente de `STG_E_MEDIUMFULL`.  
  
 `STG_E_MEDIUMFULL`  
 La base de datos no se pudo guardar porque no queda ningún espacio en el dispositivo de almacenamiento.  
  
  
