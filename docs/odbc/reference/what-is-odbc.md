---
title: ¿Qué es ODBC? | Microsoft Docs
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
ms.topic: article
helpviewer_keywords:
- ODBC [ODBC], about ODBC
ms.assetid: badf3a45-f941-44ae-a31d-393116f68a18
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: ed2f843b8b3c5da54f339d0d3e7f4602246a8d69
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="what-is-odbc"></a>¿Qué es ODBC?
Existen muchos conceptos erróneos acerca de ODBC en el mundo informático. Para el usuario final, es un icono en el Panel de Control de Microsoft® Windows®. Para el programador de aplicaciones, es una biblioteca que contiene rutinas de acceso a datos. Para muchos otros, es la respuesta a todos los problemas de acceso de base de datos nunca imaginado.  
  
 En primer lugar y ante todo, ODBC es una especificación de una API de base de datos. Esta API es independiente de cualquier un DBMS o sistema operativo; Aunque en este manual usa C, la API de ODBC es independiente del lenguaje. La API de ODBC se basa en las especificaciones de CLI de Open Group y ISO/IEC. ODBC 3. *x* implementa por completo de estas especificaciones, versiones anteriores de ODBC se basan en las versiones preliminares de estas especificaciones, pero no los implementó totalmente e incorpora características que normalmente necesarios los programadores de basado en pantalla aplicaciones de base de datos, como los cursores desplazables.  
  
 Las funciones de la API de ODBC se implementan los desarrolladores de controladores específicos de DBMS. Las aplicaciones llaman a las funciones de estos controladores para tener acceso a datos de una manera independiente del DBMS. Un administrador de controladores administra la comunicación entre las aplicaciones y controladores.  
  
 Aunque Microsoft proporciona un administrador de controladores para equipos que ejecutan Microsoft Windows® 95 y versiones posteriores, ha escrito varios controladores ODBC y llamadas a funciones ODBC de algunas de sus aplicaciones, que cualquier usuario puede escribir controladores y las aplicaciones de ODBC. De hecho, la mayoría de las aplicaciones ODBC y controladores disponibles hoy en día se escriben por otras empresas distintas de Microsoft. Además, las aplicaciones y controladores ODBC existen en el Macintosh® y una gran variedad de plataformas UNIX.  
  
 Para ayudar a los desarrolladores de aplicaciones y controladores, Microsoft ofrece un Kit de desarrollo de Software (SDK) de ODBC para equipos que ejecutan Windows 95 y versiones posteriores que proporciona el Administrador de controladores, installer DLL, las herramientas de prueba y aplicaciones de ejemplo. Microsoft se ha asociado con el Visigenic Software migrar estos SDK para Macintosh y una gran variedad de plataformas UNIX.  
  
 Es importante comprender que ODBC está diseñado para exponer las capacidades de la base de datos, no completarlas. Por lo tanto, los escritores de aplicaciones no deben esperar que usa ODBC repentinamente transforma una base de datos simple en un motor de base de datos relacional completo. Tampoco se esperan los escritores de controladores para implementar la funcionalidad que no se encuentra en la base de datos subyacente. Una excepción a esto es que los desarrolladores que escriben controladores que acceda directamente a los datos de archivo (por ejemplo, los datos en un archivo Xbase) necesarios para escribir un motor de base de datos que admite la funcionalidad SQL al menos mínima. Otro tipo de excepción es el componente ODBC del SDK de Windows, anteriormente incluida en Microsoft Data Access Components (MDAC) SDK, proporciona una biblioteca de cursores que simula los cursores desplazables para controladores que implementan un cierto nivel de funcionalidad.  
  
 Las aplicaciones que usan ODBC son responsables de cualquier funcionalidad entre bases de datos. Por ejemplo, ODBC no es un motor de combinación heterogéneo ni es un procesador de transacción distribuida. Sin embargo, dado que es independiente del DBMS, se puede utilizar para generar dichas herramientas entre bases de datos.
