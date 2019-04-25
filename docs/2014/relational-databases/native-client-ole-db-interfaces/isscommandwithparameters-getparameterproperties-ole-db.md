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
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
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
 Un puntero a la memoria que devuelve una matriz de estructuras SSPARAMPROPS. El proveedor asigna memoria para las estructuras y devuelve la dirección a esta memoria; el consumidor libera esta memoria con **IMalloc:: Free** cuando ya no necesita las estructuras. Antes de llamar a **IMalloc:: Free** para *prgParamProperties*, también deben llamar los consumidores **VariantClear** para el *vValue* propiedad de cada estructura DBPROP con el fin de evitar una pérdida de memoria en los casos donde la variante contiene una referencia de tipo (como un BSTR). Si *pcParams* cero como resultado o se produce un error distinto de DB_E_ERRORSOCCURRED, el proveedor no asigna memoria y asegura de que *prgParamProperties* es un puntero nulo en la salida.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 El **GetParameterProperties** método devuelve los mismos códigos de error que el núcleo de OLE DB **ICommandProperties:: GetProperties** no puede ser el método, excepto que DB_S_ERRORSOCCURRED y DB_E_ERRORSOCCURED Elevado.  
  
## <a name="remarks"></a>Comentarios  
 **Isscommandwithparameters:: Getparameterproperties** se comporta de forma coherente con respecto a **GetParameterInfo**. Si [isscommandwithparameters:: SetParameterProperties](isscommandwithparameters-setparameterproperties-ole-db.md) o **SetParameterInfo** no se ha llamado a o que se ha llamado con cParams igual a cero, **GetParameterInfo**deriva la información de parámetro y lo devuelve. Si **isscommandwithparameters:: SetParameterProperties** o **SetParameterInfo** ha llamado para al menos un parámetro **isscommandwithparameters:: Getparameterproperties**  devuelve las propiedades solo para esos parámetros para el que **isscommandwithparameters:: SetParameterProperties** se ha llamado. Si **isscommandwithparameters:: SetParameterProperties** se llama después de **isscommandwithparameters:: Getparameterproperties** o **GetParameterInfo**, las llamadas subsiguientes a **isscommandwithparameters:: Getparameterproperties** devuelven los valores invalidados para esos parámetros para el que **isscommandwithparameters:: SetParameterProperties** se ha llamado.  
  
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
  
## <a name="see-also"></a>Vea también  
 [ISSCommandWithParameters &#40;OLE DB&#41;](isscommandwithparameters-ole-db.md)  
  
  
