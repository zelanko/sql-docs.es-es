---
title: 'Isscommandwithparameters:: Getparameterproperties (OLE DB) | Microsoft Docs'
description: ISSCommandWithParameters::GetParameterProperties (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- ISSCommandWithParameters::GetParameterProperties (OLE DB)
apitype: COM
helpviewer_keywords:
- GetParameterProperties method
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 91bf864bef7178fe7532b33648cdf307d80fe61c
ms.sourcegitcommit: af1d9fc4a50baf3df60488b4c630ce68f7e75ed1
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 11/06/2018
ms.locfileid: "51030280"
---
# <a name="isscommandwithparametersgetparameterproperties-ole-db"></a>ISSCommandWithParameters::GetParameterProperties (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

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
 Un puntero a la memoria que devuelve una matriz de estructuras SSPARAMPROPS. El proveedor asigna memoria para las estructuras y devuelve la dirección a esta memoria; el consumidor libera esa memoria con **IMalloc::Free** cuando ya no necesita las estructuras. Antes de llamar a **IMalloc::Free** para *prgParamProperties*, el consumidor debe llamar también a **VariantClear** para la propiedad *vValue* de cada estructura DBPROP con el fin de evitar una fuga de memoria en los casos donde la variante contenga un tipo de referencia (como un BSTR). Si *pcParams* da cero como resultado o se produce un error distinto de DB_E_ERRORSOCCURRED, el proveedor no asigna memoria y se asegura de que *prgParamProperties* dé como resultado un puntero nulo.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 El método **GetParameterProperties** devuelve los mismos códigos de error que el método OLE DB básico **ICommandProperties::GetProperties**, salvo en que no puede dar DB_S_ERRORSOCCURRED ni DB_E_ERRORSOCCURED.  
  
## <a name="remarks"></a>Notas  
 El método **ISSCommandWithParameters::GetParameterProperties** se comporta de forma coherente con respecto a **GetParameterInfo**. Si no se ha llamado a [ISSCommandWithParameters::SetParameterProperties](../../oledb/ole-db-interfaces/isscommandwithparameters-setparameterproperties-ole-db.md) o **SetParameterInfo**, o bien se les ha llamado con cParams igual a cero, **GetParameterInfo** deriva la información del parámetro y la devuelve. Si se ha llamado a **ISSCommandWithParameters::SetParameterProperties** o a **SetParameterInfo** para por lo menos un parámetro, el método **ISSCommandWithParameters::GetParameterProperties** solo devuelve las propiedades de esos parámetros para los que se ha llamado a **ISSCommandWithParameters::SetParameterProperties**. Si se llama a **ISSCommandWithParameters::SetParameterProperties** después de a **ISSCommandWithParameters::GetParameterProperties** o **GetParameterInfo**, las posteriores llamadas a **ISSCommandWithParameters::GetParameterProperties** devuelven los valores invalidados para esos parámetros para los que se ha llamado al método **ISSCommandWithParameters::SetParameterProperties**.  
  
 La estructura SSPARAMPROPS se define del siguiente modo:  
  
 `struct SSPARAMPROPS {`  
  
 `DBORDINAL iOrdinal;`  
  
 `ULONG cPropertySets;`  
  
 `DBPROPSET *rgPropertySets;`  
  
 `};`  
  
|Miembro|Descripción|  
|------------|-----------------|  
|*iOrdinal*|El ordinal del parámetro que se ha pasado.|  
|*cPropertySets*|El número de estructuras DBPROPSET de *rgPropertySets*.|  
|*rgPropertySets*|Un puntero a la memoria que devuelve una matriz de estructuras DBPROPSET.|  
  
## <a name="see-also"></a>Ver también  
 [ISSCommandWithParameters &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/isscommandwithparameters-ole-db.md)  
  
  
