---
title: Determinación de los DBMS y controladores de destino ( Target DBMSs and Drivers) Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305876"
---
# <a name="determining-the-target-dbmss-and-drivers"></a>Determinar el DBMS de destino y los controladores
La siguiente pregunta a tener en cuenta es, ¿cuáles son los DBMS de destino para la aplicación y qué controladores están disponibles que admiten esos DBMS? Dado que las aplicaciones genéricas tienden a ser altamente interoperables, la cuestión de los DBMS de destino es más aplicable a las aplicaciones personalizadas y verticales. Sin embargo, la cuestión de los controladores de destino se aplica a todas las aplicaciones, ya que los controladores varían ampliamente en velocidad, calidad, compatibilidad con características y disponibilidad. Además, si los controladores deben redistribuirse con la aplicación, es necesario tener en cuenta el costo y la disponibilidad de los planes de licencia.  
  
 Para muchas aplicaciones personalizadas, los DBMS de destino son obvios: son DBMS existentes a los que la aplicación está diseñada para acceder. También deben tenerse en cuenta los DBMS en los que se planifica la migración futura. Sin embargo, la pregunta principal para estas aplicaciones es qué controlador o controladores usar con ellos. Para otras aplicaciones personalizadas, aquellas que no están diseñadas para acceder a un DBMS existente, los DBMS de destino se pueden elegir en función de la compatibilidad con características, el soporte de usuario simultáneo, la disponibilidad del controlador y la asequibilidad.  
  
 Para las aplicaciones verticales, los DBMS de destino se eligen normalmente en función del soporte de características, la disponibilidad del controlador y el mercado. Por ejemplo, una aplicación vertical diseñada para pequeñas empresas debe dirigirse a DBMS que sean asequibles para esas empresas; una aplicación vertical diseñada como un complemento de los DBMS existentes debe dirigirse a LOS DBMS ampliamente utilizados.  
  
 Al elegir DBMS de destino, se deben tener en cuenta las diferencias entre las bases de datos de escritorio y servidor. Las bases de datos de escritorio como dBASE, Paradox y Btrieve son menos eficaces que las bases de datos de servidor. Debido a que generalmente se accede a ellos a través de los motores SQL menos potentes que se encuentran en la mayoría de los controladores basados en archivos, a menudo carecen de compatibilidad completa con transacciones, admiten menos usuarios simultáneos y tienen SQL limitado. Sin embargo, son baratos y tienen una gran base instalada.  
  
 Las bases de datos de servidor como Oracle, DB2 y SQL Server proporcionan compatibilidad completa con transacciones, admiten muchos usuarios simultáneos y tienen SQL enriquecido. Son mucho más caros y tienen una base instalada más pequeña. Por otro lado, los precios del software tienden a ser más altos, algo compensando un mercado potencial más pequeño.  
  
 Por lo tanto, los DBMS de destino a veces se pueden elegir en función de las características requeridas por la aplicación y el mercado objetivo de la aplicación. Por ejemplo, es posible que un sistema de entrada de pedidos para grandes corporaciones no tenga como destino bases de datos de escritorio porque carecen de soporte de transacciones adecuado. Un sistema similar diseñado para pequeñas empresas podría excluir la mayoría de las bases de datos de servidores en función del costo. Y los desarrolladores de aplicaciones genéricas pueden dirigirse a ambos, pero evitar el uso de las características avanzadas que se encuentran en las bases de datos de servidor.
