---
title: InvokeService (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- InvokeService [RDS]
ms.assetid: ad45c676-ec7e-4a3a-9a6b-a54f75eb3012
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 86ebb27ebdc5de5a045304afe45cd8653e491827
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67963860"
---
# <a name="invokeservice-rds"></a>InvokeService (RDS)
Devuelve un puntero a la interfaz solicitada en una versión con más capacidad del objeto.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo de Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Deben migrar las aplicaciones que usan RDS a [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object.InvokeService(REFID riid, IUknown* punkNotSoFunctionalInterface, IUknown** ppunkMoreFunctionalInterface) As HRESULT  
```  
  
#### <a name="parameters"></a>Parámetros  
 *riid*  
  
 [in] El identificador de la interfaz que se solicita.  
  
 *punkNotSoFunctionalInterface*  
  
 [in] El objeto de origen de menor capacidad.  
  
 *ppunkMoreFunctionalInterface*  
  
 [out] La dirección de la variable de puntero que recibe el puntero de interfaz solicitado en *riid*. Tras la devolución es correcta, el *ppunkMoreFunctionalInterface* parámetro contiene el puntero de interfaz solicitado en el objeto. Si el objeto no es compatible con la interfaz especificada en *riid*, *ppunkMoreFunctionalInterface* se establece en NULL.  
  
## <a name="return-value"></a>Valor devuelto  
 Un valor HRESULT que indica si la llamada a la **InvokeService** método tuvo éxito.  
  
## <a name="remarks"></a>Comentarios  
 La implementación del motor de cursor RDS de **InvokeService** toma el conjunto de filas de entrada (o el objeto de resultados múltiples), rellena el motor de cursor del conjunto de filas de entrada y, a continuación, devuelve un puntero en sí mismo.  
  
## <a name="applies-to"></a>Se aplica a  
 [Interfaz IRDSService (RDS)](../../../ado/reference/rds-api/irdsservice-interface-rds.md)  
  
## <a name="see-also"></a>Vea también  
 [Métodos RDS](../../../ado/reference/rds-api/rds-methods.md)


