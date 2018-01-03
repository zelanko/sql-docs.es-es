---
title: Acceso de base de datos de red | Documentos de Microsoft
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
- ODBC [ODBC], database access
- SQL [ODBC], database access
- database access [ODBC]
- network database access [ODBC]
- standardizing database access [ODBC], network
ms.assetid: f31dd938-e992-436b-b613-145c23973064
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: acdc1f994d6fd598051ceb2e4e955650f17ffc27
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="network-database-access"></a>Acceso a la base de datos de red
Acceso a una base de datos a través de una red, requiere un número de componentes, cada uno de los cuales es independiente de y resida en la interfaz de programación. Estos componentes se muestran en la ilustración siguiente.  
  
 ![Componentes tengan acceso a una base de datos a través de una red](../../odbc/reference/media/pr04.gif "pr04")  
  
 Obtener una descripción detallada de cada componente de la siguiente:  
  
-   **Interfaz de programación** tal y como se describió anteriormente en esta sección, la interfaz de programación contiene las llamadas realizadas por la aplicación. Estas interfaces (SQL, SQL incrustadas módulos e interfaces de nivel de llamada) son generalmente específicos de cada DBMS, aunque normalmente se basan en un estándar ANSI o ISO.  
  
-   **Protocolo de flujo de datos** el protocolo de flujo de datos describe el flujo de datos transferidos entre el DBMS y su cliente. Por ejemplo, el protocolo puede requerir el primer byte para describir el resto de la secuencia que contiene: una instrucción SQL que se ejecuta, un valor de error devuelto, o se devuelven datos. El formato del resto de los datos de la secuencia, a continuación, dependería de esta marca. Por ejemplo, una secuencia de error podría contener la marca, un código de error de entero de 2 bytes, una longitud de mensaje de error de entero de 2 bytes y un mensaje de error.  
  
     El protocolo de flujo de datos es un protocolo lógico y es independiente de los protocolos utilizados por la red subyacente. Por lo tanto, generalmente puede utilizarse un protocolo de flujo de datos único en una serie de distintas redes. Los protocolos de flujo de datos son normalmente propietarios y se han optimizado para trabajar con un DBMS concreto.  
  
-   **Entre procesos mecanismo de comunicación** el mecanismo de comunicación entre procesos (IPC) es el proceso por el que un proceso se comunica con otro. Algunos ejemplos son DECnet sockets, sockets TCP/IP y canalizaciones con nombre. La elección del mecanismo IPC está restringida por el sistema operativo y la red que se va a usar.  
  
-   **Protocolo de red** el protocolo de red se utiliza para transportar el flujo de datos a través de una red. Se puede considerar la mecánica que admite los mecanismos IPC utilizados para implementar los datos de secuencia de protocolo, así como admitir operaciones de red básica, como las transferencias de archivos y uso compartido de impresoras. Protocolos de red incluyen NetBEUI, TCP/IP, DECnet y SPX/IPX y son específicos de cada red.
