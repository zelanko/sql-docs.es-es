---
title: Aplicaciones personalizadas ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], custom applications
- custom applications [ODBC]
- interoperability [ODBC], levels
ms.assetid: f28178d9-ecd6-4e8c-9644-9bb624999dcb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: df00a748ee4d5e3a63b32c95449417a1057b58e1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305286"
---
# <a name="custom-applications"></a>Aplicaciones personalizadas
Las aplicaciones personalizadas suelen realizar una tarea específica para algunos DBMS. Por ejemplo, una aplicación podría recuperar datos de un único DBMS y generar un informe, o puede transferir datos entre varios DBMS. Lo que estas aplicaciones tienen en común es que estos DBMS se conocen antes de escribir la aplicación y es poco probable que cambien a lo largo de la vida de la aplicación.  
  
 Por lo tanto, la aplicación personalizada requiere poca o ninguna interoperabilidad. El desarrollador de la aplicación puede elegir un único controlador para cada DBMS y código directamente a esos controladores. La aplicación puede contener de forma segura código específico del controlador para aprovechar las capacidades de esos controladores e incluso puede realizar llamadas a la API de base de datos nativa para usar la funcionalidad no admitida por ODBC.  
  
 La principal preocupación de interoperabilidad de la mayoría de las aplicaciones personalizadas es si los DBMS de destino cambiarán en el futuro. Si es así, este proceso se puede simplificar escribiendo más código interoperable para empezar. Sin embargo, este cambio de DBMS es raro y generalmente implica una gran cantidad de trabajo. Debido a esto, los desarrolladores de aplicaciones personalizadas rara vez optan por aumentar la interoperabilidad a expensas de la funcionalidad; por lo general optan por recodificar esa funcionalidad cuando cambian los DBMS.
