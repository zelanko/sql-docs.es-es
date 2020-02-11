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
manager: shamikg
ms.openlocfilehash: 42ab1e77dbdb7cee237a9ec22c49a725a64390c0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68264481"
---
# <a name="connect-to-oracle-oracletosql"></a>Conectarse a Oracle (OracleToSQL)
Utilice el cuadro de diálogo **conectar con Oracle** para conectarse a la base de datos de Oracle que desea migrar.  
  
Para obtener acceso a este cuadro de diálogo, en el menú **archivo** , seleccione **conectarse a Oracle**. Si ya se ha conectado, el comando se **vuelve a conectar a Oracle**.  
  
## <a name="options"></a>Opciones  
**Proveedor**  
Seleccione el proveedor de acceso a datos para la conexión a la base de datos de Oracle. Los proveedores disponibles son el proveedor de cliente de Oracle y el proveedor de OLE DB. El valor predeterminado es proveedor de cliente Oracle.  
  
**Modo**  
Seleccione estándar, TNSNAME o modo de cadena de conexión.  
  
-   En el modo estándar, escriba o seleccione los valores del proveedor, el nombre del servidor, el puerto del servidor, el SID de Oracle, el nombre de usuario y la contraseña.  
  
-   En el modo TNSNAME, escriba el identificador de conexión (alias TNS) de la base de datos de Oracle, el nombre de usuario y la contraseña.  
  
-   En el modo de cadena de conexión, se proporciona una cadena de conexión.  
  
    > [!IMPORTANT]  
    > No se recomienda usar el modo de cadena de conexión porque el texto podría incluir contraseñas y se envía como texto sin cifrar.  
  
El valor predeterminado es el modo estándar.  
  
**Nombre del servidor**  
Escriba el nombre del servidor de Oracle. El nombre del servidor predeterminado es el mismo que el nombre del equipo. Se trata de una opción de modo estándar.  
  
**Puerto de servidor**  
Si usa un número de puerto distinto de 1521 (predeterminado) para las conexiones a Oracle, escriba el número de puerto. Se trata de una opción de modo estándar.  
  
**Identificador de conexión**  
Escriba el identificador de conexión de Oracle. Este es el alias de la base de datos tal y como se define en el archivo archivo tnsnames. ora local.  
  
Se trata de una opción de modo TNSNAME.  
  
**SID de Oracle**  
Escriba el SID para la base de datos. El SID es un identificador que distingue la base de datos de Oracle en un equipo. El SID predeterminado de una base de datos de son los ocho primeros caracteres del nombre de la base de datos.  
  
Se trata de una opción de modo estándar.  
  
**Nombre de usuario**  
Escriba el nombre de usuario que SSMA usará para conectarse a la base de datos de Oracle.  
  
**Contraseña**  
Escriba la contraseña del nombre de usuario  
  
**Cadena de conexión**  
> [!IMPORTANT]  
> No se recomienda usar el modo de cadena de conexión porque el texto podría incluir contraseñas y se envía como texto sin cifrar.  
  
Si utiliza el modo de cadena de conexión, escriba la cadena de conexión completa para la conexión a Oracle.  
  
Las cadenas de conexión constan de pares de nombre y valor de parámetro.  
  
-   Para obtener OLE DB información de la cadena de conexión, vea [proveedor OLE DB de Microsoft para Oracle](https://go.microsoft.com/fwlink/?LinkId=85640) artículo en MSDN Library.  
  
En el caso de las cadenas de conexión de SSMA, incluya siempre el parámetro Provider. Además, asegúrese de incluir el parámetro de puerto al conectarse a Oracle.  
  
