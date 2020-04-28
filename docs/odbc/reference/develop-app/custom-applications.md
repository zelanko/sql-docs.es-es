---
title: Aplicaciones personalizadas | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305286"
---
# <a name="custom-applications"></a>Aplicaciones personalizadas
Normalmente, las aplicaciones personalizadas realizan una tarea específica para algunos DBMS. Por ejemplo, una aplicación puede recuperar datos de un solo DBMS y generar un informe, o puede transferir datos entre varios DBMS. Lo que estas aplicaciones tienen en común es que estos DBMS se conocen antes de que se escriba la aplicación y no es probable que cambien a lo largo de la vida de la aplicación.  
  
 Por lo tanto, la aplicación personalizada requiere poca o ninguna interoperabilidad. El desarrollador de la aplicación puede elegir un solo controlador para cada DBMS y el código directamente para esos controladores. La aplicación puede contener de forma segura código específico del controlador para aprovechar las capacidades de esos controladores e incluso puede realizar llamadas a la API de base de datos nativa para usar la funcionalidad no admitida por ODBC.  
  
 La principal preocupación de la interoperabilidad de la mayoría de las aplicaciones personalizadas es si los DBMS de destino cambiarán en el futuro. Si es así, este proceso se puede simplificar escribiendo más código interoperable con el que empezar. Sin embargo, este cambio de DBMS es poco frecuente y generalmente conlleva una gran cantidad de trabajo. Por este motivo, los desarrolladores de aplicaciones personalizadas raramente optan por aumentar la interoperabilidad a costa de la funcionalidad. Normalmente, optan por recodificar esa funcionalidad cuando cambian DBMS.
