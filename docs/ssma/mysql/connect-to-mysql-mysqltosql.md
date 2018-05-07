---
title: Conectarse a MySQL (MySQLToSQL) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssma-mysql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 94099d01-ab19-4d58-a172-340c86b4a0f3
caps.latest.revision: 9
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 2290b67ac66a1fa06d62b88390a538a3e06621ec
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="connect-to-mysql-mysqltosql"></a>Conectarse a MySQL (MySQLToSQL)
Use la **conectar con MySQL** cuadro de diálogo para conectarse a la base de datos de MySQL que se va a migrar.  
  
Para tener acceso a este cuadro de diálogo, en la **archivo** menú, seleccione **conectar con MySQL**. Si se ha conectado anteriormente, el comando es **volver a conectar con MySQL**.  
  
## <a name="options"></a>Opciones  
**Proveedor**  
  
Proveedor de MySQL disponible es controlador de MySQL ODBC 5.1 (de confianza).  
  
**Modo**  
  
El modo predeterminado es el modo estándar. En modo estándar escriba o seleccione valores el MySQL, nombre del servidor, puerto del servidor, nombre de usuario, y una contraseña.  
  
**Nombre del servidor**  
  
Escriba el nombre del servidor MySQL. Se trata de una opción de modo estándar.  
  
**Puerto del servidor**  
  
Escriba el puerto del servidor. El puerto de servidor predeterminado es 3306. Se trata de una opción de modo estándar.  
  
**Nombre de usuario.**  
  
Escriba el nombre de usuario que va a usar para conectarse a la base de datos de MySQL SSMA.  
  
**Contraseña**  
  
Escriba la contraseña del nombre de usuario.  
  
**SSL**  
  
Si desea conectarse de forma segura MySQL, asegúrese de utilizar capa de sockets seguros (SSL) al comprobar la **SSL** casilla de verificación.  
  
**Configurar**  
  
Proporciona una opción para configurar la conexión de MySQL a través de la capa de sockets seguros (SSL).  
  
> [!NOTE]  
> Para habilitar **configurar**, SSL debe estar establecido en **True**.  
  
Al hacer clic en el botón "Configurar", aparece un cuadro de diálogo. Para utilizar el cifrado al conectarse a la base de datos de MySQL, ruta de acceso a los siguientes archivos de tres certificado presentes en el cuadro de diálogo debe ser define [privacidad mejorada correo certificados (PEM)]:  
  
-   **Entidad emisora de certificados SSL:** especifica la ruta de acceso a un archivo con una lista de confianza de entidades emisoras de certificados SSL.  
  
-   **Certificado SSL:** especifica el nombre del archivo de certificado SSL que se utilizará para establecer una conexión segura.  
  
-   **CLAVE de SSL:** especifica el nombre del archivo de clave de SSL que se utilizará para establecer una conexión segura.  
  
> [!NOTE]  
> -   El **Aceptar** botón se habilita cuando se ha proporcionado la información necesaria. Si cualquiera de las rutas de acceso de archivo son válido, el botón "Aceptar" permanecerá deshabilitado.  
> -   El **cancelar** botón cierra el cuadro de diálogo y **desactiva** la opción SSL desde el formulario de conexión principal.  
  
