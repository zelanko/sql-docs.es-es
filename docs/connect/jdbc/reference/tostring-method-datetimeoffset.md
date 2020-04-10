---
title: Método toString (DateTimeOffset) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e77b9be3-1a02-4769-8acf-ac71d48d6a76
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7bd2254d1725220a3334e1de6c39343c9a6c6582
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80908509"
---
# <a name="tostring-method-datetimeoffset"></a>Método toString (DateTimeOffset)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve una representación de cadena del objeto **DateTimeOffset**.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public String toString()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Una representación de cadena del objeto **DateTimeOffset**.  
  
## <a name="remarks"></a>Observaciones  
 La cadena tiene el formato `YYYY-MM-DD HH:mm:ss[.fffffff] [+|-]HH:mm`.  
  
 Las fracciones de segundo de la cadena devuelta se rellenan con ceros hasta la precisión definida. Por ejemplo, DateTimeOffset.toString formateará un valor **datetimeoffset(6)** con un valor de "2010-03-10 12:34:56.78 -08:00" a "2010-03-10 12:34:56.780000 -08:00".  
  
## <a name="see-also"></a>Consulte también  
 [Clase DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [Miembros DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
