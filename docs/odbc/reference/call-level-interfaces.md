---
title: Interfaces de nivel de llamada ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4288a278f745d533c92d3d45892753ef1a74c2b3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306546"
---
# <a name="call-level-interfaces"></a>Interfaces de nivel de llamada
La técnica final para enviar instrucciones SQL al DBMS es a través de una interfaz de nivel de llamada (CLI). Una interfaz de nivel de llamada proporciona una biblioteca de funciones DBMS a las que puede llamar el programa de aplicación. Por lo tanto, en lugar de intentar combinar SQL con otro lenguaje de programación, una interfaz de nivel de llamada es similar a las bibliotecas de rutina que la mayoría de los programadores están acostumbrados a usar, como la cadena, E/S o bibliotecas matemáticas en C. Tenga en cuenta que los DBMS que admiten SQL incrustado ya tienen una interfaz de nivel de llamada, las llamadas a las que se generan mediante el precompilador. Sin embargo, estas llamadas son indocumentadas y están sujetas a cambios sin previo aviso.  
  
 Las interfaces de nivel de llamada se utilizan comúnmente en arquitecturas cliente/servidor, en las que el programa de aplicación (el cliente) reside en un equipo y el DBMS (el servidor) reside en un equipo diferente. La aplicación llama a las funciones CLI en el sistema local, y esas llamadas se envían a través de la red al DBMS para su procesamiento.  
  
 Una interfaz de nivel de llamada es similar a SQL dinámico, ya que las instrucciones SQL se pasan al DBMS para su procesamiento en tiempo de ejecución, pero difiere de SQL incrustado en su conjunto en que no hay instrucciones SQL incrustadas y no se requiere ningún precompilador.  
  
 El uso de una interfaz de nivel de llamada suele implicar los siguientes pasos:  
  
1.  La aplicación llama a una función CLI para conectarse al DBMS.  
  
2.  La aplicación crea una instrucción SQL y la coloca en un búfer. A continuación, llama a una o más funciones CLI para enviar la instrucción al DBMS para su preparación y ejecución.  
  
3.  Si la instrucción es una instrucción SELECT, la aplicación llama a una función CLI para devolver los resultados en los búferes de aplicación. Normalmente, esta función devuelve una fila o una columna de datos a la vez.  
  
4.  La aplicación llama a una función CLI para desconectarse del DBMS.
