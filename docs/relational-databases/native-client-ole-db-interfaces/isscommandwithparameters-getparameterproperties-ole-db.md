---
title: 'Isscommandwithparameters:: Getparameterproperties (OLE DB) | Microsoft Docs'
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ISSCommandWithParameters::GetParameterProperties (OLE DB)
apitype: COM
helpviewer_keywords:
- GetParameterProperties method
ms.assetid: 7f4cc5ea-d028-4fe5-9192-bd153ab3c26c
caps.latest.revision: 29
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 97b9a3a89693271e6dc062359114a7d7bd321bce
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37409144"
---
# <a name="isscommandwithparametersgetparameterproperties-ole-db"></a>ISSCommandWithParameters::GetParameterProperties (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

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
 Un puntero a la memoria que devuelve una matriz de estructuras SSPARAMPROPS. El proveedor asigna memoria para las estructuras y devuelve la dirección a esta memoria; el consumidor libera esta memoria con **IMalloc:: Free** cuando ya no necesita las estructuras. Antes de llamar a **IMalloc:: Free** para *prgParamProperties*, también deben llamar los consumidores **VariantClear** para el *vValue* propiedad de cada estructura DBPROP con el fin de evitar una pérdida de memoria en los casos donde la variante contiene una referencia de tipo (como un BSTR). Si *pcParams* cero como resultado o se produce un error distinto de DB_E_ERRORSOCCURRED, el proveedor no asigna memoria y asegura de que *prgParamProperties* es un puntero nulo en la salida.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 El **GetParameterProperties** método devuelve los mismos códigos de error que el núcleo de OLE DB **ICommandProperties:: GetProperties** no puede ser el método, excepto que DB_S_ERRORSOCCURRED y DB_E_ERRORSOCCURED se genera.  
  
## <a name="remarks"></a>Notas  
 **Isscommandwithparameters:: Getparameterproperties** se comporta de forma coherente con respecto a **GetParameterInfo**. Si [isscommandwithparameters:: SetParameterProperties](../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-setparameterproperties-ole-db.md) o **SetParameterInfo** no se ha llamado a o que se ha llamado con cParams igual a cero, **GetParameterInfo**deriva la información de parámetro y lo devuelve. Si **isscommandwithparameters:: SetParameterProperties** o **SetParameterInfo** ha llamado para al menos un parámetro **isscommandwithparameters:: Getparameterproperties**  devuelve las propiedades solo para esos parámetros para el que **isscommandwithparameters:: SetParameterProperties** se ha llamado. Si **isscommandwithparameters:: SetParameterProperties** se llama después de **isscommandwithparameters:: Getparameterproperties** o **GetParameterInfo**, las llamadas subsiguientes a **isscommandwithparameters:: Getparameterproperties** devuelven los valores invalidados para esos parámetros para el que **isscommandwithparameters:: SetParameterProperties** se ha llamado.  
  
 La estructura SSPARAMPROPS se define del siguiente modo:  
  
 `struct SSPARAMPROPS {`  
  
 `DBORDINAL iOrdinal;`  
  
 `ULONG cPropertySets;`  
  
 `DBPROPSET *rgPropertySets;`  
  
 `};`  
  
|Miembro|Descripción|  
|------------|-----------------|  
|*iOrdinal*|El ordinal del parámetro que se ha pasado.|  
|*cPropertySets*|El número de estructuras DBPROPSET en *rgPropertySets*.|  
|*rgPropertySets*|Un puntero a la memoria que devuelve una matriz de estructuras DBPROPSET.|  
  
## <a name="see-also"></a>Vea también  
 [ISSCommandWithParameters &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-ole-db.md)  
  
  
