---
title: Acceso de la base de datos de red | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], database access
- SQL [ODBC], database access
- database access [ODBC]
- network database access [ODBC]
- standardizing database access [ODBC], network
ms.assetid: f31dd938-e992-436b-b613-145c23973064
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1ff13d2e46377b0d29c9bbc8e8ad1705dedc048b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47633413"
---
# <a name="network-database-access"></a>Acceso a la base de datos de red
Acceso a una base de datos a través de una red, requiere una serie de componentes, cada uno de los cuales es independiente de y resida en la interfaz de programación. Estos componentes se muestran en la ilustración siguiente.  
  
 ![Componentes tengan acceso a una base de datos a través de una red](../../odbc/reference/media/pr04.gif "pr04")  
  
 A continuación se muestra una descripción detallada de cada componente:  
  
-   **Interfaz de programación** como se describió anteriormente en esta sección, la interfaz de programación contiene las llamadas realizadas por la aplicación. Estas interfaces (SQL, SQL incrustadas módulos e interfaces de nivel de llamada) son generalmente específicas de cada DBMS, aunque normalmente se basan en un estándar de ANSI o ISO.  
  
-   **Protocolo de datos Stream** el protocolo de flujo de datos describe el flujo de datos transferidos entre el DBMS y su cliente. Por ejemplo, el protocolo puede requerir el primer byte para describir lo que contiene el resto de la secuencia: una instrucción SQL que se ejecuta, un valor de error devuelto, o se devuelven datos. El formato del resto de los datos de la secuencia, a continuación, dependería de esta marca. Por ejemplo, un flujo de errores podría contener la marca, un código de error de entero de 2 bytes, una longitud de mensaje de error de entero de 2 bytes y un mensaje de error.  
  
     El protocolo de flujo de datos es un protocolo de lógico y es independiente de los protocolos utilizados por la red subyacente. Por lo tanto, generalmente puede utilizarse un protocolo de transmisión de datos única en varias redes distintas. Protocolos de transmisión de datos son normalmente propietarios y se han optimizado para trabajar con un DBMS concreto.  
  
-   **Entre procesos mecanismo de comunicación** el mecanismo de comunicación entre procesos (IPC) es el proceso por el que un proceso se comunica con otro. Algunos ejemplos son DECnet sockets, sockets de TCP/IP y canalizaciones con nombre. La elección del mecanismo IPC está restringida por el sistema operativo y la red que se utiliza.  
  
-   **Protocolo de red** el protocolo de red se utiliza para transportar el flujo de datos a través de una red. Se puede considerar la mecánica que admite los mecanismos IPC utilizados para implementar los datos de flujo de protocolo, así como admitir operaciones de red básica, como las transferencias de archivos y uso compartido de impresoras. Protocolos de red incluyen NetBEUI, TCP/IP, DECnet y SPX/IPX y son específicos de cada red.
