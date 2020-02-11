---
title: Rellenado automático de IPD | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- automatically populating ipd [ODBC]
- descriptors [ODBC], automatically populating ipd
- descriptors [ODBC], allocating and freeing
- ipd [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: 1184a7d8-d557-4140-843b-6633ae6deacc
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c1591843667ef01c6c88f5dfafb734f044679b2d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67909828"
---
# <a name="automatic-population-of-the-ipd"></a>Rellenado automático de la IPD
Algunos controladores pueden establecer los campos de IPD después de preparar una consulta con parámetros. Los campos de descriptor se rellenan automáticamente con información sobre el parámetro, incluidos el tipo de datos, la precisión, la escala y otras características. Esto es equivalente a admitir **SQLDescribeParam**. Esta información puede ser especialmente valiosa para una aplicación cuando no tiene ninguna otra manera de detectarla, por ejemplo, cuando se realiza una consulta ad hoc con parámetros que la aplicación no conoce.  
  
 Una aplicación determina si el controlador admite el rellenado automático mediante una llamada a **SQLGetConnectAttr** con un *atributo* de SQL_ATTR_AUTO_IPD. Si se devuelve SQL_TRUE, el controlador lo admite y la aplicación puede habilitarlo estableciendo el atributo de la instrucción SQL_ATTR_ENABLE_AUTO_IPD en SQL_TRUE.  
  
 Cuando se admite y habilita el rellenado automático, el controlador rellena los campos de IPD después de que una llamada a **SQLPrepare**haya preparado una instrucción SQL que contenga marcadores de parámetros. Una aplicación puede recuperar esta información mediante una llamada a **SQLGetDescField** o **SQLGetDescRec**, o **SQLDescribeParam**. La aplicación puede usar la información para enlazar el búfer de aplicación más adecuado para un parámetro o especificar una conversión de datos para él.  
  
 El rellenado automático de IPD podría producir una reducción del rendimiento. Una aplicación puede desactivarla restableciendo el atributo de instrucción SQL_ATTR_ENABLE_AUTO_IPD en SQL_FALSE (el valor predeterminado).
