---
title: Conectarse a Oracle (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 23a48cb6-ff30-49bb-b4a7-603ebcab336f
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: da846d4afb4ce8fe745b98c8503901fe804520e0
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/15/2018
ms.locfileid: "51681113"
---
# <a name="connect-to-oracle-oracletosql"></a>Conectarse a Oracle (OracleToSQL)
Use la **conectar con Oracle** cuadro de diálogo para conectarse a la base de datos de Oracle que se va a migrar.  
  
Para obtener acceso a este cuadro de diálogo, en el **archivo** menú, seleccione **conectar con Oracle**. Si se ha conectado anteriormente, el comando es **volver a conectar con Oracle**.  
  
## <a name="options"></a>Opciones  
**Proveedor**  
Seleccione el proveedor de acceso a datos para la conexión a la base de datos de Oracle. Los proveedores disponibles son el proveedor de cliente de Oracle y el proveedor OLE DB. El valor predeterminado es el proveedor de cliente de Oracle.  
  
**Modo**  
Seleccione modo estándar, TNSNAME o cadena de conexión.  
  
-   En el modo estándar, escriba o seleccione valores para el proveedor, nombre del servidor, puerto del servidor, el SID de Oracle, nombre de usuario y contraseña.  
  
-   En el modo TNSNAME, escriba el identificador de conexión (alias TNS) de la base de datos de Oracle, el nombre de usuario y la contraseña.  
  
-   En el modo de cadena de conexión, proporcione una cadena de conexión.  
  
    > [!IMPORTANT]  
    > No se recomienda que use el modo de cadena de conexión porque el texto puede incluir las contraseñas, y se envía como texto no cifrado.  
  
El valor predeterminado es el modo estándar.  
  
**Nombre del servidor**  
Escriba el nombre del servidor de Oracle. El nombre del servidor predeterminado es el mismo que el nombre del equipo. Esta es una opción de modo estándar.  
  
**Puerto del servidor**  
Si usa un número de puerto distinto 1521 (valor predeterminado) para las conexiones de Oracle, especifique el número de puerto. Esta es una opción de modo estándar.  
  
**Identificador de conexión**  
Escriba el oráculo de identificador de conexión. Éste es el alias de la base de datos tal como se define en el archivo tnsnames.ora local.  
  
Esta es una opción de modo TNSNAME.  
  
**SID de Oracle**  
Escriba al SID de la base de datos. El SID es un identificador que distingue de la base de datos de Oracle en un equipo. El valor predeterminado de SID para una base de datos es que los ocho primeros caracteres del nombre de base de datos.  
  
Esta es una opción de modo estándar.  
  
**Nombre de usuario.**  
Escriba el nombre de usuario que va a usar para conectarse a la base de datos de Oracle SSMA.  
  
**Contraseña**  
Escriba la contraseña del nombre de usuario.  
  
**Cadena de conexión**  
> [!IMPORTANT]  
> No se recomienda que use el modo de cadena de conexión porque el texto puede incluir las contraseñas, y se envía como texto no cifrado.  
  
Si usa el modo de cadena de conexión, escriba la cadena de conexión completa para la conexión a Oracle.  
  
Las cadenas de conexión constan de pares de nombre y valor de parámetro.  
  
-   Para información de la cadena de conexión de OLE DB, consulte [proveedor Microsoft OLE DB para Oracle](https://go.microsoft.com/fwlink/?LinkId=85640) artículo en MSDN Library.  
  
SSMA cadenas de conexión, siempre que incluya el parámetro de proveedor. Además, asegúrese de incluir el parámetro de puerto al conectarse a Oracle.  
  
