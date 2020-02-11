---
title: ISSCommandWithParameters::SetParameterProperties (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- ISSCommandWithParameters::SetParameterProperties (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- SetParameterProperties method
ms.assetid: 4cd0281a-a2a0-43df-8e46-eb478b64cb4b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 778021ce007f0c1eac68197e0c07e2cb7b0bb001
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62638767"
---
# <a name="isscommandwithparameterssetparameterproperties-ole-db"></a>ISSCommandWithParameters::SetParameterProperties (OLE DB)
  Establece las propiedades de los parámetros por cada parámetro por ordinal o establece las propiedades masivas de los parámetro especificando una matriz de estructuras SSPARAMPROPS.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
HRESULT SetParameterProperties(  
DB_UPARAMS cParams,   
SSPARAMPROPS rgParamProperties[]);  
```  
  
## <a name="arguments"></a>Argumentos  
 *cParams*[in]  
 El número de estructuras SSPARAMPROPS en la matriz *rgParamProperties*. Si este número es cero, `ISSCommandWithParameters::SetParameterProperties` eliminará todas las propiedades que se puedan haber especificado para los parámetros del comando.  
  
 *rgParamProperties*[in]  
 Una matriz de estructuras SSPARAMPROPS que se van a establecer.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 El `ISSCommandWithParameters::SetParameterProperties` método devuelve los mismos códigos de error que el método básico OLE DB **ICommandProperties:: SetProperties** .  
  
## <a name="remarks"></a>Observaciones  
 La configuración de las propiedades de parámetro con este método se permite por cada parámetro por ordinal o con una `ISSCommandWithParameters::SetParameterProperties` sola llamada una vez que SSPARAMPROPS se ha creado a partir de la matriz de propiedades.  
  
 Se debe llamar al método **SetParameterInfo** antes de llamar `ISSCommandWithParameters::SetParameterProperties` al método. La llamada a `SetParameterProperties(0, NULL)` borra todas las propiedades de parámetro especificadas, en tanto que la llamada a `SetParameterInfo(0,NULL,NULL)` borra toda la información de parámetros, incluidas las propiedades que puedan estar asociadas a un parámetro.  
  
 Llamar `ISSCommandWithParameters::SetParameterProperties` a para especificar las propiedades de un parámetro que no es del tipo DBTYPE_XML o DBTYPE_UDT devuelve DB_E_ERRORSOCCURRED o DB_S_ERRORSOCCURRED y marca el campo *dwStatus* de todos los dbprop contenidos en SSPARAMPROPS para ese parámetro con DBPROPSTATUS_NOTSET. Se debe recorrer la matriz DBPROP de cada DBPROPSET incluido en SSPARAMPROPS para detectar a qué parámetro hace referencia DB_E_ERRORSOCCURRED o DB_S_ERRORSOCCURRED.  
  
 Si `ISSCommandWithParameters::SetParameterProperties` se llama a para especificar las propiedades de los parámetros cuya información de parámetros no se ha establecido todavía con **SetParameterInfo**, el proveedor devuelve E_UNEXPECTED con el siguiente mensaje de error:  
  
 No se puede llamar al método SetParameterProperties para los parámetros especificados sin llamar primero al método SetParameterInfo. La información de parámetro debe configurarse antes que las propiedades de parámetro.  
  
 Si la llamada a `ISSCommandWithParameters::SetParameterProperties` contiene algunos parámetros en los que se ha establecido la información de parámetros y algunos parámetros en los que no se ha establecido la información de parámetros, las propiedades de DWSTATUS del DBPROPSET del conjunto de propiedades SSPARAMPROPS devolverán con DBSTATUS_NOTSET.  
  
 La estructura SSPARAMPROPS se define del siguiente modo:  
  
 `struct SSPARAMPROPS {`  
  
 `DBORDINAL iOrdinal;`  
  
 `ULONG cPropertySets;`  
  
 `DBPROPSET *rgPropertySets;`  
  
 `};`  
  
 Mejoras en el motor de base de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] datos a partir de allow ISSCommandWithParameters:: SetParameterProperties para obtener descripciones más precisas de los resultados esperados. Estos resultados más precisos pueden diferir de los valores devueltos por ISSCommandWithParameters:: SetParameterProperties [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]en versiones anteriores de. Para obtener más información, vea [Detección de metadatos](../native-client/features/metadata-discovery.md).  
  
|Miembro|Descripción|  
|------------|-----------------|  
|*iOrdinal*|El ordinal del parámetro que se ha pasado.|  
|*cPropertySets*|El número de estructuras DBPROPSET de *rgPropertySets*.|  
|*rgPropertySets*|Un puntero a la memoria que devuelve una matriz de estructuras DBPROPSET.|  
  
## <a name="see-also"></a>Consulte también  
 [ISSCommandWithParameters &#40;OLE DB&#41;](isscommandwithparameters-ole-db.md)  
  
  
