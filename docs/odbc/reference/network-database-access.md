---
description: Acceso a la base de datos de red
title: Acceso a la base de datos de red | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 025959072b7ebadc96fd1d1a628bdfaf5d449940
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461327"
---
# <a name="network-database-access"></a>Acceso a la base de datos de red
El acceso a una base de datos a través de una red requiere una serie de componentes, cada uno de los cuales es independiente de y reside en la interfaz de programación. Estos componentes se muestran en la ilustración siguiente.  
  
 ![Componentes para obtener acceso a una base de datos por toda una red](../../odbc/reference/media/pr04.gif "pr04")  
  
 A continuación se ofrece una descripción más detallada de cada componente:  
  
-   **Interfaz de programación** Tal y como se describió anteriormente en esta sección, la interfaz de programación contiene las llamadas realizadas por la aplicación. Estas interfaces (SQL incrustado, módulos SQL e interfaces de nivel de llamada) suelen ser específicas de cada DBMS, aunque normalmente se basan en un estándar ANSI o ISO.  
  
-   **Protocolo de flujo de datos** El protocolo de flujo de datos describe el flujo de datos transferido entre el DBMS y su cliente. Por ejemplo, el protocolo podría requerir el primer byte para describir lo que contiene el resto de la secuencia: una instrucción SQL que se va a ejecutar, un valor de error devuelto o datos devueltos. El formato del resto de los datos del flujo dependerá de esta marca. Por ejemplo, una secuencia de error podría contener la marca, un código de error entero de 2 bytes, una longitud de mensaje de error de un entero de 2 bytes y un mensaje de error.  
  
     El protocolo de flujo de datos es un protocolo lógico y es independiente de los protocolos usados por la red subyacente. Por lo tanto, se puede usar un único protocolo de flujo de datos en varias redes diferentes. Los protocolos de flujo de datos suelen ser propietarios y se han optimizado para trabajar con un DBMS determinado.  
  
-   **Mecanismo de comunicación entre procesos** El mecanismo de comunicación entre procesos (IPC) es el proceso por el que un proceso se comunica con otro. Algunos ejemplos son las canalizaciones con nombre, los Sockets TCP/IP y los sockets de DECnet. La elección del mecanismo IPC está restringida por el sistema operativo y la red que se utiliza.  
  
-   **Protocolo de red** El protocolo de red se usa para transportar el flujo de datos a través de una red. Se puede considerar la fontanería que admite los mecanismos IPC usados para implementar el protocolo de flujo de datos, así como la compatibilidad con operaciones de red básicas, como las transferencias de archivos y el uso compartido de impresoras. Los protocolos de red incluyen NetBEUI, TCP/IP, DECnet y SPX/IPX, y son específicos de cada red.
