---
title: Rellenado automático de la IPD | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 3d127e2da3397e96059c7d04305a983766ca1db6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47767315"
---
# <a name="automatic-population-of-the-ipd"></a>Rellenado automático de la IPD
Algunos controladores son capaces de establecer los campos de la IPD después de que se ha preparado una consulta parametrizada. Los campos de descriptor se rellenan automáticamente con información sobre el parámetro, incluidos el tipo de datos, precisión, escala y otras características. Esto es equivalente a admitir **SQLDescribeParam**. Esta información puede ser especialmente útil para una aplicación cuando no tiene ninguna otra manera de detectar, por ejemplo, cuando se realiza una consulta ad hoc con parámetros que la aplicación no se conoce.  
  
 Una aplicación determina si el controlador admite el rellenado automático mediante una llamada a **SQLGetConnectAttr** con un *atributo* de SQL_ATTR_AUTO_IPD. Si se devuelve SQL_TRUE, lo admite el controlador y la aplicación puede habilitar estableciendo el atributo de instrucción SQL_ATTR_ENABLE_AUTO_IPD en SQL_TRUE.  
  
 Cuando el rellenado automático es compatible y habilitado, el controlador rellena los campos de la IPD después de una instrucción SQL que contiene marcadores de parámetros se prepara mediante una llamada a **SQLPrepare**. Una aplicación puede recuperar esta información mediante una llamada a **SQLGetDescField** o **SQLGetDescRec**, o **SQLDescribeParam**. La aplicación puede usar la información para enlazar el búfer de aplicación más adecuado para un parámetro o especificar una conversión de datos para él.  
  
 Rellenado automático de la IPD podría producir una reducción del rendimiento. Una aplicación puede desactivarlo al restablecer el atributo de instrucción SQL_ATTR_ENABLE_AUTO_IPD SQL_FALSE (el valor predeterminado).
