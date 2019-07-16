---
title: Elegir datos de un origen o el controlador | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connecting to driver [ODBC], selecting driver
- connecting to data source [ODBC], selecting data source
- data sources [ODBC], selecting
- ODBC drivers [ODBC], selecting
ms.assetid: 10aaf570-01ab-4478-8339-bdde2a5e3dd1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9aac31af80ff5774d464f76f130d2d113002e60a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68001398"
---
# <a name="choosing-a-data-source-or-driver"></a>Elegir datos de un origen o el controlador
El origen de datos o el controlador utilizado por una aplicación a veces es codificado de forma rígida en la aplicación. Por ejemplo, una aplicación personalizada escrita por un departamento MIS para transferir datos desde un origen de datos a otro contendría los nombres de los datos de orígenes de la aplicación simplemente no funcionarían con otros orígenes de datos. Otro ejemplo es una aplicación vertical, como uno utilizado para la entrada de pedidos. Este tipo de aplicación siempre usa el mismo origen de datos, que tiene un esquema predefinido conocido por la aplicación.  
  
 Otras aplicaciones seleccione el origen de datos o el controlador en tiempo de ejecución. Normalmente, estas son aplicaciones genéricas que realizar consultas ad hoc, por ejemplo, una hoja de cálculo que usa ODBC para importar datos. Estas aplicaciones normalmente una lista de los orígenes de datos disponibles o los controladores y permiten a los usuarios elegir las que desean trabajar. Si una aplicación genérica enumera los orígenes de datos, controladores o ambos con frecuencia depende de si la aplicación usa controladores basados en DBMS o basados en archivos.  
  
 Controladores basados en DBMS suelen requieran un conjunto complejo de información de conexión, como la dirección de red, protocolo de red, el nombre de base de datos y así sucesivamente. El propósito de un origen de datos es ocultar toda esta información. Por lo tanto, el paradigma de origen de datos se presta a usar con los controladores basados en DBMS. Una aplicación puede mostrar una lista de orígenes de datos al usuario en uno de dos maneras. Puede llamar a **SQLDriverConnect** con el **DSN** palabra clave (nombre de origen de datos) y ningún valor asociado; el Administrador de controladores se mostrará una lista de nombres de origen de datos. Si la aplicación desea un control sobre la apariencia de la lista, llama a **SQLDataSources** para recuperar una lista de disponibles orígenes de datos y crea su propio cuadro de diálogo. Esta función se implementa mediante el Administrador de controladores y se puede llamar antes de que todos los controladores se cargan. La aplicación, a continuación, llama a una función de conexión y lo pasa el nombre del origen de datos elegido.  
  
 Si no se especifica un origen de datos, se utiliza el origen de datos predeterminado indicado por la información del sistema. (Para obtener más información, consulte [subclave predeterminada](../../../odbc/reference/install/default-subkey.md).) Si **SQLConnect** se le llama mediante un *ServerName* argumento que no se encuentra, es un puntero nulo o es "DEFAULT", el Administrador de controladores se conecta al origen de datos de forma predeterminada. El valor predeterminado también se utiliza el origen de datos si la cadena de conexión que se utiliza en una llamada a **SQLDriverConnect** o **SQLBrowseConnect** contiene el **DSN** palabra clave establecida en "DEFAULT "o si no se encuentra el origen de datos especificado. Además, el valor predeterminado se utiliza el origen de datos si la cadena de conexión que se utiliza en una llamada a **SQLDriverConnect** no contiene el **DSN** palabra clave.  
  
 Con los controladores basados en archivos, es posible utilizar un paradigma de archivo. Para los datos almacenados en el equipo local, los usuarios con frecuencia saben que sus datos están en un archivo determinado, como Employee.dbf. En lugar de seleccionar un origen de datos desconocido, resulta más fácil para que estos usuarios seleccionar el archivo que conocen. Para implementar esto, la aplicación llama primero a **SQLDrivers**. Esta función se implementa mediante el Administrador de controladores y se puede llamar antes de que todos los controladores se cargan. **SQLDrivers** devuelve una lista de controladores disponibles; también devuelve valores para el **FileUsage** y **FileExtns** palabras clave. El **FileUsage** palabra clave explica si los controladores basados en archivos tratan archivos como tablas, como no Xbase o, como bases de datos, tal como hace Microsoft® Access. El **FileExtns** palabra clave enumera las extensiones de nombre de archivo que reconoce el controlador, tal como .dbf para un controlador de Xbase. Con esta información, la aplicación crea un cuadro de diálogo a través del cual el usuario elige un archivo. Basándose en la extensión del archivo elegida, la aplicación, a continuación, se conecta al controlador mediante una llamada a **SQLDriverConnect** con el **controlador** palabra clave.  
  
 No hay nada para detener una aplicación de uso de un origen de datos con un controlador basado en archivos o una llamada a **SQLDriverConnect** con el **controlador** palabra clave para conectarse a un controlador basados en DBMS. Estos son algunos de los usos comunes de la **controlador** palabra clave para controladores basados en DBMS:  
  
-   **No crear orígenes de datos.** Por ejemplo, una aplicación personalizada puede usar un controlador determinado y la base de datos. Si el nombre del controlador y toda la información necesaria para conectarse a la base de datos está codificado de forma rígida en la aplicación, los usuarios no es necesario que crear un origen de datos en su equipo para ejecutar la aplicación. Todo lo que deben hacer es instalar la aplicación y el controlador.  
  
     Una desventaja de este método es que la aplicación se debe volver a compilar y redistribuir si cambia la información de conexión. Si un nombre de origen de datos está codificado de forma rígida en la aplicación en lugar de la información de conexión completa, cada usuario debe cambiar solo la información del origen de datos.  
  
-   **Obtener acceso a un DBMS concreto una sola vez.** Por ejemplo, podría contener una hoja de cálculo que recupera datos mediante una llamada a funciones ODBC el **controlador** palabra clave para identificar un controlador determinado. Dado que el nombre del controlador es significativo para los usuarios que tengan ese controlador, la hoja de cálculo podría pasarse entre esos usuarios. Si la hoja de cálculo contiene un nombre de origen de datos, cada usuario tendría que crear el mismo origen de datos para usar la hoja de cálculo.  
  
-   **Examinar el sistema para todas las bases de datos accesibles para un controlador determinado.** Para obtener más información, consulte [conectar con SQLBrowseConnect](../../../odbc/reference/develop-app/connecting-with-sqlbrowseconnect.md), más adelante en esta sección.
