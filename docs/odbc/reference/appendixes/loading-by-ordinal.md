---
title: Cargar por Ordinal | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- backward compatibility [ODBC], loading by ordinal
- compatibility [ODBC], loading by ordinal
- loading by ordinal [ODBC]
ms.assetid: 337d90ab-68eb-4940-a2f3-f7d5693ee766
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e37cd9754b402960ca12b0dbdbeaf43a5f2aee61
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="loading-by-ordinal"></a>Cargar por Ordinal
En ODBC 2. *x*, se pudo realizar la carga por ordinal para mejorar el rendimiento del proceso de conexión. Un ODBC 2. *x* controlador exporta una función ficticia con el ordinal 199; cuando el Administrador de controladores lo detecta, resuelve las direcciones de las funciones ODBC por ordinal, no por nombre. Esta funcionalidad todavía se admite para ODBC 2. *x* controladores, pero no es compatible con ODBC 3 *.x* controladores.
