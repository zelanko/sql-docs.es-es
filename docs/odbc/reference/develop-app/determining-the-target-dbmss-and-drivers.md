---
title: Determinar el DBMS de destino y los controladores | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- target DBMSs and drivers in interoperability [ODBC]
- interoperability [ODBC], target dbmss and drivers
ms.assetid: 23bee0f6-e12a-4598-b34e-df11a8086829
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 76daa1e2753c91df7a016d4801ddea48bc285eb5
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="determining-the-target-dbmss-and-drivers"></a>Determinar el DBMS de destino y los controladores
La siguiente pregunta a tener en cuenta es, ¿cuáles son el DBMS de destino para la aplicación y los controladores estén disponibles que admiten los DBMS? Dado que las aplicaciones genéricas tienden a ser muy interoperable, la pregunta del DBMS de destino es más apropiada para aplicaciones personalizadas y verticales. Sin embargo, la pregunta de controladores de destino se aplica a todas las aplicaciones, porque los controladores varían ampliamente en velocidad, la calidad, la compatibilidad con las características y la disponibilidad. Además, si hay controladores para redistribuir con la aplicación, el costo y la disponibilidad de planes de licencias deben tenerse en cuenta.  
  
 Para muchas aplicaciones personalizadas, el DBMS de destino son obvios: existentes de DBMS que la aplicación está diseñada para tener acceso. También se deben considerar el DBMS al que se ha planeado futura migración. Sin embargo, la pregunta importante de estas aplicaciones es qué controlador o controladores que puede utilizar con ellas. Para otras aplicaciones personalizadas: aquellos que no están diseñados para tener acceso a un DBMS existente, el DBMS de destino se pueden elegir en función de la compatibilidad con las características, compatibilidad de usuario simultáneas, disponibilidad del controlador y asequibles.  
  
 Para las aplicaciones verticales, el destino de que DBMS se eligen normalmente se basa en compatibilidad con las características, la disponibilidad de controlador y el mercado. Por ejemplo, una aplicación vertical diseñada para pequeñas empresas debe tener como destino DBMS que son accesibles a esas empresas; una aplicación vertical diseñada como un complemento de DBMS existentes debe tener como destino ampliamente utilizado DBMS.  
  
 Al elegir el DBMS de destino, se deben considerar las diferencias entre las bases de datos de escritorio y servidores. Las bases de datos de escritorio, como dBASE y Paradox, Btrieve son menos eficaces que las bases de datos de servidor. Dado que normalmente se acceden a través de los motores SQL menos eficaces que se encuentra en los controladores basados en archivos más, a menudo carecen de compatibilidad con transacciones lleno, admiten menos usuarios simultáneos y tenga limitado SQL. Sin embargo, son económicos y tienen una gran base instalada.  
  
 Las bases de datos de servidor, como Oracle, DB2 y SQL Server proporcionan total compatibilidad con transacciones, admiten muchos usuarios simultáneos y tienen SQL enriquecido. Son mucho más caros y tienen una base instalada más pequeña. Por otro lado, los precios de software tienden a ser superior, un poco el desplazamiento de un mercado más pequeño posible.  
  
 Por lo tanto, el destino de los DBMS a veces puede elegir en función de las características requeridas por la aplicación y mercado de destino de la aplicación. Por ejemplo, un sistema de entrada de pedidos para las grandes organizaciones podría destinarse bases de datos de escritorio porque estos no tienen compatibilidad con transacciones adecuados. Un sistema similar diseñado para las pequeñas empresas puede excluir mayoría bases de datos de servidor basándose en el costo. Y los desarrolladores de aplicaciones genéricas podrían tener como destino ambos pero evite el uso de las características avanzadas que se encuentran en las bases de datos de servidor.
