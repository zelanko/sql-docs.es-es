---
title: Cargando por Ordinal ( Ordinal) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- backward compatibility [ODBC], loading by ordinal
- compatibility [ODBC], loading by ordinal
- loading by ordinal [ODBC]
ms.assetid: 337d90ab-68eb-4940-a2f3-f7d5693ee766
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 64bff8dcdd3802f75dc402c9ada60f82580aca5c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288725"
---
# <a name="loading-by-ordinal"></a>Cargar por ordinal
En ODBC *2.x*, se podría realizar la carga por ordinal para mejorar el rendimiento del proceso de conexión. Un controlador ODBC *2.x* exporta una función ficticia con el ordinal 199; cuando el Administrador de controladores lo detecta, resuelve las direcciones de las funciones ODBC por ordinal, no por nombre. Esta funcionalidad todavía se admite para los controladores ODBC *2.x,* pero no es compatible con los controladores ODBC *3.x.*
