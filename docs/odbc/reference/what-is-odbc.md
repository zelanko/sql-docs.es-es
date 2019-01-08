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
manager: craigg
ms.openlocfilehash: cc9c7a3d9f75e1863d90b16986234e0036229d01
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52540440"
---
# <a name="what-is-odbc"></a>¿Qué es ODBC?
Existen muchas ideas erróneas sobre ODBC en el mundo de la informática. Para el usuario final, es un icono en el Panel de Control de Microsoft® Windows®. Para el programador de aplicaciones, es una biblioteca que contiene rutinas de acceso a datos. Para muchos otros, es la respuesta a todos los problemas de acceso de base de datos nunca imaginado.  
  
 En primer lugar y ante todo, ODBC es una especificación para una API de base de datos. Esta API es independiente del sistema operativo; ni un DBMS Aunque en este manual usa C, la API de ODBC es independiente del lenguaje. La API de ODBC se basa en las especificaciones de la CLI de Open Group y ISO/IEC. ODBC 3. *x* totalmente implementa ambas de estas especificaciones - versiones anteriores de ODBC se basaban en las versiones preliminares de estas especificaciones pero no totalmente implementó ellos - y agrega características normalmente necesarias los programadores de basado en pantalla aplicaciones de base de datos, como los cursores desplazables.  
  
 Las funciones de la API de ODBC se implementan los desarrolladores de controladores específicos de DBMS. Las aplicaciones llaman a las funciones de estos controladores para tener acceso a datos de manera independiente del DBMS. Un administrador de controladores administra la comunicación entre aplicaciones y controladores.  
  
 Aunque Microsoft proporciona un administrador de controladores para los equipos que ejecutan Microsoft Windows® 95 y versiones posteriores, ha escrito varios controladores ODBC y llama a las funciones ODBC de algunas de sus aplicaciones, cualquiera puede escribir controladores y aplicaciones de ODBC. De hecho, la mayoría de las aplicaciones ODBC y controladores disponibles hoy en día se escriben por empresas que no sean de Microsoft. Además, las aplicaciones y controladores ODBC existen en el Macintosh® y una variedad de plataformas UNIX.  
  
 Para ayudar a los desarrolladores de aplicaciones y los controladores, Microsoft ofrece un Kit de desarrollo de Software (SDK) de ODBC para los equipos que ejecutan Windows 95 y versiones posteriores que proporciona el Administrador de controladores, DLL de instalador, herramientas de pruebas y aplicaciones de ejemplo. Microsoft ha trabajado con Visigenic Software trasladar estos SDK para Macintosh y una variedad de plataformas UNIX.  
  
 Es importante comprender que ODBC está diseñado para exponer capacidades de base de datos, no para completarlas. Por lo tanto, los escritores de aplicaciones no deben esperar que utiliza ODBC, de repente, transformará una base de datos simple en un motor de base de datos relacional completa. Tampoco se esperan los escritores de controladores para implementar la funcionalidad que no se encuentra en la base de datos subyacente. Una excepción a esto es que los desarrolladores que escriben controladores que directamente tienen acceso a datos de archivo (por ejemplo, los datos en un archivo Xbase) son necesarios para escribir un motor de base de datos que admite la funcionalidad mínima al menos de SQL. Otro tipo de excepción es el componente ODBC del SDK de Windows, anteriormente incluida en Microsoft Data Access Components (MDAC) SDK, proporciona una biblioteca de cursores que simula los cursores desplazables para controladores que implementan un cierto nivel de funcionalidad.  
  
 Las aplicaciones que usan ODBC son responsables de ninguna funcionalidad entre bases de datos. Por ejemplo, no es un motor de combinación heterogéneo ODBC, ni es un procesador de la transacción distribuida. Sin embargo, dado que es independiente de DBMS, puede usar para crear dichas herramientas entre bases de datos.
