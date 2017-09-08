---
title: "Conéctese a DB2 (DB2ToSQL) | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 9d485fd0-ab5d-402a-a59a-e9982a61b7de
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 733fae47c5c74eb120b7f8719dd53675eb5b7e36
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="connect-to-db2-db2tosql"></a>Conéctese a DB2 (DB2ToSQL)
Use la **conectar a DB2** cuadro de diálogo para conectarse a la base de datos de DB2 que se va a migrar.  
  
Para tener acceso a este cuadro de diálogo, en la **archivo** menú, seleccione **conectar a DB2**. Si se ha conectado anteriormente, el comando es **volver a conectar a DB2**.  
  
## <a name="options"></a>Opciones  
**Proveedor**  
Seleccione el proveedor de acceso de datos para la conexión a la base de datos DB2. Proveedores disponibles son los proveedores de cliente DB2 y el proveedor OLE DB. El valor predeterminado es el proveedor de cliente de DB2.  
  
**Modo**  
Seleccione modo estándar, TNSNAME o cadena de conexión.  
  
-   En modo estándar, escriba o seleccione valores para el proveedor, nombre del servidor, puerto del servidor, DB2 SID, nombre de usuario y la contraseña.  
  
-   En el modo TNSNAME, escriba el identificador de conexión (alias TNS) de la base de datos de DB2, el nombre de usuario y la contraseña.  
  
-   En el modo de cadena de conexión, proporcionar una cadena de conexión.  
  
    > [!IMPORTANT]  
    > No se recomienda que use el modo de cadena de conexión porque el texto puede incluir las contraseñas, y se envía como texto sin cifrar.  
  
El valor predeterminado es el modo estándar.  
  
**Nombre del servidor**  
Escriba el nombre del servidor DB2. El nombre del servidor predeterminado es el mismo que el nombre del equipo. Se trata de una opción de modo estándar.  
  
**Puerto del servidor**  
Si está utilizando un número de puerto distinto 1521 (valor predeterminado) para las conexiones a DB2, escriba el número de puerto. Se trata de una opción de modo estándar.  
  
**Identificador de conexión**  
Escriba DB2 conectarse identificador. Éste es el alias de la base de datos tal como se define en el archivo tnsnames.ora local.  
  
Se trata de una opción de modo TNSNAME.  
  
**DB2 SID**  
Escriba al SID de la base de datos. El SID es un identificador que distingue la base de datos de DB2 en un equipo. El valor predeterminado de SID para una base de datos es los ocho primeros caracteres del nombre de base de datos.  
  
Se trata de una opción de modo estándar.  
  
**Nombre de usuario.**  
Escriba el nombre de usuario que va a usar para conectarse a la base de datos de DB2 SSMA.  
  
**Contraseña**  
Escriba la contraseña del nombre de usuario.  
  
**Cadena de conexión**  
> [!IMPORTANT]  
> No se recomienda que use el modo de cadena de conexión porque el texto puede incluir las contraseñas, y se envía como texto sin cifrar.  
  
Si utiliza el modo de cadena de conexión, escriba la cadena de conexión completa para la conexión a DB2.  
  
Las cadenas de conexión se componen de pares de nombre y valor de parámetro.  
  
-   Para información de la cadena de conexión de OLE DB, vea [proveedor Microsoft OLE DB para DB2](http://go.microsoft.com/fwlink/?LinkId=85640) artículo en MSDN Library.  
  
SSMA para cadenas de conexión, siempre que incluya el parámetro de proveedor. Además, asegúrese de incluir el parámetro de puerto cuando se conecta a DB2.  
  

