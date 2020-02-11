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
ms.openlocfilehash: c6c37084ad91a931c4479ecf826c5cb554765412
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68135674"
---
# <a name="call-level-interfaces"></a>Interfaces de nivel de llamada
La técnica final para enviar instrucciones SQL al DBMS es a través de una interfaz de nivel de llamada (CLI). Una interfaz de nivel de llamada proporciona una biblioteca de funciones DBMS a las que puede llamar el programa de la aplicación. Por lo tanto, en lugar de intentar mezclar SQL con otro lenguaje de programación, una interfaz de nivel de llamada es similar a la mayoría de los programadores de las bibliotecas de rutinas están acostumbrados a usar, como las bibliotecas de cadenas, e/s o matemáticas en C. tenga en cuenta que los DBMS que admiten SQL incrustado ya tienen una interfaz de nivel de llamada, las llamadas Sin embargo, estas llamadas no están documentadas y están sujetas a cambios sin previo aviso.  
  
 Las interfaces de nivel de llamada se utilizan normalmente en las arquitecturas de cliente/servidor, en las que el programa de aplicación (el cliente) reside en un equipo y el DBMS (el servidor) reside en un equipo diferente. La aplicación llama a las funciones de la CLI en el sistema local y esas llamadas se envían a través de la red al DBMS para su procesamiento.  
  
 Una interfaz de nivel de llamada es similar a SQL dinámico, ya que las instrucciones SQL se pasan al DBMS para su procesamiento en tiempo de ejecución, pero difiere de SQL incrustado en su totalidad en que no hay instrucciones SQL incrustadas y no se requiere ningún precompilador.  
  
 El uso de una interfaz de nivel de llamada suele implicar los siguientes pasos:  
  
1.  La aplicación llama a una función de la CLI para conectarse al DBMS.  
  
2.  La aplicación crea una instrucción SQL y la coloca en un búfer. A continuación, llama a una o varias funciones de la CLI para enviar la instrucción al DBMS para su preparación y ejecución.  
  
3.  Si la instrucción es una instrucción SELECT, la aplicación llama a una función de la CLI para devolver los resultados en los búferes de la aplicación. Normalmente, esta función devuelve una fila o una columna de datos a la vez.  
  
4.  La aplicación llama a una función de la CLI para desconectarse del DBMS.
