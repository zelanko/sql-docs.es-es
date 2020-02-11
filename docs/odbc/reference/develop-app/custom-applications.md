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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 240bdf074fbe7fd28f5aafff5c1bbab7651d0c71
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68067475"
---
# <a name="custom-applications"></a>Aplicaciones personalizadas
Normalmente, las aplicaciones personalizadas realizan una tarea específica para algunos DBMS. Por ejemplo, una aplicación puede recuperar datos de un solo DBMS y generar un informe, o puede transferir datos entre varios DBMS. Lo que estas aplicaciones tienen en común es que estos DBMS se conocen antes de que se escriba la aplicación y no es probable que cambien a lo largo de la vida de la aplicación.  
  
 Por lo tanto, la aplicación personalizada requiere poca o ninguna interoperabilidad. El desarrollador de la aplicación puede elegir un solo controlador para cada DBMS y el código directamente para esos controladores. La aplicación puede contener de forma segura código específico del controlador para aprovechar las capacidades de esos controladores e incluso puede realizar llamadas a la API de base de datos nativa para usar la funcionalidad no admitida por ODBC.  
  
 La principal preocupación de la interoperabilidad de la mayoría de las aplicaciones personalizadas es si los DBMS de destino cambiarán en el futuro. Si es así, este proceso se puede simplificar escribiendo más código interoperable con el que empezar. Sin embargo, este cambio de DBMS es poco frecuente y generalmente conlleva una gran cantidad de trabajo. Por este motivo, los desarrolladores de aplicaciones personalizadas raramente optan por aumentar la interoperabilidad a costa de la funcionalidad. Normalmente, optan por recodificar esa funcionalidad cuando cambian DBMS.
