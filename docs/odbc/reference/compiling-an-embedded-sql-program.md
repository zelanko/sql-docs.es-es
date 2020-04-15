---
title: Compilación de un programa SQL integrado ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: eb801dc532009410055b67031b3e036cc6b9c3d0
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306536"
---
# <a name="compiling-an-embedded-sql-program"></a>Compilar un programa SQL incrustado
Dado que un programa SQL incrustado contiene una combinación de instrucciones de lenguaje SQL y host, no se puede enviar directamente a un compilador para el lenguaje host. En su lugar, se compila a través de un proceso de varios pasos. Aunque este proceso difiere de un producto a otra, los pasos son aproximadamente los mismos para todos los productos.  
  
 Esta ilustración muestra los pasos necesarios para compilar un programa SQL incrustado.  
  
 ![Pasos para compilar un programa SQL incrustado](../../odbc/reference/media/pr02.gif "pr02")  
  
 Cinco pasos están implicados en la compilación de un programa SQL incrustado:  
  
1.  El programa SQL incrustado se envía al precompilador SQL, una herramienta de programación. El precompilador examina el programa, busca las instrucciones SQL incrustadas y las procesa. Se requiere un precompilador diferente para cada lenguaje de programación admitido por el DBMS. Los productos DBMS suelen ofrecer precompiladores para uno o más idiomas, incluidos C, Pascal, COBOL, Fortran, Ada, PL/I y varios lenguajes de ensamblado.  
  
2.  El precompilador genera dos archivos de salida. El primer archivo es el archivo de origen, despojado de sus instrucciones SQL incrustadas. En su lugar, el precompilador sustituye las llamadas a rutinas de DBMS propietarias que proporcionan el vínculo en tiempo de ejecución entre el programa y el DBMS. Normalmente, los nombres y las secuencias de llamada de estas rutinas solo se conocen para el precompilador y el DBMS; no son una interfaz pública para el DBMS. El segundo archivo es una copia de todas las instrucciones SQL incrustadas utilizadas en el programa. Este archivo a veces se denomina módulo de solicitud de base de datos o DBRM.  
  
3.  La salida del archivo de origen del precompilador se envía al compilador estándar para el lenguaje de programación host (por ejemplo, un compilador C o COBOL). El compilador procesa el código fuente y genera código de objeto como salida. Tenga en cuenta que este paso no tiene nada que ver con el DBMS o con SQL.  
  
4.  El vinculador acepta los módulos de objetos generados por el compilador, los vincula con varias rutinas de biblioteca y genera un programa ejecutable. Las rutinas de biblioteca vinculadas al programa ejecutable incluyen las rutinas de DBMS propietarias descritas en el paso 2.  
  
5.  El módulo de solicitud de base de datos generado por el precompilador se envía a una utilidad de enlace especial. Esta utilidad examina las instrucciones SQL, analiza, valida y optimiza y, a continuación, genera un plan de acceso para cada instrucción. El resultado es un plan de acceso combinado para todo el programa, que representa una versión ejecutable de las instrucciones SQL incrustadas. La utilidad de enlace almacena el plan en la base de datos, normalmente asignándole el nombre del programa de aplicación que lo usará. Si este paso tiene lugar en tiempo de compilación o en tiempo de ejecución depende del DBMS.  
  
 Observe que los pasos utilizados para compilar un programa SQL incrustado se correlacionan muy estrechamente con los pasos descritos anteriormente en Procesamiento de [una instrucción SQL](../../odbc/reference/processing-a-sql-statement.md). En particular, tenga en cuenta que el precompilador separa las instrucciones SQL del código de idioma host y la utilidad de enlace analiza y valida las instrucciones SQL y crea los planes de acceso. En LOS DBMS donde el paso 5 tiene lugar en tiempo de compilación, los primeros cuatro pasos de procesamiento de una instrucción SQL tienen lugar en tiempo de compilación, mientras que el último paso (ejecución) tiene lugar en tiempo de ejecución. Esto tiene el efecto de hacer que la ejecución de consultas en estos DBMS sea muy rápida.
