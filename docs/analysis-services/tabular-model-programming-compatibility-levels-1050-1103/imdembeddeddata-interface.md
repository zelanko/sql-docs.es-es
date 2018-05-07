---
title: Interfaz IMDEmbeddedData | Documentos de Microsoft
ms.custom: ''
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: 9dba8c68-4bef-4c2b-815c-c286f1a1939b
caps.latest.revision: 9
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 645f672d00fe685cbb19d6494a6f0f37a61c174b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="imdembeddeddata-interface"></a>Interfaz IMDEmbeddedData
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  La interfaz de IMDEmbeddedData es una interfaz pública que se utiliza para administrar un incrustado [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] base de datos o una base de datos de modelo tabular. La interfaz hereda de la **IPersistStream** interfaz. La interfaz permite las siguientes operaciones:  
  
-   Obtenga un identificador para el flujo incrustado en el documento contenedor.  
  
-   Establezca la dirección URL del documento contenedor.  
  
-   Establezca una marca para indicar si la aplicación de incrustación está en un entorno hospedado.  
  
-   Establezca la ruta de acceso a los archivos temporales que usa la aplicación de incrustación.  
  
-   Cancele la operación incrustada actual.  
  
-   Obtenga el tamaño calculado (en bytes) del flujo para guardar el objeto incrustado. Se hereda de **IPersistStream**.  
  
-   Compruebe si la base de datos incrustada ha cambiado desde que se guardó por última vez. Se hereda de **IPersistStream**.  
  
-   Cargue la base de datos incrustada en el motor local o en proceso. Se hereda de **IPersistStream**.  
  
-   Guarde la base de datos local o en proceso en el flujo incrustado en el documento contenedor. Se hereda de **IPersistStream**.  
  
## <a name="reference"></a>Referencia  
 La siguiente referencia documenta la **IMDEmbeddedData** tal como se presenta en la interfaz **msmd.h** archivo de encabezado.  
  
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
  
#### <a name="description"></a>Description  
 Obtiene el identificador que usa la aplicación host para el flujo incrustado en el documento contenedor.  
  
#### <a name="parameters"></a>Parámetros  
 *out_pbstrStreamId*  
 Especifica la ubicación del identificador del flujo.  
  
#### <a name="return-value"></a>Valor devuelto  
 **S_OK**  
 El identificador del flujo se devolvió correctamente.  
  
 **S_FALSE**  
 No hay ningún identificador del flujo.  
  
 **E_FAIL**  
 Se produjo un error al tener acceso al identificador del flujo.  
  
#### <a name="remarks"></a>Comentarios  
 Para comprobar si la conexión actual contiene una base de datos incrustada, el usuario debería comprobar el valor de la propiedad DBPROP_MSMD_EMBEDDED_DATA de las propiedades de conexión OLE DB.  
  
 Los valores posibles de DBPROP_MSMD_EMBEDDED_DATA son:  
  
|Nombre|Value|Definición|  
|----------|-----------|----------------|  
|DBPROPVAL_EMBED_NONE|0x00|No hay ninguna base de datos incrustada|  
|DBPROPVAL_EMBED_EMBEDDED|0x01|La aplicación actual contiene la base de datos incrustada|  
|DBPROPVAL_EMBED_LINKED|0x02|La base de datos incrustada se hospeda en una aplicación remota (es decir, el servidor de SharePoint)|  
  
#### <a name="source"></a>Origen  
  
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
  
#### <a name="description"></a>Description  
 Establece la dirección URL del archivo que contiene el flujo incrustado.  
  
#### <a name="parameters"></a>Parámetros  
 *in_bstrURL*  
 Especifica la dirección URL del documento contenedor.  
  
#### <a name="return-value"></a>Valor devuelto  
 **S_OK**  
 La dirección URL del elemento contenedor se estableció correctamente.  
  
 **E_FAIL**  
 Se produjo un error al establecer la dirección URL del elemento contenedor.  
  
#### <a name="source"></a>Origen  
  
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
  
#### <a name="description"></a>Description  
 Establezca una marca para indicar si la aplicación de incrustación está en un entorno hospedado.  
  
#### <a name="parameters"></a>Parámetros  
 *in_ftHosted*  
 TRUE, si el autor de la llamada se hospeda en una aplicación de servicio (como IIS).  
  
#### <a name="return-value"></a>Valor devuelto  
 **S_OK**  
 La marca se estableció correctamente.  
  
 **E_FAIL**  
 Se produjo un error al establecer la marca.  
  
#### <a name="source"></a>Origen  
  
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
  
#### <a name="description"></a>Description  
 Establezca la ruta de acceso a los archivos temporales que usa la aplicación de incrustación.  
  
#### <a name="parameters"></a>Parámetros  
 *in_bstrPath*  
 Ruta de acceso que usa la aplicación host para los archivos temporales.  
  
#### <a name="return-value"></a>Valor devuelto  
 **S_OK**  
 El directorio de archivo temporal se estableció correctamente.  
  
 **E_FAIL**  
 Se produjo un error al establecer la ruta de acceso.  
  
#### <a name="source"></a>Origen  
  
```  
[id(4), helpstring("Set the path used by the host application for temporary files")]   
 HRESULT SetTempDirPath(  
  [in]  BSTR in_bstrPath);  
```  
  
### <a name="imdembeddeddatacancel"></a>IMDEmbeddedData::Cancel  
  
```  
HRESULT Cancel ( void )  
```  
  
#### <a name="description"></a>Description  
 Cancela la operación de base de datos incrustada actual  
  
#### <a name="parameters"></a>Parámetros  
 Ninguno.  
  
#### <a name="return-value"></a>Valor devuelto  
 **S_OK**  
 La operación se canceló correctamente.  
  
 **DB_E_CANTCANCEL**  
 No hay ninguna operación cancelable actualmente en curso.  
  
 **E_FAIL**  
 Se produjo un error al cancelar la operación incrustada.  
  
#### <a name="source"></a>Origen  
  
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
  
#### <a name="description"></a>Description  
 Obtiene el tamaño calculado (en bytes) del flujo para guardar el objeto incrustado. Se hereda de **IPersistStream**.  
  
#### <a name="parameters"></a>Parámetros  
 *in_bstrPath*  
 Tamaño calculado (en bytes) de la imagen de la base de datos incrustada.  
  
#### <a name="return-value"></a>Valor devuelto  
 **S_OK**  
 El tamaño se obtuvo correctamente.  
  
 **E_FAIL**  
 Se produjo un error al obtener el tamaño.  
  
### <a name="imdembeddeddataisdirty-ipersiststreamisdirty"></a>IMDEmbeddedData::IsDirty (IPersistStream::IsDirty)  
  
```  
HRESULT IsDirty ( void )  
```  
  
#### <a name="description"></a>Description  
 Comprueba si la base de datos incrustada ha cambiado desde que se guardó por última vez. Se hereda de **IPersistStream**.  
  
#### <a name="parameters"></a>Parámetros  
 none  
  
#### <a name="return-values"></a>Devolver valores  
 **S_OK**  
 La base de datos ha cambiado desde que se guardó por última vez.  
  
 **S_FALSE**  
 La base de datos no ha cambiado desde que se guardó por última vez.  
  
 **E_FAIL**  
 Se produjo un error al obtener el estado de la base de datos.  
  
### <a name="imdembeddeddataload-ipersiststreamload"></a>IMDEmbeddedData::Load (IPersistStream::Load)  
  
```  
HRESULT Load (   
    [in] IStream * in_pStm   
    )  
```  
  
#### <a name="description"></a>Description  
 Carga la base de datos incrustada en el motor local o en proceso. Se hereda de **IPersistStream**.  
  
#### <a name="parameters"></a>Parámetros  
 *in_pStm*  
 Puntero a una interfaz de flujo desde donde cargar la base de datos incrustada.  
  
#### <a name="return-values"></a>Devolver valores  
 **S_OK**  
 La base de datos se cargó correctamente.  
  
 **E_OUTOFMEMORY**  
 No hay suficiente memoria para cargar la base de datos.  
  
 **E_FAIL**  
 Se produjo un error al cargar la base de datos diferente **E_OUTOFMEMORY**.  
  
### <a name="imdembeddeddatasave-ipersiststreamsave"></a>IMDEmbeddedData::Save (IPersistStream::Save)  
  
```  
HRESULT Save (   
    [in] IStream * in_pStm,  
    [in] BOOL in_fClearDirty  
    )  
```  
  
#### <a name="description"></a>Description  
 Guarda la base de datos local o en proceso en el flujo incrustado en el documento contenedor. Se hereda de **IPersistStream**.  
  
#### <a name="parameters"></a>Parámetros  
 *in_pStm*  
 Puntero a una interfaz de flujo donde guardar la base de datos incrustada.  
  
 *in_fClearDirty*  
 Marca que indica si la marca modificada se debería borrar después de esta operación.  
  
#### <a name="return-values"></a>Devolver valores  
 **S_OK**  
 La base de datos se guardó correctamente.  
  
 **STG_E_CANTSAVE**  
 Se produjo un error al guardar la base de datos diferente **STG_E_MEDIUMFULL**.  
  
 **STG_E_MEDIUMFULL**  
 La base de datos no se pudo guardar porque no queda ningún espacio en el dispositivo de almacenamiento.  
  
  
