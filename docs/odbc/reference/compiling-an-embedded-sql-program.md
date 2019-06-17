---
title: Compilar un programa SQL incrustado | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL [ODBC], embedded SQL
- SQL statements [ODBC], embedded SQL
- compiling embedded SQL programs [ODBC]
- embedded SQL [ODBC]
ms.assetid: 9e94146a-5b80-4a01-b586-1e03ff05b9ac
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bc8133241ad0b76579e87164350a5c6fe2a39f2e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63186329"
---
# <a name="compiling-an-embedded-sql-program"></a>Compilar un programa SQL incrustado
Dado que un programa SQL incrustado contiene una combinación de las instrucciones de lenguaje SQL y el host, no se pueden enviar directamente a un compilador para el lenguaje del host. En su lugar, se compila mediante un proceso de varios pasos. Aunque este proceso es diferente del producto, los pasos son aproximadamente el mismo para todos los productos.  
  
 Esta ilustración muestra los pasos necesarios para compilar un programa SQL incrustado.  
  
 ![Pasos para compilar un programa SQL incrustado](../../odbc/reference/media/pr02.gif "pr02")  
  
 Cinco pasos implicados en compilar un programa SQL incrustado:  
  
1.  El programa SQL incrustado se envía al precompilador SQL, una herramienta de programación. El precompilador examina el programa, busca las instrucciones SQL incrustadas y los procesa. Falta un precompilador diferentes para cada lenguaje de programación compatible con el DBMS. Normalmente, los productos DBMS ofrecen precompilers para uno o varios idiomas, incluyendo C, Pascal, COBOL, Fortran, Ada, PL / me y varios lenguajes de ensamblado.  
  
2.  El precompilador genera dos archivos de salida. El primer archivo es el archivo de origen, sus instrucciones SQL insertadas que se han quitado. En su lugar, el precompilador sustituye las llamadas a rutinas DBMS propietarias que proporcionan el vínculo de tiempo de ejecución entre el programa y el DBMS. Normalmente, los nombres y las secuencias que realiza la llamada de estas rutinas solo conocen el precompilador y DBMS; no son una interfaz pública para el DBMS. El segundo archivo es una copia de todas las instrucciones SQL incrustadas que se utiliza en el programa. Este archivo se denomina a veces un módulo de solicitud de la base de datos o DBRM.  
  
3.  La salida del archivo de origen desde el precompilador se envía al compilador estándar para la programación de lenguaje (por ejemplo, un compilador de C o COBOL) del host. El compilador procesa el código fuente y genera código de objeto como su resultado. Tenga en cuenta que este paso no tiene nada que ver con el DBMS o con SQL.  
  
4.  El vinculador acepta los módulos de objeto generados por el compilador, vincula con distintas rutinas de biblioteca y genera un programa ejecutable. Las rutinas de biblioteca vinculadas en el programa ejecutable incluyen las rutinas DBMS propietarias que se describe en el paso 2.  
  
5.  El módulo de solicitudes de base de datos generado por el precompilador se envía a una utilidad de enlace especial. Esta utilidad examina las instrucciones SQL, analiza, valida y optimiza y, a continuación, genera un plan de acceso para cada instrucción. El resultado es un plan de acceso combinado para todo el programa, que representa una versión ejecutable de las instrucciones SQL incrustadas. La utilidad de enlace almacena el plan en la base de datos, normalmente le asigna el nombre de la aplicación que va a usar. Si este paso realiza en tiempo de compilación o tiempo de ejecución depende de la instancia de DBMS.  
  
 Tenga en cuenta que los pasos usados para compilar un programa SQL incrustado correlacionan muy de cerca con los pasos descritos anteriormente en [procesar una instrucción SQL](../../odbc/reference/processing-a-sql-statement.md). En concreto, tenga en cuenta que el precompilador separa las instrucciones SQL desde el código de idioma del host y la utilidad de enlace analiza y valida las instrucciones SQL y crea los planes de acceso. En el DBMS donde paso 5 realiza en tiempo de compilación, los cuatro primeros pasos de procesamiento de una instrucción SQL tienen lugar en tiempo de compilación, mientras que el último paso (ejecución) realiza en tiempo de ejecución. Esto tiene el efecto de realizar la ejecución de la consulta en este tipo DBMS muy rápidos.
