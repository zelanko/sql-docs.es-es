---
title: ISSCommandWithParameters::GetParameterProperties (OLE DB)
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- ISSCommandWithParameters::GetParameterProperties (OLE DB)
apitype: COM
helpviewer_keywords:
- GetParameterProperties method
ms.assetid: 7f4cc5ea-d028-4fe5-9192-bd153ab3c26c
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 26c95c64f0f2922ef11946841b160879f001e358
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81290096"
---
# <a name="isscommandwithparametersgetparameterproperties-ole-db"></a>ISSCommandWithParameters::GetParameterProperties (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Devuelve una matriz de estructuras de conjunto de propiedades SSPARAMPROPS, un conjunto de propiedades SSPARAMPROPS para cada parámetro XML o UDT.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp
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
 **ISSCommandWithParameters:: GetParameterProperties** se comporta de forma coherente con respecto a **GetParameterInfo**. Si no se ha llamado a [ISSCommandWithParameters:: SetParameterProperties](../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-setparameterproperties-ole-db.md) o **SetParameterInfo** o se ha llamado a cParams igual a cero, **GetParameterInfo** deriva la información de parámetros y devuelve this. Si se ha llamado a **ISSCommandWithParameters:: SetParameterProperties** o **SetParameterInfo** para al menos un parámetro, **ISSCommandWithParameters:: GetParameterProperties** devuelve propiedades solo para los parámetros para los que se ha llamado a **ISSCommandWithParameters:: SetParameterProperties** . Si se llama a **ISSCommandWithParameters:: SetParameterProperties** después de **ISSCommandWithParameters:: GetParameterProperties** o **GetParameterInfo**, las llamadas subsiguientes a **ISSCommandWithParameters:: GetParameterProperties** devuelven los valores invalidados para los parámetros para los que se ha llamado a **ISSCommandWithParameters:: SetParameterProperties** .  
  
 La estructura SSPARAMPROPS se define del siguiente modo:  

```cpp
struct SSPARAMPROPS {
    DBORDINAL iOrdinal;
    ULONG cPropertySets;
    DBPROPSET *rgPropertySets;
};
```

|Member|Descripción|  
|------------|-----------------|  
|*iOrdinal*|El ordinal del parámetro que se ha pasado.|  
|*cPropertySets*|El número de estructuras DBPROPSET de *rgPropertySets*.|  
|*rgPropertySets*|Un puntero a la memoria que devuelve una matriz de estructuras DBPROPSET.|  
|||

## <a name="see-also"></a>Consulte también  
 [ISSCommandWithParameters &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-ole-db.md)  
  
  
