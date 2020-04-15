---
title: ISSCommandWithParameters::SetParameterProperties (OLE DB)
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- ISSCommandWithParameters::SetParameterProperties (OLE DB)
apitype: COM
helpviewer_keywords:
- SetParameterProperties method
ms.assetid: 4cd0281a-a2a0-43df-8e46-eb478b64cb4b
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 80cf43e4abc1be19b1a6033174c980aa6d7cd378
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81290193"
---
# <a name="isscommandwithparameterssetparameterproperties-ole-db"></a>ISSCommandWithParameters::SetParameterProperties (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Establece las propiedades de los parámetros por cada parámetro por ordinal o establece las propiedades masivas de los parámetro especificando una matriz de estructuras SSPARAMPROPS.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp
HRESULT SetParameterProperties(  
      DB_UPARAMS cParams,   
      SSPARAMPROPS rgParamProperties[]);  
```  
  
## <a name="arguments"></a>Argumentos  
 *cParams*[in]  
 El número de estructuras SSPARAMPROPS en la matriz *rgParamProperties*. Si este número es cero, **ISSCommandWithParameters::SetParameterProperties** eliminará todas las propiedades que se puedan haber especificado en cualquier parámetro del comando.  
  
 *rgParamProperties*[in]  
 Una matriz de estructuras SSPARAMPROPS que se van a establecer.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 El método **ISSCommandWithParameters::SetParameterProperties** devuelve los mismos códigos de error que el método **ICommandProperties::SetProperties** de OLE DB básico.  
  
## <a name="remarks"></a>Observaciones  
 El establecimiento de propiedades de parámetro con este método se permite por parámetro y por ordinal, o bien mediante una única llamada a **ISSCommandWithParameters::SetParameterProperties** después de generar SSPARAMPROPS desde la matriz de propiedades.  
  
 Se debe llamar al método **SetParameterInfo** antes de llamar al método **ISSCommandWithParameters::SetParameterProperties**. La llamada a `SetParameterProperties(0, NULL)` borra todas las propiedades de parámetro especificadas, en tanto que la llamada a `SetParameterInfo(0,NULL,NULL)` borra toda la información de parámetros, incluidas las propiedades que puedan estar asociadas a un parámetro.  
  
 Llamar a **ISSCommandWithParameters::SetParameterProperties** para especificar propiedades para un parámetro que no es de tipo DBTYPE_XML o DBTYPE_UDT devuelve DB_E_ERRORSOCCURRED o DB_S_ERRORSOCCURRED y marca el campo *dwStatus* de todos los DBPROP contenidos en SSPARAMPROPS para ese parámetro con DBPROPSTATUS_NOTSET. Se debe recorrer la matriz DBPROP de cada DBPROPSET incluido en SSPARAMPROPS para detectar a qué parámetro hace referencia DB_E_ERRORSOCCURRED o DB_S_ERRORSOCCURRED.  
  
 Si se llama a **ISSCommandWithParameters::SetParameterProperties** para especificar las propiedades de parámetros cuya información de parámetro todavía no se ha establecido con **SetParameterInfo**, el proveedor devuelve E_UNEXPECTED con el siguiente mensaje de error:  
  
 No se puede llamar al método SetParameterProperties para los parámetros especificados sin llamar primero al método SetParameterInfo. La información de parámetro debe configurarse antes que las propiedades de parámetro.  
  
 Si la llamada a **ISSCommandWithParameters::SetParameterProperties** contiene algunos parámetros donde se ha establecido la información de parámetro y algunos parámetros donde no se ha establecido, las propiedades dwStatus en DBPROPSET del conjunto de propiedades SSPARAMPROPS devolverán DBSTATUS_NOTSET.  
  
 La estructura SSPARAMPROPS se define del siguiente modo:  

```cpp
struct SSPARAMPROPS {
    DBORDINAL iOrdinal;
    ULONG cPropertySets;
    DBPROPSET *rgPropertySets;
};
```

 Las mejoras en el motor de base de datos a partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] permiten a ISSCommandWithParameters::SetParameterProperties obtener descripciones más precisas de los resultados esperados. Estos resultados más precisos pueden diferir de los valores que devuelve ISSCommandWithParameters::SetParameterProperties en las versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, vea [Detección de metadatos](../../relational-databases/native-client/features/metadata-discovery.md).  
  
|Member|Descripción|  
|------------|-----------------|  
|*iOrdinal*|El ordinal del parámetro que se ha pasado.|  
|*cPropertySets*|El número de estructuras DBPROPSET de *rgPropertySets*.|  
|*rgPropertySets*|Un puntero a la memoria que devuelve una matriz de estructuras DBPROPSET.|  
|||

## <a name="see-also"></a>Consulte también  
 [ISSCommandWithParameters &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-ole-db.md)  
  
  
