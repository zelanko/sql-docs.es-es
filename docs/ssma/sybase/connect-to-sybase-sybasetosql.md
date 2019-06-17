---
title: Conectarse a Sybase (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 524f95ef-10bd-497c-84ca-c06a0ae794fb
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 0805246d5b88138cfa97019d1e0cd524c82456c6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63061008"
---
# <a name="connect-to-sybase-sybasetosql"></a>Conectarse a Sybase (SybaseToSQL)
Use la **conectarse a Sybase** cuadro de diálogo para conectarse a la instancia de Sybase Adaptive Server Enterprise (ASE) que se va a migrar.  
  
Para obtener acceso a este cuadro de diálogo, en el **archivo** menú, seleccione **conectarse a Sybase**. Si se ha conectado anteriormente, el comando es **volver a conectar a Sybase**.  
  
## <a name="options"></a>Opciones  
**Proveedor**  
Seleccione cualquiera de lo proveedor instalado en el equipo para conectarse al servidor de Sybase.  
  
**Modo**  
Seleccione el modo de conexión estándar o avanzada. En el modo estándar, escriba o seleccione valores para el nombre del servidor, puerto, nombre de usuario y contraseña. En el modo avanzado, proporcionar una cadena de conexión.  
  
**Nombre del servidor**  
Escriba o seleccione el nombre o dirección IP del servidor adaptable. El nombre del servidor predeterminado es el mismo que el nombre del equipo. Esta es una opción de modo estándar.  
  
**Puerto del servidor**  
Si usa un puerto no predeterminado para las conexiones a la instancia de ASE, escriba el número de puerto. El número de puerto predeterminado es 5000. Esta es una opción de modo estándar.  
  
**Nombre de usuario.**  
Escriba el nombre de usuario que se usa para conectarse a la instancia de ASE. Esta es una opción de modo estándar.  
  
**Contraseña**  
Escriba la contraseña del nombre de usuario. Esta es una opción de modo estándar.  
  
**Cadena de conexión**  
Escriba la cadena de conexión completa para la conexión al ASE.  
  
Las cadenas de conexión constan de pares de nombre y valor de parámetro. Los nombres de los parámetros varían con el proveedor que se utiliza.  
  
**Parámetros de conexión de varios proveedores son los siguientes:**  
  
1.  Parámetros de conexión para **proveedor OLE DB**  
  
    |Parámetro|Parámetro de Sybase 12,5|Parámetro de Sybase 15|  
    |-----------|-------------------------|-----------------------|  
    |Nombre del servidor|Nombre del servidor|Servidor|  
    |Puerto|Dirección de puerto del servidor|Puerto|  
    |Nombre de usuario|Id. de usuario|Id. de usuario|  
    |Contraseña|Contraseña|Contraseña|  
    |Proveedor|Proveedor|Proveedor|  
  
    Para Sybase ASE 12,5, una cadena de conexión de ejemplo es el siguiente:  
  
    `Server Name=sybserver;User ID=MyUserID;Password=MyP@$$word;Provider=Sybase.ASEOLEDBProvider;`  
  
    Para Sybase ASE 15, una cadena de conexión de ejemplo es el siguiente:  
  
    `Server=sybserver;User ID=MyUserID;Password=MyP@$$word;Provider=ASEOLEDB;Port=5000;`  
  
2.  Parámetros de conexión para **proveedor ODBC**  
  
    |Parámetro|Parámetro de Sybase 12,5/15|  
    |-----------|-----------------------------|  
    |Nombre del controlador|controlador|  
    |Nombre del servidor|Servidor|  
    |Nombre de usuario|UID|  
    |Contraseña|Pwd|  
    |Número de puerto|Puerto|  
  
    Para Sybase ASE 12,5 o 15, una cadena de conexión de ejemplo es el siguiente:  
  
    `driver=Adaptive Server Enterprise;Server=sybserver;uid=MyUserID;pwd=MyP@$$word;Port=5000;`  
  
3.  Parámetros de conexión para **proveedor ADO.NET**  
  
    |Parámetro|Parámetro de Sybase 12,5/15|  
    |-----------|-----------------------------|  
    |Nombre del servidor|Servidor|  
    |Nombre de usuario|UID|  
    |Contraseña|Pwd|  
    |Número de puerto|Puerto|  
  
    Un ejemplo de la cadena de conexión para el proveedor ADO.NET es como sigue:  
  
    `Server=sybserver;Port=5000;uid=MyUserID;pwd=MyP@$$word;`  
  
Para obtener más información, consulte la documentación de ASE.  
  
Esta es una opción de modo avanzado.  
  
