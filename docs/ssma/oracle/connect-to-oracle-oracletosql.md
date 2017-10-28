---
title: Conectar con Oracle (OracleToSQL) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 23a48cb6-ff30-49bb-b4a7-603ebcab336f
caps.latest.revision: 5
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: d685be15fb8d0c6fea21d539e3370b3377316324
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="connect-to-oracle-oracletosql"></a>Conectar con Oracle (OracleToSQL)
Use la **conectar con Oracle** cuadro de diálogo para conectarse a la base de datos de Oracle que se va a migrar.  
  
Para tener acceso a este cuadro de diálogo, en la **archivo** menú, seleccione **conectar con Oracle**. Si se ha conectado anteriormente, el comando es **volver a conectar con Oracle**.  
  
## <a name="options"></a>Opciones  
**Proveedor**  
Seleccione el proveedor de acceso de datos para la conexión a la base de datos de Oracle. Proveedores disponibles están en el proveedor de cliente de Oracle y el proveedor OLE DB. El valor predeterminado es el proveedor de cliente de Oracle.  
  
**Modo**  
Seleccione modo estándar, TNSNAME o cadena de conexión.  
  
-   En modo estándar, escriba o seleccione valores para el proveedor, nombre del servidor, puerto del servidor, el SID de Oracle, nombre de usuario y la contraseña.  
  
-   En el modo TNSNAME, escriba el identificador de conexión (alias TNS) de la base de datos de Oracle, el nombre de usuario y la contraseña.  
  
-   En el modo de cadena de conexión, proporcionar una cadena de conexión.  
  
    > [!IMPORTANT]  
    > No se recomienda que use el modo de cadena de conexión porque el texto puede incluir las contraseñas, y se envía como texto sin cifrar.  
  
El valor predeterminado es el modo estándar.  
  
**Nombre del servidor**  
Escriba el nombre del servidor de Oracle. El nombre del servidor predeterminado es el mismo que el nombre del equipo. Se trata de una opción de modo estándar.  
  
**Puerto del servidor**  
Si está utilizando un número de puerto distinto 1521 (valor predeterminado) para las conexiones con Oracle, escriba el número de puerto. Se trata de una opción de modo estándar.  
  
**Identificador de conexión**  
Escriba el Oracle conectarse identificador. Éste es el alias de la base de datos tal como se define en el archivo tnsnames.ora local.  
  
Se trata de una opción de modo TNSNAME.  
  
**SID de Oracle**  
Escriba al SID de la base de datos. El SID es un identificador que distingue la base de datos de Oracle en un equipo. El valor predeterminado de SID para una base de datos es los ocho primeros caracteres del nombre de base de datos.  
  
Se trata de una opción de modo estándar.  
  
**Nombre de usuario.**  
Escriba el nombre de usuario que va a usar SSMA para conectarse a la base de datos de Oracle.  
  
**Contraseña**  
Escriba la contraseña del nombre de usuario.  
  
**Cadena de conexión**  
> [!IMPORTANT]  
> No se recomienda que use el modo de cadena de conexión porque el texto puede incluir las contraseñas, y se envía como texto sin cifrar.  
  
Si utiliza el modo de cadena de conexión, escriba la cadena de conexión completa para la conexión a Oracle.  
  
Las cadenas de conexión se componen de pares de nombre y valor de parámetro.  
  
-   Para información de la cadena de conexión de OLE DB, vea [proveedor Microsoft OLE DB para Oracle](http://go.microsoft.com/fwlink/?LinkId=85640) artículo en MSDN Library.  
  
SSMA para cadenas de conexión, siempre que incluya el parámetro de proveedor. Además, asegúrese de incluir el parámetro de puerto al conectarse a Oracle.  
  

