---
title: Elegir datos de un origen o el controlador | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- connecting to driver [ODBC], selecting driver
- connecting to data source [ODBC], selecting data source
- data sources [ODBC], selecting
- ODBC drivers [ODBC], selecting
ms.assetid: 10aaf570-01ab-4478-8339-bdde2a5e3dd1
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d3e9c5964d529fa70bd82c3aec7d25a42cb10c08
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32913160"
---
# <a name="choosing-a-data-source-or-driver"></a>Elegir datos de un origen o el controlador
El origen de datos o el controlador utilizado por una aplicación a veces es codificado de forma rígida en la aplicación. Por ejemplo, una aplicación personalizada creada por el departamento de un MIS para transferir datos de un origen de datos a otro contendría los nombres de los orígenes de datos, la aplicación simplemente no funciona con cualquier otro origen de datos. Otro ejemplo es una aplicación vertical, como uno utilizado para la entrada de pedido. Este tipo de aplicación siempre utiliza el mismo origen de datos, que tiene un esquema predefinido conocido por la aplicación.  
  
 Otras aplicaciones seleccione el origen de datos o el controlador en tiempo de ejecución. Normalmente, estas son aplicaciones genéricas que realizar consultas ad hoc, como una hoja de cálculo que utiliza ODBC para importar datos. Estas aplicaciones normalmente enumeran los orígenes de datos disponibles o los controladores y permiten a los usuarios elegir las que desean trabajar. Si una aplicación genérica enumera los orígenes de datos, controladores o ambos con frecuencia depende de si la aplicación utiliza controladores basados en DBMS o basados en archivos.  
  
 Controladores basados en DBMS suelen requieran un conjunto complejo de información de conexión, como la dirección de red, protocolo de red, nombre de base de datos y así sucesivamente. El propósito de un origen de datos es ocultar toda esta información. Por lo tanto, el paradigma de origen de datos se presta a usar con controladores basados en DBMS. Una aplicación puede mostrar una lista de orígenes de datos para el usuario en uno de dos maneras. Puede llamar a **SQLDriverConnect** con el **DSN** palabra clave (nombre de origen de datos) y ningún valor asociado; el Administrador de controladores se mostrará una lista de nombres de origen de datos. Si la aplicación desea el control sobre la apariencia de la lista, llama a **SQLDataSources** para recuperar una lista de elementos disponibles orígenes de datos y crea su propio cuadro de diálogo. Esta función se implementa mediante el Administrador de controladores y se puede llamar antes de que se carguen todos los controladores. A continuación, la aplicación llama a una función de la conexión y pasa el nombre del origen de datos elegido.  
  
 Si no se especifica un origen de datos, se utiliza el origen de datos predeterminado indicado por la información del sistema. (Para obtener más información, consulte [subclave predeterminado](../../../odbc/reference/install/default-subkey.md).) Si **SQLConnect** llamar mediante un *ServerName* argumento que no se encuentra, es un puntero nulo o es "DEFAULT", el Administrador de controladores se conecta al origen de datos predeterminado. El valor predeterminado también se utiliza el origen de datos si la cadena de conexión que se utiliza en una llamada a **SQLDriverConnect** o **SQLBrowseConnect** contiene el **DSN** palabra clave se establece en "predeterminado "o si no se encuentra el origen de datos especificado. Además, el valor predeterminado se utiliza el origen de datos si la cadena de conexión que se utiliza en una llamada a **SQLDriverConnect** no contiene el **DSN** palabra clave.  
  
 Con los controladores basados en archivos, es posible utilizar un paradigma de archivo. Para los datos almacenados en el equipo local, los usuarios con frecuencia saben que sus datos en un archivo determinado, como Employee.dbf. En lugar de seleccionar un origen de datos desconocidos, resulta más fácil para que estos usuarios seleccionar el archivo que conocen. Para hacerlo, la aplicación llama primero a **SQLDrivers**. Esta función se implementa mediante el Administrador de controladores y se puede llamar antes de que se carguen todos los controladores. **SQLDrivers** devuelve una lista de controladores disponibles; también devuelve valores para la **FileUsage** y **FileExtns** palabras clave. El **FileUsage** palabra clave explica si controladores basados en archivos tratan archivos como tablas, como no Xbase o, como bases de datos, como hace Microsoft® Access. El **FileExtns** palabra clave enumera las extensiones de nombre de archivo que reconoce el controlador, tal como .dbf para un controlador de Xbase. Con esta información, la aplicación crea un cuadro de diálogo a través del cual el usuario elige un archivo. En función de la extensión de archivo elegido, la aplicación, a continuación, se conecta al controlador mediante una llamada a **SQLDriverConnect** con el **controlador** palabra clave.  
  
 No hay nada para detener una aplicación de uso de un origen de datos con un controlador basados en archivos o una llamada a **SQLDriverConnect** con el **controlador** (palabra clave) para conectarse a un controlador de DBMS. Estos son algunos usos comunes de la **controlador** palabra clave para controladores basados en DBMS:  
  
-   **No crear orígenes de datos.** Por ejemplo, una aplicación personalizada puede usar un controlador en particular y la base de datos. Si el nombre del controlador y toda la información necesaria para conectarse a la base de datos está codificado de forma rígida en la aplicación, los usuarios no es necesario que crear un origen de datos en su equipo para ejecutar la aplicación. Lo único que deben hacer es instalar la aplicación y el controlador.  
  
     Una desventaja de este método es que la aplicación se debe volver a compilar y redistribuir si cambia la información de conexión. Si un nombre de origen de datos está codificado de forma rígida en la aplicación en lugar de la información de conexión completa, cada usuario debe cambiar solo la información del origen de datos.  
  
-   **Obtener acceso a un DBMS determinado una sola vez.** Por ejemplo, podría contener una hoja de cálculo que recupera los datos mediante una llamada a funciones ODBC el **controlador** palabra clave para identificar un controlador en particular. Dado que el nombre del controlador es significativo para los usuarios que tienen ese controlador, la hoja de cálculo podría pasarse entre los usuarios. Si la hoja de cálculo contiene un nombre de origen de datos, cada usuario tendría que crear el mismo origen de datos para usar la hoja de cálculo.  
  
-   **Examinando el sistema para todas las bases de datos puede tener acceso a un controlador específico.** Para obtener más información, consulte [conectarse con SQLBrowseConnect](../../../odbc/reference/develop-app/connecting-with-sqlbrowseconnect.md), más adelante en esta sección.
