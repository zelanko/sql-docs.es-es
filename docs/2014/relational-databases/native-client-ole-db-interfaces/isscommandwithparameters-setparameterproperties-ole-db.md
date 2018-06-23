---
title: 'Isscommandwithparameters:: SetParameterProperties (OLE DB) | Documentos de Microsoft'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- ISSCommandWithParameters::SetParameterProperties (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- SetParameterProperties method
ms.assetid: 4cd0281a-a2a0-43df-8e46-eb478b64cb4b
caps.latest.revision: 31
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: f17947c2b5eb0a8438c074ffca34dca728ae859a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36109237"
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
 El número de estructuras SSPARAMPROPS en la *rgParamProperties* matriz. Si este número es cero, `ISSCommandWithParameters::SetParameterProperties` eliminará todas las propiedades que pueden especificar para los parámetros en el comando.  
  
 *rgParamProperties*[in]  
 Una matriz de estructuras SSPARAMPROPS que se van a establecer.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 El `ISSCommandWithParameters::SetParameterProperties` método devuelve los mismos códigos de error como el núcleo de OLE DB **ICommandProperties:: SetProperties** método.  
  
## <a name="remarks"></a>Notas  
 Establecer las propiedades de parámetro con este método está permitida en cada parámetro por ordinal o con una sola `ISSCommandWithParameters::SetParameterProperties` llamar una vez que se ha generado SSPARAMPROPS desde la matriz de propiedades.  
  
 El **SetParameterInfo** método debe llamarse antes de llamar a la `ISSCommandWithParameters::SetParameterProperties` método. La llamada a `SetParameterProperties(0, NULL)` borra todas las propiedades de parámetro especificadas, en tanto que la llamada a `SetParameterInfo(0,NULL,NULL)` borra toda la información de parámetros, incluidas las propiedades que puedan estar asociadas a un parámetro.  
  
 Al llamar a `ISSCommandWithParameters::SetParameterProperties` para especificar las propiedades de un parámetro que no es de tipo DBTYPE_XML o DBTYPE_UDT devuelve DB_E_ERRORSOCCURRED o DB_S_ERRORSOCCURRED y marca el *dwStatus* campo de todas las DBPROP incluidas en SSPARAMPROPS para ese parámetro con DBPROPSTATUS_NOTSET. Se debe recorrer la matriz DBPROP de cada DBPROPSET incluido en SSPARAMPROPS para detectar a qué parámetro hace referencia DB_E_ERRORSOCCURRED o DB_S_ERRORSOCCURRED.  
  
 Si `ISSCommandWithParameters::SetParameterProperties` se llama para especificar las propiedades de parámetros cuya información de parámetro no se ha establecido aún con **SetParameterInfo**, el proveedor devuelve E_UNEXPECTED con el siguiente mensaje de error:  
  
 No se puede llamar al método SetParameterProperties para los parámetros especificados sin llamar primero al método SetParameterInfo. La información de parámetro debe configurarse antes que las propiedades de parámetro.  
  
 Si la llamada a `ISSCommandWithParameters::SetParameterProperties` contiene algunos parámetros donde se ha establecido la información de parámetros, y algunos parámetros donde no se ha establecido la información de parámetros, las propiedades dwStatus en DBPROPSET del conjunto de propiedades SSPARAMPROPS devolverán dbstatus_notset.  
  
 La estructura SSPARAMPROPS se define del siguiente modo:  
  
 `struct SSPARAMPROPS {`  
  
 `DBORDINAL iOrdinal;`  
  
 `ULONG cPropertySets;`  
  
 `DBPROPSET *rgPropertySets;`  
  
 `};`  
  
 Mejoras en el motor de base de datos a partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] permitir isscommandwithparameters:: SetParameterProperties obtener descripciones más precisas de los resultados esperados. Estos resultados más precisos pueden diferir de los valores devueltos por isscommandwithparameters:: SetParameterProperties en versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, consulte [de detección de metadatos](../native-client/features/metadata-discovery.md).  
  
|Miembro|Descripción|  
|------------|-----------------|  
|*iOrdinal*|El ordinal del parámetro que se ha pasado.|  
|*cPropertySets*|El número de estructuras DBPROPSET en *rgPropertySets*.|  
|*rgPropertySets*|Un puntero a la memoria que devuelve una matriz de estructuras DBPROPSET.|  
  
## <a name="see-also"></a>Vea también  
 [ISSCommandWithParameters &#40;OLE DB&#41;](isscommandwithparameters-ole-db.md)  
  
  