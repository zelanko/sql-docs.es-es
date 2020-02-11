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
ms.openlocfilehash: 9ef460a7d004227e34e0043223abdf3769c92520
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68135660"
---
# <a name="compiling-an-embedded-sql-program"></a>Compilar un programa SQL incrustado
Dado que un programa SQL incrustado contiene una combinación de instrucciones de lenguaje de host y SQL, no se puede enviar directamente a un compilador para el idioma del host. En su lugar, se compila a través de un proceso de varios pasos. Aunque este proceso difiere del producto al producto, los pasos son aproximadamente los mismos para todos los productos.  
  
 En esta ilustración se muestran los pasos necesarios para compilar un programa SQL incrustado.  
  
 ![Pasos para compilar un programa SQL incrustado](../../odbc/reference/media/pr02.gif "pr02")  
  
 Hay cinco pasos implicados en la compilación de un programa SQL incrustado:  
  
1.  El programa SQL incrustado se envía al precompilador de SQL, una herramienta de programación. El precompilador examina el programa, busca las instrucciones SQL incrustadas y las procesa. Se requiere un precompilador diferente para cada lenguaje de programación admitido por el DBMS. Normalmente, los productos DBMS ofrecen precompiladores para uno o varios idiomas, incluidos C, Pascal, COBOL, Fortran, ADA, PL/I y varios lenguajes de ensamblado.  
  
2.  El precompilador genera dos archivos de salida. El primer archivo es el archivo de origen, que se ha quitado de las instrucciones SQL incrustadas. En su lugar, el precompilador sustituye las llamadas a las rutinas de DBMS de propiedad que proporcionan el vínculo en tiempo de ejecución entre el programa y el DBMS. Normalmente, los nombres y las secuencias de llamada de estas rutinas solo se conocen en el precompilador y en el DBMS; no son una interfaz pública para el DBMS. El segundo archivo es una copia de todas las instrucciones SQL incrustadas que se usan en el programa. Este archivo a veces se denomina módulo de solicitud de base de datos o DBRM.  
  
3.  La salida del archivo de código fuente del precompilador se envía al compilador estándar para el lenguaje de programación del host (por ejemplo, un compilador de C o COBOL). El compilador procesa el código fuente y genera el código del objeto como salida. Tenga en cuenta que este paso no tiene nada que hacer con el DBMS o con SQL.  
  
4.  El vinculador acepta los módulos de objeto generados por el compilador, los vincula con varias rutinas de biblioteca y genera un programa ejecutable. Las rutinas de biblioteca vinculadas al programa ejecutable incluyen las rutinas de DBMS de propiedad descritas en el paso 2.  
  
5.  El módulo de solicitud de base de datos generado por el precompilador se envía a una utilidad de enlace especial. Esta utilidad examina las instrucciones SQL, las analiza, las valida y las optimiza y, a continuación, genera un plan de acceso para cada instrucción. El resultado es un plan de acceso combinado para todo el programa, que representa una versión ejecutable de las instrucciones SQL incrustadas. La utilidad de enlace almacena el plan en la base de datos, lo que normalmente le asigna el nombre del programa de aplicación que lo utilizará. El hecho de que este paso tenga lugar en tiempo de compilación o en tiempo de ejecución depende del DBMS.  
  
 Tenga en cuenta que los pasos que se usan para compilar un programa SQL incrustado se correlacionan estrechamente con los pasos descritos anteriormente en [procesamiento de una instrucción SQL](../../odbc/reference/processing-a-sql-statement.md). En concreto, observe que el precompilador separa las instrucciones SQL del código de idioma del host, y la utilidad de enlace analiza y valida las instrucciones SQL y crea los planes de acceso. En los DBMS en los que el paso 5 tiene lugar en tiempo de compilación, los cuatro primeros pasos para procesar una instrucción SQL tienen lugar en tiempo de compilación, mientras que el último paso (ejecución) tiene lugar en tiempo de ejecución. Esto tiene el efecto de que la ejecución de consultas en estos DBMS sea muy rápida.
