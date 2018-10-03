---
title: Arquitecturas de acceso de base de datos estándar | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: a9d41800-9068-4b76-895a-32b2853692dd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9ff5ee3c22a01b0b1963f1ca6021e72502aa377b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47724123"
---
# <a name="standard-database-access-architectures"></a>Arquitecturas de acceso a base de datos estándar
Observar los componentes de acceso de la base de datos se describe en la sección anterior, pero resulta que dos de ellos, protocolos de flujo de datos y las interfaces de programación, son buenos candidatos para la estandarización. Los dos componentes, protocolos de red y el mecanismo IPC, no sólo reside en un nivel demasiado bajo, pero que son sumamente dependiente de la red y el sistema operativo. Hay también un tercer enfoque, las puertas de enlace, que ofrece posibilidades de normalización.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Interfaz de programación estándar](../../odbc/reference/standard-programming-interface.md)  
  
-   [Protocolo de flujo de datos estándar](../../odbc/reference/standard-data-stream-protocol.md)  
  
-   [Puerta de enlace estándar](../../odbc/reference/standard-gateway.md)
