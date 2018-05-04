---
title: Arquitecturas de acceso de base de datos estándar | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: a9d41800-9068-4b76-895a-32b2853692dd
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 99e0a0eee2636a04d182076bb580b1ccf8069921
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="standard-database-access-architectures"></a>Arquitecturas de acceso de base de datos estándar
Para buscar en los componentes de acceso de la base de datos se describe en la sección anterior, pero resulta que dos de ellos: interfaces de programación y los datos de secuencia protocolos: son buenos candidatos para la estandarización. Los otros dos componentes: IPC mecanismo y protocolos de red, no solo residen en un nivel demasiado bajo, pero son ambos dependen en gran medida de la red y el sistema operativo. Hay también un tercer enfoque, las puertas de enlace, que proporciona posibilidades de normalización.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Interfaz de programación estándar](../../odbc/reference/standard-programming-interface.md)  
  
-   [Protocolo de flujo de datos estándar](../../odbc/reference/standard-data-stream-protocol.md)  
  
-   [Puerta de enlace estándar](../../odbc/reference/standard-gateway.md)
