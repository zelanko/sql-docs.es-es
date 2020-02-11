---
title: Cargando por ordinal | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fdc7728fe06df708efd973423f5c8c05333ce189
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68041601"
---
# <a name="loading-by-ordinal"></a>Cargar por ordinal
En ODBC *2. x*, se puede realizar la carga por ordinal para mejorar el rendimiento del proceso de conexión. Un controlador ODBC *2. x* exporta una función ficticia con el ordinal 199; Cuando el administrador de controladores lo detecta, resuelve las direcciones de las funciones ODBC por ordinal, no por nombre. Esta funcionalidad todavía se admite para los controladores ODBC *2. x* , pero no se admite para los controladores ODBC *3. x* .
