---
title: 'Isscommandwithparameters:: Getparameterproperties (OLE DB) | Documentos de Microsoft'
description: ISSCommandWithParameters::GetParameterProperties (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ISSCommandWithParameters::GetParameterProperties (OLE DB)
apitype: COM
helpviewer_keywords:
- GetParameterProperties method
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: dcd93da8a4a40af97284ea787ebf359490ebd0c1
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2018
---
# <a name="isscommandwithparametersgetparameterproperties-ole-db"></a>ISSCommandWithParameters::GetParameterProperties (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Devuelve una matriz de estructuras de conjunto de propiedades SSPARAMPROPS, un conjunto de propiedades SSPARAMPROPS para cada parámetro XML o UDT.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
HRESULT GetParameterProperties(  
      DB_UPARAMS *pcParams,  
      SSPARAMPROPS **prgParamProperties);  
```  
  
## <a name="arguments"></a>Argumentos  
 *pcParams*[out] [in]  
 Devuelve un puntero a la memoria que contiene el número de estructuras SSPARAMPROPS en *prgParamProperties*.  
  
 *prgParamProperties*[out]  
 Un puntero a la memoria que devuelve una matriz de estructuras SSPARAMPROPS. El proveedor asigna memoria para las estructuras y devuelve la dirección a esta memoria, el consumidor libera esta memoria con **IMalloc:: Free** cuando ya no necesita las estructuras. Antes de llamar a **IMalloc:: Free** para *prgParamProperties*, el consumidor debe llamar a **VariantClear** para el *vValue* propiedad de cada estructura DBPROP con el fin de evitar una pérdida de memoria en casos donde la variante contenga una referencia de tipo como una cadena BSTR. Si *pcParams* da cero como resultado o se produce un error distinto de DB_E_ERRORSOCCURRED, el proveedor no asigna memoria y se asegura *prgParamProperties* es un puntero nulo en la salida.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 El **GetParameterProperties** método devuelve los mismos códigos de error como el núcleo de OLE DB **ICommandProperties:: GetProperties** método, excepto que DB_S_ERRORSOCCURRED y DB_E_ERRORSOCCURED no puede ser se genera.  
  
## <a name="remarks"></a>Comentarios  
 **Isscommandwithparameters:: Getparameterproperties** método se comporta de forma coherente con respecto a **GetParameterInfo**. Si [isscommandwithparameters:: SetParameterProperties](../../oledb/ole-db-interfaces/isscommandwithparameters-setparameterproperties-ole-db.md) o **SetParameterInfo** no se ha llamado o haber llamado con cParams igual a cero, **GetParameterInfo**deriva la información de parámetros y lo devuelve. Si **isscommandwithparameters:: SetParameterProperties** o **SetParameterInfo** piden al menos un parámetro **isscommandwithparameters:: Getparameterproperties**  método devuelve propiedades solo para esos parámetros para el que **isscommandwithparameters:: SetParameterProperties** se ha llamado. Si **isscommandwithparameters:: SetParameterProperties** se llama después de **isscommandwithparameters:: Getparameterproperties** o **GetParameterInfo**, las llamadas subsiguientes a **isscommandwithparameters:: Getparameterproperties** devolver los valores invalidados para esos parámetros para los que **isscommandwithparameters:: SetParameterProperties** ha llamado al método.  
  
 La estructura SSPARAMPROPS se define del siguiente modo:  
  
 `struct SSPARAMPROPS {`  
  
 `DBORDINAL iOrdinal;`  
  
 `ULONG cPropertySets;`  
  
 `DBPROPSET *rgPropertySets;`  
  
 `};`  
  
|Miembro|Description|  
|------------|-----------------|  
|*iOrdinal*|El ordinal del parámetro que se ha pasado.|  
|*cPropertySets*|El número de estructuras DBPROPSET en *rgPropertySets*.|  
|*rgPropertySets*|Un puntero a la memoria que devuelve una matriz de estructuras DBPROPSET.|  
  
## <a name="see-also"></a>Vea también  
 [ISSCommandWithParameters &#40; OLE DB &#41;](../../oledb/ole-db-interfaces/isscommandwithparameters-ole-db.md)  
  
  
