---
title: Determinar el DBMS de destino y los controladores | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5fe868eb16b48afd83fdd5af7dcd146157338947
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47788473"
---
# <a name="determining-the-target-dbmss-and-drivers"></a>Determinar el DBMS de destino y los controladores
Es la siguiente pregunta que tenga en cuenta, ¿cuáles son el DBMS de destino para la aplicación, y están disponibles los controladores que admiten esos DBMS? Dado que las aplicaciones genéricas tienden a ser muy interoperable, la pregunta de DBMS de destino es más aplicable a las aplicaciones personalizadas y verticales. Sin embargo, la pregunta de controladores de destino se aplica a todas las aplicaciones, porque los controladores varían ampliamente en velocidad, calidad, disponibilidad y compatibilidad con las características. Además, si controladores se pueden redistribuir con la aplicación, el costo y la disponibilidad de los planes de licencia deben considerarse.  
  
 Para muchas aplicaciones personalizadas, el DBMS de destino son obvias: existentes de DBMS que la aplicación está diseñada para tener acceso. También se deben considerar el DBMS al que está prevista la futura migración. Sin embargo, la pregunta importante para estas aplicaciones es qué controlador o controladores para usarlos con ellos. Para otras aplicaciones personalizadas: aquellas que no están diseñados para tener acceso a un DBMS existente, el DBMS de destino se puede elegir en función de la compatibilidad con las características, soporte técnico de usuario simultáneas, disponibilidad de controladores y rentabilidad.  
  
 Para aplicaciones verticales, el destino de que DBMS se eligen normalmente se basa en la compatibilidad con las características, la disponibilidad del controlador y mercado. Por ejemplo, una aplicación vertical diseñada para pequeñas empresas debe tener como destino los DBMS son rentables para esas empresas; una aplicación vertical que se ha diseñado como un complemento de DBMS existentes debe tener como destino ampliamente utilizado DBMS.  
  
 Al elegir el DBMS de destino, se deben considerar las diferencias entre las bases de datos de escritorio y servidores. Las bases de datos de escritorio como dBASE, Paradox y Btrieve son menos eficaces que las bases de datos del servidor. Dado que generalmente se acceden a través de los motores SQL menos eficaces que se encuentra en los controladores basados en archivos más, a menudo hacen carecen de compatibilidad de transacciones lleno, admiten menos usuarios simultáneos y tienen una limitada de SQL. Sin embargo, son económicos y tienen una gran base instalada.  
  
 Las bases de datos del servidor, como Oracle, DB2 y SQL Server proporcionan compatibilidad de transacciones lleno, admiten muchos usuarios simultáneos y tienen SQL avanzadas. Son mucho más caros y tienen una menor base instalada. Por otro lado, los precios de software tienden a ser mayor, un poco el desplazamiento de un mercado potencial más pequeño.  
  
 Por lo tanto, el destino de los DBMS a veces se puede elegir en función de las características necesarias para la aplicación y el mercado de destino de la aplicación. Por ejemplo, un sistema de entrada de pedidos para grandes empresas podría no tener como destino bases de datos de escritorio porque estos no tienen compatibilidad con transacciones adecuados. Un sistema similar diseñado para pequeñas empresas podría excluir muchas bases de datos de servidor basándose en el costo. Y los desarrolladores de aplicaciones genéricas pueden destinar pero evite el uso de las características avanzadas de las bases de datos del servidor.
