---
title: Interfaces de nivel de llamada | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], CLI
- CLI [ODBC], using CLI
- sending SQL statements to DBMS [ODBC]
- SQL [ODBC], CLI
- call-level interface [ODBC], using call-level interface
ms.assetid: 42257bb6-0bf1-4533-a4ef-4a6dd2aecb18
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 99ec2d9a1995502a4bfd96dad02157ccc6574f6c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47821109"
---
# <a name="call-level-interfaces"></a>Interfaces de nivel de llamada
La técnica final para enviar instrucciones SQL para el DBMS es a través de una interfaz de nivel de llamada (CLI). Una interfaz de nivel de llamada proporciona una biblioteca de funciones DBMS que puede llamarse mediante el programa de aplicación. Por lo tanto, en lugar de intentar fusionar SQL con otro lenguaje de programación, una interfaz de nivel de llamada es similar a las bibliotecas de rutina que mayoría de los programadores está acostumbrada a usar, como la cadena, E/S o bibliotecas de matemáticas en C. tenga en cuenta que los DBMS que admiten SQL incrustado ya tiene una interfaz de nivel de llamada, las llamadas a la que se generan por el precompilador. Sin embargo, estas llamadas son indocumentados y sujeta a cambios sin previo aviso.  
  
 Interfaces de nivel de llamada se usan normalmente en las arquitecturas de cliente/servidor, en el que reside el programa de aplicación (cliente) en un equipo y el DBMS (el servidor) en un equipo diferente. La aplicación llama a funciones de la CLI en el sistema local, y esas llamadas se envían a través de la red a la instancia de DBMS para su procesamiento.  
  
 Una interfaz de nivel de llamada es similar a SQL dinámico, en que las instrucciones SQL se pasan a la instancia de DBMS para el procesamiento en tiempo de ejecución, pero difiere de SQL incrustado como un todo en que no hay ninguna instrucción SQL incrustada y no es necesario ningún precompilador.  
  
 Mediante una interfaz de nivel de llamada normalmente implica los pasos siguientes:  
  
1.  La aplicación llama a una función de la CLI para conectarse a la instancia de DBMS.  
  
2.  La aplicación compila una instrucción SQL y lo coloca en un búfer. A continuación, llama a una o varias funciones CLI para enviar la instrucción a la instancia de DBMS para la preparación y ejecución.  
  
3.  Si la instrucción es una instrucción SELECT, la aplicación llama a una función de la CLI para devolver los resultados en búferes de la aplicación. Normalmente, esta función devuelve una fila o una columna de datos a la vez.  
  
4.  La aplicación llama a una función de la CLI para desconectarse del DBMS.
