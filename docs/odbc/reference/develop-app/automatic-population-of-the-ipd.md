---
title: "El rellenado automático de la IPD | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- automatically populating ipd [ODBC]
- descriptors [ODBC], automatically populating ipd
- descriptors [ODBC], allocating and freeing
- ipd [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: 1184a7d8-d557-4140-843b-6633ae6deacc
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d637ddfebc0563ed2591740498d519f91e34321e
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="automatic-population-of-the-ipd"></a>Rellenado automático de la IPD
Algunos controladores son capaces de establecer los campos de la IPD después de que se ha preparado una consulta parametrizada. Los campos del descriptor se rellenan automáticamente con la información sobre el parámetro, incluidos el tipo de datos, precisión, escala y otras características. Esto es equivalente a admitir **SQLDescribeParam**. Esta información puede ser especialmente útil para una aplicación cuando no tiene ninguna otra manera de detectar, por ejemplo, cuando se realiza una consulta ad hoc con parámetros que la aplicación no conozca.  
  
 Una aplicación determina si el controlador admite el rellenado automático mediante una llamada a **SQLGetConnectAttr** con una *atributo* de SQL_ATTR_AUTO_IPD. Si se devuelve SQL_TRUE, lo admite el controlador y la aplicación puede habilitar estableciendo el atributo de instrucción de SQL_ATTR_ENABLE_AUTO_IPD en SQL_TRUE.  
  
 Cuándo el rellenado automático se admite y se habilita, el controlador rellena los campos de la IPD después de una instrucción SQL que contiene marcadores de parámetros se ha preparado mediante una llamada a **SQLPrepare**. Una aplicación puede recuperar esta información mediante una llamada a **SQLGetDescField** o **SQLGetDescRec**, o **SQLDescribeParam**. La aplicación puede utilizar la información para enlazar el búfer de aplicación más adecuado para un parámetro o para especificar una conversión de datos para él.  
  
 El rellenado automático de la IPD podría producir una reducción del rendimiento. Una aplicación puede desactivarlo al restablecer el atributo de instrucción de SQL_ATTR_ENABLE_AUTO_IPD SQL_FALSE (el valor predeterminado).

