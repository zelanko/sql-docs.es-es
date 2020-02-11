---
title: Arquitecturas de acceso a bases de datos estándar | Microsoft Docs
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
ms.openlocfilehash: 5b2113167bb3440c0d772a99b4b8098104d7ed11
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68129247"
---
# <a name="standard-database-access-architectures"></a>Arquitecturas de acceso a base de datos estándar
Al examinar los componentes de acceso a bases de datos descritos en la sección anterior, resulta que dos de ellos son interfaces de programación y protocolos de flujo de datos: son buenos candidatos para la normalización. Los otros dos componentes: el mecanismo IPC y los protocolos de red, no solo residen en un nivel demasiado bajo, pero dependen en gran medida de la red y del sistema operativo. También hay un tercer enfoque: puertas de enlace, que proporcionan posibilidades de normalización.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Interfaz de programación estándar](../../odbc/reference/standard-programming-interface.md)  
  
-   [Protocolo de flujo de datos estándar](../../odbc/reference/standard-data-stream-protocol.md)  
  
-   [Puerta de enlace estándar](../../odbc/reference/standard-gateway.md)
