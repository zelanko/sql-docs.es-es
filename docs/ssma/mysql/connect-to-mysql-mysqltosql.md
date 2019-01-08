---
title: Conectarse a MySQL (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 94099d01-ab19-4d58-a172-340c86b4a0f3
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 7289b3d5b287c1619a08921eba5cc30ff741e3b1
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2018
ms.locfileid: "52399908"
---
# <a name="connect-to-mysql-mysqltosql"></a>Conectarse a MySQL (MySQLToSQL)
Use la **conectar con MySQL** cuadro de diálogo para conectarse a la base de datos MySQL que se va a migrar.  
  
Para obtener acceso a este cuadro de diálogo, en el **archivo** menú, seleccione **conectar con MySQL**. Si se ha conectado anteriormente, el comando es **volver a conectar con MySQL**.  
  
## <a name="options"></a>Opciones  
**Proveedor**  
  
Proveedor de MySQL disponible es ODBC de MySQL 5.1 Driver (de confianza).  
  
**Modo**  
  
El modo predeterminado es el modo estándar. En modo estándar escriba o seleccione valores para el MySQL nombre del servidor, puerto del servidor, nombre de usuario y contraseña.  
  
**Nombre del servidor**  
  
Escriba el nombre del servidor MySQL. Esta es una opción de modo estándar.  
  
**Puerto del servidor**  
  
Escriba el puerto del servidor. El puerto de servidor predeterminado es 3306. Esta es una opción de modo estándar.  
  
**Nombre de usuario.**  
  
Escriba el nombre de usuario que va a usar para conectarse a la base de datos MySQL SSMA.  
  
**Contraseña**  
  
Escriba la contraseña del nombre de usuario.  
  
**SSL**  
  
Si desea conectarse de forma segura a MySQL, asegúrese de utilizar capa de sockets seguros (SSL) al comprobar la **SSL** casilla de verificación.  
  
**Configurar**  
  
Proporciona una opción para configurar la conexión a MySQL a través de la capa de sockets seguros (SSL).  
  
> [!NOTE]  
> Para habilitar **configurar**, SSL debe establecerse en **True**.  
  
Al hacer clic en el botón "Configurar", aparece un cuadro de diálogo. Para usar el cifrado mientras se conecta a la base de datos MySQL, ruta de acceso a los siguientes archivos de tres certificado presentes en el cuadro de diálogo debe ser definido [privacidad mejorada correo certificados (PEM)]:  
  
-   **Entidad emisora de certificados SSL:** Especifica la ruta de acceso a un archivo con una lista de confianza de entidades emisoras de certificados SSL.  
  
-   **Certificado SSL:** Especifica el nombre del archivo de certificado SSL que se utilizará para establecer una conexión segura.  
  
-   **CLAVE SSL:** Especifica el nombre del archivo de clave SSL que se utilizará para establecer una conexión segura.  
  
> [!NOTE]  
> -   El **Aceptar** botón se habilita cuando se ha proporcionado la información necesaria. Si cualquiera de las rutas de acceso de archivo son válida, el botón "Aceptar" permanecerá deshabilitado.  
> -   El **cancelar** botón cierra el cuadro de diálogo y **desactiva** la opción SSL desde el formulario principal de la conexión.  
  
