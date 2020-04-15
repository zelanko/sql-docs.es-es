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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ea0aa81188e5e58d3a66032af38700ece2d4e5b4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286505"
---
# <a name="what-is-odbc"></a>¿Qué es ODBC?
Existen muchos conceptos erróneos sobre ODBC en el mundo de la computación. Para el usuario final, es un icono en el Panel de control de Microsoft® Windows®. Para el programador de aplicaciones, es una biblioteca que contiene rutinas de acceso a datos. Para muchos otros, es la respuesta a todos los problemas de acceso a la base de datos jamás imaginados.  
  
 En primer lugar, ODBC es una especificación para una API de base de datos. Esta API es independiente de cualquier DBMS o sistema operativo; aunque este manual utiliza C, la API ODBC es independiente del lenguaje. La API ODBC se basa en las especificaciones de la CLI de Open Group e ISO/IEC. ODBC 3. *x* implementa completamente ambas especificaciones - versiones anteriores de ODBC se basaban en versiones preliminares de estas especificaciones, pero no las implementaba completamente - y agrega características comúnmente necesarias por los desarrolladores de aplicaciones de base de datos basadas en pantalla, como cursores desplazables.  
  
 Las funciones de la API ODBC las implementan los desarrolladores de controladores específicos de DBMS. Las aplicaciones llaman a las funciones de estos controladores para tener acceso a los datos de forma independiente de DBMS. Un administrador de controladores administra la comunicación entre las aplicaciones y los controladores.  
  
 Aunque Microsoft proporciona un administrador de controladores para equipos que ejecutan Microsoft Windows® 95 y versiones posteriores, ha escrito varios controladores ODBC y llama a funciones ODBC desde algunas de sus aplicaciones, cualquiera puede escribir aplicaciones ODBC y controladores. De hecho, la gran mayoría de las aplicaciones ODBC y controladores disponibles hoy en día están escritos por empresas que no sean Microsoft. Además, existen controladores ODBC y aplicaciones en Macintosh® y una variedad de plataformas UNIX.  
  
 Para ayudar a los desarrolladores de aplicaciones y controladores, Microsoft ofrece un kit de desarrollo de software (SDK) ODBC para equipos que ejecutan Windows 95 y versiones posteriores que proporciona el administrador de controladores, el archivo DLL del instalador, las herramientas de prueba y las aplicaciones de ejemplo. Microsoft se ha asociado con Visigenic Software para transferir estos SDK a Macintosh y a una variedad de plataformas UNIX.  
  
 Es importante comprender que ODBC está diseñado para exponer las capacidades de la base de datos, no complementarlas. Por lo tanto, los escritores de aplicaciones no deben esperar que el uso de ODBC transformará repentinamente una base de datos simple en un motor de base de datos relacional con todas las funciones. Tampoco se espera que los escritores de controladores implementen la funcionalidad que no se encuentra en la base de datos subyacente. Una excepción a esto es que los desarrolladores que escriben controladores que acceden directamente a los datos de archivo (como los datos de un archivo Xbase) son necesarios para escribir un motor de base de datos que admita al menos una funcionalidad SQL mínima. Otra excepción es que el componente ODBC del Windows SDK, que anteriormente se incluía en el SDK de microsoft Data Access Components (MDAC), proporciona una biblioteca de cursores que simula cursores desplazables para los controladores que implementan un determinado nivel de funcionalidad.  
  
 Las aplicaciones que usan ODBC son responsables de cualquier funcionalidad entre bases de datos. Por ejemplo, ODBC no es un motor de combinación heterogéneo, ni es un procesador de transacciones distribuidas. Sin embargo, dado que es independiente de DBMS, se puede utilizar para crear estas herramientas entre bases de datos.
