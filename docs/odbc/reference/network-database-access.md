---
title: Acceso a la base de datos de red ( Network Database Access) Microsoft Docs
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
ms.openlocfilehash: 2237c725d6fe3696d1f28d80c09f22183f718de8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81295588"
---
# <a name="network-database-access"></a>Acceso a la base de datos de red
El acceso a una base de datos a través de una red requiere una serie de componentes, cada uno de los cuales es independiente de la interfaz de programación y reside debajo de ella. Estos componentes se muestran en la ilustración siguiente.  
  
 ![Componentes para obtener acceso a una base de datos por toda una red](../../odbc/reference/media/pr04.gif "pr04")  
  
 A continuación se describe más cada componente:  
  
-   **Interfaz de programación** Como se describió anteriormente en esta sección, la interfaz de programación contiene las llamadas realizadas por la aplicación. Estas interfaces (SQL incrustado, módulos SQL e interfaces de nivel de llamada) son generalmente específicas de cada DBMS, aunque normalmente se basan en un estándar ANSI o ISO.  
  
-   **Protocolo de flujo de datos** El protocolo de flujo de datos describe el flujo de datos transferidos entre el DBMS y su cliente. Por ejemplo, el protocolo puede requerir el primer byte para describir lo que contiene el resto de la secuencia: una instrucción SQL que se va a ejecutar, un valor de error devuelto o datos devueltos. El formato del resto de los datos de la secuencia dependería de esta marca. Por ejemplo, una secuencia de errores puede contener la marca, un código de error entero de 2 bytes, una longitud de mensaje de error entero de 2 bytes y un mensaje de error.  
  
     El protocolo de flujo de datos es un protocolo lógico y es independiente de los protocolos utilizados por la red subyacente. Por lo tanto, un solo protocolo de flujo de datos se puede utilizar generalmente en un número de redes diferentes. Los protocolos de flujo de datos suelen ser propietarios y se han optimizado para trabajar con un DBMS determinado.  
  
-   Mecanismo de **comunicación entre procesos** El mecanismo de comunicación entre procesos (IPC) es el proceso por el cual un proceso se comunica con otro. Los ejemplos incluyen canalizaciones con nombre, sockets TCP/IP y sockets DECnet. La elección del mecanismo IPC está limitada por el sistema operativo y la red que se utiliza.  
  
-   **Protocolo de red** El protocolo de red se utiliza para transportar el flujo de datos a través de una red. Se puede considerar la plomería que soporta los mecanismos IPC utilizados para implementar el protocolo de flujo de datos, así como el soporte de operaciones de red básicas como transferencias de archivos y uso compartido de impresión. Los protocolos de red incluyen NetBEUI, TCP/IP, DECnet y SPX/IPX y son específicos de cada red.
