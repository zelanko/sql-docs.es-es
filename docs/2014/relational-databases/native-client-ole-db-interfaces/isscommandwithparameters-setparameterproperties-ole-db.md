---
title: 'Isscommandwithparameters:: SetParameterProperties (OLE DB) | Microsoft Docs'
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
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
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
 El número de estructuras SSPARAMPROPS en la matriz *rgParamProperties*. Si este número es cero, `ISSCommandWithParameters::SetParameterProperties` eliminará todas las propiedades que es posible que se han especificado para los parámetros del comando.  
  
 *rgParamProperties*[in]  
 Una matriz de estructuras SSPARAMPROPS que se van a establecer.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 El `ISSCommandWithParameters::SetParameterProperties` método devuelve los mismos códigos de error que el núcleo de OLE DB **ICommandProperties:: SetProperties** método.  
  
## <a name="remarks"></a>Comentarios  
 Establecer propiedades de parámetro con este método se permite en una por cada parámetro por ordinal o con una sola `ISSCommandWithParameters::SetParameterProperties` llamar una vez que se ha generado SSPARAMPROPS desde la matriz de propiedades.  
  
 El **SetParameterInfo** método debe llamarse antes de llamar a la `ISSCommandWithParameters::SetParameterProperties` método. La llamada a `SetParameterProperties(0, NULL)` borra todas las propiedades de parámetro especificadas, en tanto que la llamada a `SetParameterInfo(0,NULL,NULL)` borra toda la información de parámetros, incluidas las propiedades que puedan estar asociadas a un parámetro.  
  
 Una llamada a `ISSCommandWithParameters::SetParameterProperties` para especificar propiedades para un parámetro que no es de tipo DBTYPE_XML o DBTYPE_UDT devuelve DB_E_ERRORSOCCURRED o DB_S_ERRORSOCCURRED y marca el *dwStatus* campo de todas las DBPROP incluidas en SSPARAMPROPS para ese parámetro con DBPROPSTATUS_NOTSET. Se debe recorrer la matriz DBPROP de cada DBPROPSET incluido en SSPARAMPROPS para detectar a qué parámetro hace referencia DB_E_ERRORSOCCURRED o DB_S_ERRORSOCCURRED.  
  
 Si `ISSCommandWithParameters::SetParameterProperties` se llama para especificar las propiedades de parámetros cuya información de parámetro no se ha establecido aún con **SetParameterInfo**, el proveedor devuelve E_UNEXPECTED con el mensaje de error siguiente:  
  
 No se puede llamar al método SetParameterProperties para los parámetros especificados sin llamar primero al método SetParameterInfo. La información de parámetro debe configurarse antes que las propiedades de parámetro.  
  
 Si la llamada a `ISSCommandWithParameters::SetParameterProperties` contiene algunos parámetros donde se ha establecido la información de parámetros, y algunos parámetros donde no se ha establecido la información de parámetros, las propiedades dwStatus en DBPROPSET del conjunto de propiedades SSPARAMPROPS devolverán dbstatus_notset.  
  
 La estructura SSPARAMPROPS se define del siguiente modo:  
  
 `struct SSPARAMPROPS {`  
  
 `DBORDINAL iOrdinal;`  
  
 `ULONG cPropertySets;`  
  
 `DBPROPSET *rgPropertySets;`  
  
 `};`  
  
 Mejoras en el motor de base de datos a partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] permitir isscommandwithparameters:: SetParameterProperties obtener descripciones más precisas de los resultados esperados. Estos resultados más precisos pueden diferir de los valores devueltos por isscommandwithparameters:: SetParameterProperties en versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, vea [Detección de metadatos](../native-client/features/metadata-discovery.md).  
  
|Miembro|Descripción|  
|------------|-----------------|  
|*iOrdinal*|El ordinal del parámetro que se ha pasado.|  
|*cPropertySets*|El número de estructuras DBPROPSET de *rgPropertySets*.|  
|*rgPropertySets*|Un puntero a la memoria que devuelve una matriz de estructuras DBPROPSET.|  
  
## <a name="see-also"></a>Vea también  
 [ISSCommandWithParameters &#40;OLE DB&#41;](isscommandwithparameters-ole-db.md)  
  
  
