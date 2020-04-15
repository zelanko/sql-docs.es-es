---
title: Elegir un origen de datos o un controlador ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b10aafad95463f56ec0f5a029eac59a02cff003b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303376"
---
# <a name="choosing-a-data-source-or-driver"></a>Elegir datos de un origen o el controlador
El origen de datos o el controlador utilizado por una aplicación a veces está codificado de forma rígida en la aplicación. Por ejemplo, una aplicación personalizada escrita por un departamento de MIS para transferir datos de un origen de datos a otro contendría los nombres de esos orígenes de datos: la aplicación simplemente no funcionaría con ningún otro origen de datos. Otro ejemplo es una aplicación vertical, como una utilizada para la entrada de pedidos. Dicha aplicación siempre utiliza el mismo origen de datos, que tiene un esquema predefinido conocido por la aplicación.  
  
 Otras aplicaciones seleccionan el origen de datos o el controlador en tiempo de ejecución. Normalmente, se trata de aplicaciones genéricas que realizan consultas ad hoc, como una hoja de cálculo que usa ODBC para importar datos. Estas aplicaciones suelen enumerar las fuentes de datos o controladores disponibles y permiten a los usuarios elegir los que desean trabajar con. Si una aplicación genérica enumera orígenes de datos, controladores o ambos con frecuencia depende de si la aplicación utiliza controladores basados en DBMS o basados en archivos.  
  
 Los controladores basados en DBMS suelen requerir un conjunto complejo de información de conexión, como la dirección de red, el protocolo de red, el nombre de la base de datos, etc. El propósito de un origen de datos es ocultar toda esta información. Por lo tanto, el paradigma del origen de datos se presta para su uso con controladores basados en DBMS. Una aplicación puede mostrar una lista de orígenes de datos al usuario de una de dos maneras. Puede llamar a **SQLDriverConnect** con la palabra clave **DSN** (Nombre de origen de datos) y ningún valor asociado; el Administrador de controladores mostrará una lista de nombres de origen de datos. Si la aplicación desea controlar la apariencia de la lista, llama a **SQLDataSources** para recuperar una lista de orígenes de datos disponibles y construye su propio cuadro de diálogo. Esta función es implementada por el Administrador de controladores y se puede llamar antes de que se carguen los controladores. A continuación, la aplicación llama a una función de conexión y le pasa el nombre del origen de datos elegido.  
  
 Si no se especifica un origen de datos, se utiliza el origen de datos predeterminado indicado por la información del sistema. (Para obtener más información, consulte [Subclave predeterminada](../../../odbc/reference/install/default-subkey.md).) Si **SQLConnect** se llama mediante un *ServerName* argumento que no se puede encontrar, es un puntero nulo o es "DEFAULT", el Administrador de controladores se conecta al origen de datos predeterminado. El origen de datos predeterminado también se utiliza si la cadena de conexión que se utiliza en una llamada a **SQLDriverConnect** o **SQLBrowseConnect** contiene la palabra clave **DSN** establecida en "DEFAULT" o si no se encuentra el origen de datos especificado. Además, se usa el origen de datos predeterminado si la cadena de conexión que se utiliza en una llamada a **SQLDriverConnect** no contiene la palabra clave **DSN.**  
  
 Con los controladores basados en archivos, es posible utilizar un paradigma de archivo. Para los datos almacenados en el equipo local, los usuarios saben con frecuencia que sus datos se encuentra en un archivo determinado, como Employee.dbf. En lugar de seleccionar un origen de datos desconocido, es más fácil para estos usuarios seleccionar el archivo que conocen. Para implementar esto, la aplicación llama primero **sqlDrivers**. Esta función es implementada por el Administrador de controladores y se puede llamar antes de que se carguen los controladores. **SQLDrivers** devuelve una lista de controladores disponibles; también devuelve valores para las palabras clave **FileUsage** y **FileExtns.** La palabra clave **FileUsage** explica si los controladores basados en archivos tratan los archivos como tablas, al igual que Xbase, o como bases de datos, al igual que Microsoft® Access. La palabra clave **FileExtns** enumera las extensiones de nombre de archivo que reconoce el controlador, como .dbf para un controlador Xbase. Con esta información, la aplicación construye un cuadro de diálogo a través del cual el usuario elige un archivo. En función de la extensión del archivo elegido, la aplicación se conecta al controlador llamando a **SQLDriverConnect** con la palabra clave **DRIVER.**  
  
 No hay nada que impida que una aplicación use un origen de datos con un controlador basado en archivos o que llame a **SQLDriverConnect** con la palabra clave **DRIVER** para conectarse a un controlador basado en DBMS. Aquí están varios usos comunes de la palabra clave **DRIVER** para los controladores basados en DBMS:  
  
-   **No crear orígenes de datos.** Por ejemplo, una aplicación personalizada podría usar un controlador y una base de datos determinados. Si el nombre del controlador y toda la información necesaria para conectarse a la base de datos está codificado de forma rígida en la aplicación, los usuarios no tienen que crear un origen de datos en su equipo para ejecutar la aplicación. Todo lo que deben hacer es instalar la aplicación y el controlador.  
  
     Una desventaja de este método es que la aplicación debe volver a compilarse y redistribuirse si cambia la información de conexión. Si un nombre de origen de datos está codificado de forma rígida en la aplicación en lugar de información de conexión completa, cada usuario debe cambiar solo la información del origen de datos.  
  
-   **Acceder a un DBMS determinado una sola vez.** Por ejemplo, una hoja de cálculo que recupera datos mediante una llamada a funciones ODBC puede contener la palabra clave **DRIVER** para identificar un controlador determinado. Dado que el nombre del controlador es significativo para los usuarios que tienen ese controlador, la hoja de cálculo podría pasarse entre esos usuarios. Si la hoja de cálculo contenía un nombre de origen de datos, cada usuario tendría que crear el mismo origen de datos para usar la hoja de cálculo.  
  
-   **Navegar por el sistema para todas las bases de datos accesibles para un controlador determinado.** Para obtener más información, consulte [Conexión con SQLBrowseConnect](../../../odbc/reference/develop-app/connecting-with-sqlbrowseconnect.md), más adelante en esta sección.
