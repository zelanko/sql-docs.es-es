---
title: Conexión a MySQL (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 94099d01-ab19-4d58-a172-340c86b4a0f3
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 3fe4b59a5131838357d7f58e5333e0ba6b9c80f2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68103230"
---
# <a name="connect-to-mysql-mysqltosql"></a>Conectarse a MySQL (MySQLToSQL)
Utilice el cuadro de diálogo **conectar con MySQL** para conectarse a la base de datos MySQL que desea migrar.  
  
Para obtener acceso a este cuadro de diálogo, en el menú **archivo** , seleccione **conectarse a MySQL**. Si ya se ha conectado, el comando se **vuelve a conectar a MySQL**.  
  
## <a name="options"></a>Opciones  
**Proveedor**  
  
El proveedor de MySQL disponible es el controlador de MySQL ODBC 5,1 (de confianza).  
  
**Modo**  
  
El modo predeterminado es el modo estándar. En el modo estándar, escriba o seleccione valores para MySQL, el nombre del servidor, el puerto del servidor, el nombre de usuario y la contraseña.  
  
**Nombre del servidor**  
  
Escriba el nombre del servidor MySQL. Se trata de una opción de modo estándar.  
  
**Puerto de servidor**  
  
Escriba el puerto del servidor. El puerto del servidor predeterminado es 3306. Se trata de una opción de modo estándar.  
  
**Nombre de usuario**  
  
Escriba el nombre de usuario que SSMA usará para conectarse a la base de datos MySQL.  
  
**Contraseña**  
  
Escriba la contraseña del nombre de usuario  
  
**SSL**  
  
Si desea conectarse de forma segura a MySQL, haga uso de la capa de sockets seguros (SSL). para ello, active la casilla **SSL** .  
  
**Configuración**  
  
Proporciona una opción para configurar la conexión a MySQL a través de la capa de sockets seguros (SSL).  
  
> [!NOTE]  
> Para habilitar **configurar**, SSL debe establecerse en **true**.  
  
Al hacer clic en el botón "configurar", aparece un cuadro de diálogo. Para usar el cifrado al conectarse a la base de datos MySQL, se debe definir la ruta de acceso a los tres archivos de certificado siguientes presentes en el cuadro de diálogo [certificados de correo mejorado de privacidad (PEM)]:  
  
-   **Entidad de certificación SSL:** Especifica la ruta de acceso a un archivo con una lista de entidades de certificación SSL de confianza.  
  
-   **Certificado SSL:** Especifica el nombre del archivo de certificado SSL que se va a usar para establecer una conexión segura.  
  
-   **clave SSL:** Especifica el nombre del archivo de clave SSL que se va a usar para establecer una conexión segura.  
  
> [!NOTE]  
> -   El botón **Aceptar** está habilitado cuando se ha proporcionado la información necesaria. Si alguna de las rutas de acceso de archivo no es válida, el botón "Aceptar" permanecerá deshabilitado.  
> -   El botón **Cancelar** cierra el cuadro de diálogo y **desactiva** la opción SSL del formulario de conexión principal.  
  
