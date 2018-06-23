---
title: 'Isscommandwithparameters:: Getparameterproperties (OLE DB) | Documentos de Microsoft'
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
- ISSCommandWithParameters::GetParameterProperties (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- GetParameterProperties method
ms.assetid: 7f4cc5ea-d028-4fe5-9192-bd153ab3c26c
caps.latest.revision: 28
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: f06c97d1f6d1e477700117c3038d0186db085fd1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36108082"
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
 *pcParams*[out] [in]  
 Devuelve un puntero a la memoria que contiene el número de estructuras SSPARAMPROPS en *prgParamProperties*.  
  
 *prgParamProperties*[out]  
 Un puntero a la memoria que devuelve una matriz de estructuras SSPARAMPROPS. El proveedor asigna memoria para las estructuras y devuelve la dirección a esta memoria; el consumidor libera esta memoria con **IMalloc:: Free** cuando ya no necesita las estructuras. Antes de llamar a **IMalloc:: Free** para *prgParamProperties*, el consumidor debe llamar a **VariantClear** para el *vValue* propiedad de cada estructura DBPROP con el fin de evitar una pérdida de memoria en casos donde la variante contenga una referencia de tipo (por ejemplo, un BSTR). Si *pcParams* da cero como resultado o se produce un error distinto de DB_E_ERRORSOCCURRED, el proveedor no asigna memoria y asegura de que *prgParamProperties* es un puntero nulo en la salida.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 El **GetParameterProperties** método devuelve los mismos códigos de error como el núcleo de OLE DB **ICommandProperties:: GetProperties** método, excepto que DB_S_ERRORSOCCURRED y DB_E_ERRORSOCCURED no puede ser se genera.  
  
## <a name="remarks"></a>Notas  
 **Isscommandwithparameters:: Getparameterproperties** se comporta de forma coherente con respecto a **GetParameterInfo**. Si [isscommandwithparameters:: SetParameterProperties](isscommandwithparameters-setparameterproperties-ole-db.md) o **SetParameterInfo** no se ha llamado o haber llamado con cParams igual a cero, **GetParameterInfo**deriva la información de parámetros y lo devuelve. Si **isscommandwithparameters:: SetParameterProperties** o **SetParameterInfo** piden al menos un parámetro **isscommandwithparameters:: Getparameterproperties**  devuelve propiedades solo para esos parámetros para el que **isscommandwithparameters:: SetParameterProperties** se ha llamado. Si **isscommandwithparameters:: SetParameterProperties** se llama después de **isscommandwithparameters:: Getparameterproperties** o **GetParameterInfo**, las llamadas subsiguientes a **isscommandwithparameters:: Getparameterproperties** devolver los valores invalidados para esos parámetros para los que **isscommandwithparameters:: SetParameterProperties** se ha llamado.  
  
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
 [ISSCommandWithParameters &#40;OLE DB&#41;](isscommandwithparameters-ole-db.md)  
  
  