---
title: ISSCommandWithParameters::GetParameterProperties (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- ISSCommandWithParameters::GetParameterProperties (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- GetParameterProperties method
ms.assetid: 7f4cc5ea-d028-4fe5-9192-bd153ab3c26c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6d492a64b6d8a4e8ddf7de27067f1f0bcfef205e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62638087"
---
# <a name="isscommandwithparametersgetparameterproperties-ole-db"></a>ISSCommandWithParameters::GetParameterProperties (OLE DB)
  Devuelve una matriz de estructuras de conjunto de propiedades SSPARAMPROPS, un conjunto de propiedades SSPARAMPROPS para cada parámetro XML o UDT.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
HRESULT GetParameterProperties(  
DB_UPARAMS *pcParams,  
SSPARAMPROPS **prgParamProperties);  
```  
  
## <a name="arguments"></a>Argumentos  
 *pcParams*[out][in]  
 Un puntero a la memoria que contiene el número de estructuras SSPARAMPROPS devueltas en *prgParamProperties*.  
  
 *prgParamProperties*[out]  
 Un puntero a la memoria que devuelve una matriz de estructuras SSPARAMPROPS. El proveedor asigna memoria a las estructuras y devuelve la dirección a esta memoria; el consumidor libera esta memoria con **IMalloc:: Free** cuando ya no necesita las estructuras. Antes de llamar a **IMalloc:: Free** para *prgParamProperties*, el consumidor también debe llamar a **VariantClear** para la propiedad *vValue* de cada estructura DBPROP con el fin de evitar una pérdida de memoria en los casos en los que la variante contiene un tipo de referencia (por ejemplo, un BSTR). Si *pcParams* es cero en la salida o se produce un error distinto de DB_E_ERRORSOCCURRED, el proveedor no asigna memoria y se asegura de que *prgParamProperties* sea un puntero nulo en la salida.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 El método **GetParameterProperties** devuelve los mismos códigos de error que el método principal OLE DB **ICommandProperties:: GetProperties** , salvo que no se pueden generar DB_S_ERRORSOCCURRED y DB_E_ERRORSOCCURED.  
  
## <a name="remarks"></a>Observaciones  
 **ISSCommandWithParameters:: GetParameterProperties** se comporta de forma coherente con respecto a **GetParameterInfo**. Si no se ha llamado a [ISSCommandWithParameters:: SetParameterProperties](isscommandwithparameters-setparameterproperties-ole-db.md) o **SetParameterInfo** o se ha llamado a cParams igual a cero, **GetParameterInfo** deriva la información de parámetros y devuelve this. Si se ha llamado a **ISSCommandWithParameters:: SetParameterProperties** o **SetParameterInfo** para al menos un parámetro, **ISSCommandWithParameters:: GetParameterProperties** devuelve propiedades solo para los parámetros para los que se ha llamado a **ISSCommandWithParameters:: SetParameterProperties** . Si se llama a **ISSCommandWithParameters:: SetParameterProperties** después de **ISSCommandWithParameters:: GetParameterProperties** o **GetParameterInfo**, las llamadas subsiguientes a **ISSCommandWithParameters:: GetParameterProperties** devuelven los valores invalidados para los parámetros para los que se ha llamado a **ISSCommandWithParameters:: SetParameterProperties** .  
  
 La estructura SSPARAMPROPS se define del siguiente modo:  
  
 `struct SSPARAMPROPS {`  
  
 `DBORDINAL iOrdinal;`  
  
 `ULONG cPropertySets;`  
  
 `DBPROPSET *rgPropertySets;`  
  
 `};`  
  
|Member|Descripción|  
|------------|-----------------|  
|*iOrdinal*|El ordinal del parámetro que se ha pasado.|  
|*cPropertySets*|El número de estructuras DBPROPSET de *rgPropertySets*.|  
|*rgPropertySets*|Un puntero a la memoria que devuelve una matriz de estructuras DBPROPSET.|  
  
## <a name="see-also"></a>Consulte también  
 [ISSCommandWithParameters &#40;OLE DB&#41;](isscommandwithparameters-ole-db.md)  
  
  
