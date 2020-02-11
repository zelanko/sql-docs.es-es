---
title: ¿Qué es ODBC? | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], about ODBC
ms.assetid: badf3a45-f941-44ae-a31d-393116f68a18
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bda4abf9802bd58e81f35bd4223b28f687e89b4f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67951797"
---
# <a name="what-is-odbc"></a>¿Qué es ODBC?
Muchas de las malentendidos sobre ODBC existen en el mundo informático. Para el usuario final, se trata de un icono del panel de control de Microsoft® Windows®. Para el programador de la aplicación, se trata de una biblioteca que contiene rutinas de acceso a datos. A muchos otros, es la respuesta a todos los problemas de acceso a la base de datos que se han imaginado.  
  
 En primer lugar, ODBC es una especificación para una API de base de datos. Esta API es independiente de un DBMS o sistema operativo. Aunque este manual usa C, la API de ODBC es independiente del lenguaje. La API de ODBC se basa en las especificaciones de la CLI de Open Group e ISO/IEC. ODBC 3. *x* implementa totalmente ambas Especificaciones: las versiones anteriores de ODBC se basaban en las versiones preliminares de estas especificaciones, pero no las implementaba totalmente, y agrega características que suelen necesitar los desarrolladores de aplicaciones de base de datos basadas en pantalla, como los cursores desplazables.  
  
 Las funciones de la API de ODBC las implementan los programadores de controladores específicos del DBMS. Las aplicaciones llaman a las funciones de estos controladores para tener acceso a los datos de una manera independiente del DBMS. Un administrador de controladores administra la comunicación entre aplicaciones y controladores.  
  
 Aunque Microsoft proporciona un administrador de controladores para los equipos que ejecutan Microsoft Windows® 95 y versiones posteriores, ha escrito varios controladores ODBC y llama a las funciones ODBC desde algunas de sus aplicaciones, cualquiera puede escribir aplicaciones y controladores ODBC. De hecho, la gran mayoría de las aplicaciones y los controladores ODBC disponibles hoy en día están escritos por compañías distintas de Microsoft. Además, los controladores y las aplicaciones ODBC existen en la® de Macintosh y en una variedad de plataformas de UNIX.  
  
 Para ayudar a los desarrolladores de aplicaciones y controladores, Microsoft ofrece un kit de desarrollo de software (SDK) de ODBC para equipos que ejecutan Windows 95 y versiones posteriores que proporciona el administrador de controladores, el instalador DLL, las herramientas de prueba y las aplicaciones de ejemplo. Microsoft ha agrupado el software de Visigenic para portar estos SDK a Macintosh y una variedad de plataformas UNIX.  
  
 Es importante comprender que ODBC está diseñado para exponer las capacidades de base de datos, no complementarlas. Por lo tanto, los escritores de aplicaciones no deberían esperar que el uso de ODBC transformase repentinamente una base de datos simple en un motor de base de datos relacional completo. Tampoco se espera que los escritores de controladores implementen la funcionalidad no encontrada en la base de datos subyacente. Una excepción a esto es que los desarrolladores que escriben controladores que acceden directamente a los datos de archivo (como los datos en un archivo xBase) deben escribir un motor de base de datos que admita al menos una funcionalidad mínima de SQL. Otra excepción es que el componente ODBC del Windows SDK, anteriormente incluido en el SDK de Microsoft Data Access Components (MDAC), proporciona una biblioteca de cursores que simula los cursores desplazables para los controladores que implementan un cierto nivel de funcionalidad.  
  
 Las aplicaciones que usan ODBC son responsables de cualquier funcionalidad entre bases de datos. Por ejemplo, ODBC no es un motor de combinación heterogéneo, ni tampoco es un procesador de transacciones distribuidas. Sin embargo, dado que es independiente del DBMS, se puede usar para compilar dichas herramientas entre bases de datos.
