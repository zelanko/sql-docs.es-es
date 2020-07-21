---
title: Determinación de los DBMS y controladores de destino | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- target DBMSs and drivers in interoperability [ODBC]
- interoperability [ODBC], target dbmss and drivers
ms.assetid: 23bee0f6-e12a-4598-b34e-df11a8086829
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f8811e4d289a8fc89c2c3773aab973df523025f5
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305876"
---
# <a name="determining-the-target-dbmss-and-drivers"></a>Determinar el DBMS de destino y los controladores
La siguiente pregunta a tener en cuenta es, ¿cuáles son los DBMS de destino de la aplicación y qué controladores están disponibles que admiten estos DBMS? Dado que las aplicaciones genéricas tienden a ser altamente interoperables, la cuestión de DBMS de destino es la más aplicable a aplicaciones personalizadas y verticales. Sin embargo, la pregunta de los controladores de destino se aplica a todas las aplicaciones, ya que los controladores varían considerablemente en velocidad, calidad, compatibilidad con características y disponibilidad. Además, si los controladores se van a redistribuir con la aplicación, es necesario tener en cuenta el costo y la disponibilidad de los planes de licencias.  
  
 En el caso de muchas aplicaciones personalizadas, los DBMS de destino son obvios: son DBMS existentes a los que la aplicación está diseñada para acceder. También se deben tener en cuenta los DBMS en los que está planeada la migración futura. Sin embargo, la principal pregunta para estas aplicaciones es el controlador o los controladores que se van a usar con ellas. Para otras aplicaciones personalizadas, que no están diseñadas para tener acceso a un DBMS existente, se pueden elegir los DBMS de destino en función de la compatibilidad de características, la compatibilidad con usuarios simultáneos, la disponibilidad de controladores y la capacidad de asequibilidad.  
  
 En el caso de las aplicaciones verticales, los DBMS de destino se eligen normalmente en función de la compatibilidad de las características, la disponibilidad del controlador y el mercado. Por ejemplo, una aplicación vertical diseñada para pequeñas empresas debe tener como destino DBMS que sean asequibles para esas empresas. una aplicación vertical diseñada como complemento a DBMS existente debe tener como destino DBMS de uso generalizado.  
  
 Al elegir DBMS de destino, se deben tener en cuenta las diferencias entre las bases de datos de servidor y de escritorio. Las bases de datos de escritorio, como dBASE, Paradox y Btrieve, son menos eficaces que las bases de datos de servidor. Dado que normalmente se accede a ellos a través de los motores SQL menos eficaces que se encuentran en la mayoría de los controladores basados en archivos, a menudo carecen de compatibilidad completa con transacciones, admiten menos usuarios simultáneos y tienen SQL limitado. Sin embargo, son económicos y tienen una base de gran tamaño instalada.  
  
 Las bases de datos de servidor como Oracle, DB2 y SQL Server proporcionan compatibilidad completa con las transacciones, admiten muchos usuarios simultáneos y tienen SQL enriquecido. Son mucho más caras y tienen una base más pequeña instalada. Por otro lado, los precios de software tienden a ser más altos, lo que se refiere a un mercado más pequeño posible.  
  
 Por lo tanto, a veces se pueden elegir DBMS de destino en función de las características requeridas por la aplicación y el mercado de destino de la aplicación. Por ejemplo, un sistema de entrada de pedidos para grandes corporaciones podría no tener como destino las bases de datos de escritorio porque estas carecen de compatibilidad de transacciones adecuada. Un sistema similar diseñado para pequeñas empresas podría excluir la mayoría de las bases de datos de servidor en función del costo. Y los desarrolladores de aplicaciones genéricas pueden tener como destino y evitar el uso de las características avanzadas que se encuentran en las bases de datos del servidor.
