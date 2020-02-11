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
ms.openlocfilehash: 6cb2f4196737cceec2f60684de1b7409f5e383a0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68083393"
---
# <a name="connect-to-sybase-sybasetosql"></a>Conectarse a Sybase (SybaseToSQL)
Utilice el cuadro de diálogo **conectar a Sybase** para conectarse a la instancia de Sybase Adaptive Server Enterprise (ASE) que desea migrar.  
  
Para obtener acceso a este cuadro de diálogo, en el menú **archivo** , seleccione **conectarse a Sybase**. Si ya se ha conectado, el comando se **vuelve a conectar a Sybase**.  
  
## <a name="options"></a>Opciones  
**Proveedor**  
Seleccione cualquiera de los proveedores instalados en el equipo para conectarse al servidor de Sybase.  
  
**Modo**  
Seleccione el modo de conexión estándar o avanzado. En el modo estándar, escriba o seleccione valores para el nombre del servidor, el puerto, el nombre de usuario y la contraseña. En el modo avanzado, se proporciona una cadena de conexión.  
  
**Nombre del servidor**  
Escriba o seleccione el nombre o la dirección IP del servidor adaptable. El nombre del servidor predeterminado es el mismo que el nombre del equipo. Se trata de una opción de modo estándar.  
  
**Puerto de servidor**  
Si usa un puerto no predeterminado para las conexiones con ASE, escriba el número de puerto. El número de puerto predeterminado es 5000. Se trata de una opción de modo estándar.  
  
**Nombre de usuario**  
Escriba el nombre de usuario que se usa para conectarse a ASE. Se trata de una opción de modo estándar.  
  
**Contraseña**  
Escriba la contraseña del nombre de usuario Se trata de una opción de modo estándar.  
  
**Cadena de conexión**  
Escriba la cadena de conexión completa para la conexión a ASE.  
  
Las cadenas de conexión constan de pares de nombre y valor de parámetro. Los nombres de los parámetros varían con el proveedor que se está usando.  
  
**Los parámetros de conexión para varios proveedores son los siguientes:**  
  
1.  Parámetros de conexión para el **proveedor de OLE DB**  
  
    |Configuración|Parámetro Sybase 12,5|Parámetro de Sybase 15|  
    |-----------|-------------------------|-----------------------|  
    |Nombre de servidor|Nombre del servidor|Server|  
    |Port|Dirección del puerto del servidor|Port|  
    |Nombre de usuario|Id. de usuario|Id. de usuario|  
    |Contraseña|Contraseña|Contraseña|  
    |Proveedor|Proveedor|Proveedor|  
  
    En el caso de Sybase ASE 12,5, una cadena de conexión de ejemplo es la siguiente:  
  
    `Server Name=sybserver;User ID=MyUserID;Password=MyP@$$word;Provider=Sybase.ASEOLEDBProvider;`  
  
    En el caso de Sybase ASE 15, una cadena de conexión de ejemplo es la siguiente:  
  
    `Server=sybserver;User ID=MyUserID;Password=MyP@$$word;Provider=ASEOLEDB;Port=5000;`  
  
2.  Parámetros de conexión para el **proveedor ODBC**  
  
    |Configuración|Parámetro de Sybase 12,5/15|  
    |-----------|-----------------------------|  
    |Nombre del controlador|controlador|  
    |Nombre del servidor|Server|  
    |User Name|UID|  
    |Contraseña|Pwd|  
    |Número de puerto|Port|  
  
    En el caso de Sybase ASE 12,5 o 15, una cadena de conexión de ejemplo es la siguiente:  
  
    `driver=Adaptive Server Enterprise;Server=sybserver;uid=MyUserID;pwd=MyP@$$word;Port=5000;`  
  
3.  Parámetros de conexión para el **proveedor ADO.net**  
  
    |Configuración|Parámetro de Sybase 12,5/15|  
    |-----------|-----------------------------|  
    |Nombre del servidor|Server|  
    |User Name|UID|  
    |Contraseña|Pwd|  
    |Número de puerto|Port|  
  
    Un ejemplo de la cadena de conexión para el proveedor ADO.NET es el siguiente:  
  
    `Server=sybserver;Port=5000;uid=MyUserID;pwd=MyP@$$word;`  
  
Para obtener más información, consulte la documentación de ASE.  
  
Se trata de una opción de modo avanzado.  
  
