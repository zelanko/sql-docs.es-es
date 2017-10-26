---
title: Cargar por Ordinal | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- backward compatibility [ODBC], loading by ordinal
- compatibility [ODBC], loading by ordinal
- loading by ordinal [ODBC]
ms.assetid: 337d90ab-68eb-4940-a2f3-f7d5693ee766
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ef22486a7cbd9932c90069f461b83358c2db8fd4
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="loading-by-ordinal"></a>Cargar por Ordinal
En ODBC 2. *x*, se pudo realizar la carga por ordinal para mejorar el rendimiento del proceso de conexión. Un ODBC 2. *x* controlador exporta una función ficticia con el ordinal 199; cuando el Administrador de controladores lo detecta, resuelve las direcciones de las funciones ODBC por ordinal, no por nombre. Esta funcionalidad todavía se admite para ODBC 2. *x* controladores, pero no es compatible con ODBC 3*.x* controladores.

