---
title: Interfaces de nivel de llamada | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL statements [ODBC], CLI
- CLI [ODBC], using CLI
- sending SQL statements to DBMS [ODBC]
- SQL [ODBC], CLI
- call-level interface [ODBC], using call-level interface
ms.assetid: 42257bb6-0bf1-4533-a4ef-4a6dd2aecb18
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 253a322e200f0da9046f5928385c5892265cbc19
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="call-level-interfaces"></a>Interfaces de nivel de llamada
La técnica final para enviar instrucciones SQL en el DBMS es a través de una interfaz de nivel de llamada (CLI). Una interfaz de nivel de llamada proporciona una biblioteca de funciones DBMS que puede llamarse mediante el programa de aplicación. Por lo tanto, en lugar de intentar SQL se combinen con otro lenguaje de programación, una interfaz de nivel de llamada es similar a las bibliotecas de rutina que los programadores están acostumbrados a utilizar, por ejemplo, la cadena, E/S o bibliotecas de matemáticas en C. tenga en cuenta que los DBMS que admiten SQL incrustado ya tiene una interfaz de nivel de llamada, las llamadas a la que se generan por el precompilador. Sin embargo, estas llamadas son no documentado y sujeto a cambios sin previo aviso.  
  
 Interfaces de nivel de llamada se usan habitualmente en las arquitecturas de cliente/servidor, en el que reside el programa de aplicación (cliente) en un equipo y el DBMS (el servidor) en un equipo diferente. La aplicación llama a funciones CLI en el sistema local, y esas llamadas se envían a través de la red para el sistema DBMS para su procesamiento.  
  
 Una interfaz de nivel de llamada es similar a SQL dinámico, ya que las instrucciones SQL se pasan al DBMS para el procesamiento en tiempo de ejecución, pero es diferente de SQL incrustado como un conjunto en que no hay ninguna instrucción SQL incrustada y no es necesario ningún precompilador.  
  
 Mediante una interfaz de nivel de llamada normalmente implica los pasos siguientes:  
  
1.  La aplicación llama a una función CLI para conectar con el DBMS.  
  
2.  La aplicación genera una instrucción SQL y lo coloca en un búfer. A continuación, llama a una o más funciones CLI para enviar la instrucción en el DBMS de preparación y ejecución.  
  
3.  Si la instrucción es una instrucción SELECT, la aplicación llama a una función CLI para devolver los resultados de los búferes de la aplicación. Normalmente, esta función devuelve una fila o una columna de datos a la vez.  
  
4.  La aplicación llama a una función CLI para desconectarse del DBMS.
